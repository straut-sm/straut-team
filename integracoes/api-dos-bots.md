# API dos bots: especificação

> **Status: ✅ construída pelo Straut Brain · App em 2026-11-26** (`straut-sm/straut-brain`,
> `src/app/api/bots/[...path]/route.ts` e `src/lib/bots.ts`). Testada no servidor local (27 testes).
> **Para ligar em produção:** o Guilherme cria a `BOTS_API_KEY` na Vercel (Production) e no OpenBot.
> Sem a chave, a API responde 503 e fica fechada.
>
> O pedido original segue abaixo; a seção **"Como usar (rotas reais)"** no fim tem o que foi
> construído, com exemplos.

## Por que existe
Hoje todo acesso ao painel passa pelo login da Straut ou pela senha da cliente (Server Actions em
`src/app/actions.ts`). Os bots do OpenBot precisam de uma porta própria, com regras claras e registro
de tudo o que fazem.

## Decisões
- **Uma chave única para todos os bots** (decisão do Guilherme, 2026-11-23).
  - Consequência: o sistema não diferencia um bot do outro. **Os limites de cada bot são garantidos
    pelas instruções**, não pela chave.
  - **Atualização 2026-11-26 (Guilherme):** os bots também podem apagar, marcar como publicado e
    aceitar sugestões. Apagar manda para a **Lixeira** do painel: o item fica 30 dias, o Guilherme pode
    restaurar, e só depois some de vez. Nada é apagado na hora.
  - Para o futuro: se algo sair do controle, criar chaves por bot (ex.: a Lari só com leitura).
- A chave fica guardada como segredo no OpenBot e na Vercel (`BOTS_API_KEY`). **Nunca** no GitHub.

## Autenticação e registro
- Cabeçalho `Authorization: Bearer <BOTS_API_KEY>`.
- Cabeçalho `X-Bot: <nome-do-bot>` obrigatório (`samuel`, `estrategia`, `design`, `lari`...).
- Toda ação de escrita entra no histórico do bloco como **Straut**, com o nome do bot no texto da ação
  (ex.: "Straut (bot design) adicionou 6 imagens"). Na tela da cliente aparece só "Straut".
- Limite de requisições (ex.: 60 por minuto) e log de acessos.

## Rotas propostas (prefixo `/api/bots`)

### Leitura
| Método | Rota | Retorna |
|---|---|---|
| GET | `/clientes` | Clientes ativas: slug, nome, especialidade, meta de posts por mês |
| GET | `/clientes/:slug/resumo?mes=AAAA-MM` | Meta, publicados, aprovados, em produção, aguardando aprovação, ajustes sugeridos, comentários não lidos |
| GET | `/clientes/:slug/blocos?de=AAAA-MM-DD&ate=AAAA-MM-DD&status=` | Blocos do período (sem mídias pesadas, só links temporários) |
| GET | `/blocos/:id` | Bloco completo: textos, status, mídias, sugestão pendente, comentários, histórico |
| GET | `/pendencias` | De todas as clientes: aguardando aprovação há mais de 48 horas, ajustes sugeridos, comentários novos |
| GET | `/blocos?data=AAAA-MM-DD&excluir_formato=roteiro` | Posts do dia de todas as clientes (rotina diária do Samuel), com status, mídias e **link direto** |
| GET | `/blocos?formato=reels&com_video=sim&sem_capa=sim` | Reels que já têm vídeo e ainda não têm capa (rotina do Design) |

Todo bloco retornado deve trazer um **`link`** para abrir aquele conteúdo direto no painel
(ex.: `https://painel.strautmarketing.com/c/<slug>?bloco=<id>`). O Samuel envia esse link ao Guilherme.
O painel já abre o bloco por esse link (verificado em 2026-11-26).

**A API nunca devolve** dados de acesso ou financeiros da cliente (senha da página, dia de pagamento),
os arquivos da cliente (contratos) nem chaves do sistema.

Melhorias sugeridas para depois da primeira versão (rota de novidades, marca "agendado no mLabs",
registro das ações dos bots): veja [`passagem-straut-brain.md`](passagem-straut-brain.md), seção 4.

### Escrita (pedido original; a versão final está em "Como usar")
| Método | Rota | Faz | Regras |
|---|---|---|---|
| POST | `/clientes/:slug/blocos` | Cria um bloco (data, formato, formato planejado, título, roteiro, legenda) | Sempre nasce `em_producao` |
| PATCH | `/blocos/:id` | Edita título, legenda, roteiro e data | Só se o status for `em_producao` ou `ajuste_sugerido`; guarda a versão anterior no histórico |
| POST | `/blocos/:id/upload-url` | Gera links de upload assinados (como `createUploadUrl`) | Só imagens e vídeos |
| POST | `/blocos/:id/midias` | Anexa as mídias enviadas (como `attachMedia`), na ordem | Não remove mídias existentes |
| PUT | `/blocos/:id/ordem-midias` | Reordena os slides | — |
| POST | `/blocos/:id/avancar` | Roteiro aprovado → formato planejado (como `advanceScript`) | Só roteiros `aprovado` |
| POST | `/blocos/:id/enviar-para-aprovacao` | `em_producao` → `aguardando_aprovacao` | Só a partir de `em_producao` |
| POST | `/blocos/:id/comentarios` | Comentário da Straut no bloco | — |

### Fora da API (só o Guilherme, pelo painel)
**Atualizado em 2026-11-26:** aprovar, recusar sugestões da cliente, restaurar versões, restaurar ou
apagar de vez itens da Lixeira, editar o cadastro da cliente, ativar ou desativar páginas, arquivos da cliente.

## Quem usa o quê (garantido pelas instruções)
| Bot | Usa |
|---|---|
Desde 2026-11-27 não há mais Gestores de cliente: as tarefas deles foram para o Samuel e a Estratégia.

| Bot | Usa |
|---|---|
| Samuel | Leitura + criar e editar blocos + avançar roteiros aprovados + enviar para aprovação (com autorização) + comentários + dias de produção + `novidades`. Apagar, publicar e aceitar sugestões estão liberados na API; **quem usa cada um é definido nas instruções dos bots** |
| Estratégia | Leitura (inclusive métricas, que lê **do painel**, não do mLabs) |
| Analista | Leitura + **gravar métricas** (`PUT /clientes/:slug/metricas`). É o único bot que busca números no mLabs |
| Social Media | Leitura + rascunhos da aba Tendências + "virar roteiro" |
| Copy | Leitura + criar blocos `roteiro` (`POST /clientes/:slug/blocos`) depois do Revisor + editar o texto deles (`PATCH`) |
| Revisor | Leitura (recebe e devolve pelo número do bloco) |
| Lari | Leitura + `novidades` (aprovações e comentários das clientes) |
| Design | Leitura + upload, anexar e reordenar mídias + comentários (link do Canva) |

O agendamento e a postagem são do Samuel, **no mLabs**, não pela API do painel.

---

## Como usar (rotas reais)

**Endereço:** `https://painel.strautmarketing.com/api/bots`

**Cabeçalhos em toda chamada:**
```
Authorization: Bearer <BOTS_API_KEY>
X-Bot: <nome-do-bot>          # minúsculas, números e hífen: samuel, design, estrategia, analista, lari...
Content-Type: application/json   # nas escritas
```

**Resposta:** sempre JSON. Sucesso: `{ "ok": true, "dados": ... }`. Erro: `{ "ok": false, "erro": "mensagem" }`.

| Código | Quando |
|---|---|
| 200 / 201 | Deu certo (201 ao criar bloco) |
| 400 | Pedido inválido (campo, data ou filtro errado); a mensagem diz o que corrigir |
| 401 | Chave errada ou ausente |
| 404 | Cliente inativa/inexistente, bloco ou rota não encontrados |
| 405 | Método não aceito naquela rota (ex.: DELETE, que não existe na API) |
| 409 | A regra não permite agora (ex.: editar bloco aguardando aprovação). **Não insista: avise o Samuel/Guilherme** |
| 429 | Passou de 60 requisições por minuto (por bot). Espere e tente de novo |
| 503 | API desligada (sem `BOTS_API_KEY` no servidor) |

### Formato de um bloco
```json
{
  "id": "uuid", "cliente": "jose-erasmo",
  "link": "https://painel.strautmarketing.com/c/jose-erasmo?bloco=<id>",
  "data": "2026-12-03", "titulo": "...", "formato": "roteiro | reels | carrossel | foto",
  "formato_planejado": "reels | carrossel | foto | null", "status": "em_producao | aguardando_aprovacao | ajuste_sugerido | aprovado | publicado",
  "legenda": "...", "roteiro": "...", "link_instagram": "https://www.instagram.com/reel/... | null",
  "midias": [{ "id": "uuid", "tipo": "video | capa | imagem", "url": "link temporário (1 h)", "google_drive": true }],
  "tem_video": true, "tem_capa": false,
  "sugestao_pendente": { "campo": "legenda | roteiro", "original": "...", "proposta": "...", "em": "ISO" },
  "comentarios_nao_lidos": 0
}
```
`GET /blocos/:id` traz também `comentarios` (`em, autor, bot, interno, lido, texto`) e `historico`
(`em, autor, bot, acao`).

### Leitura
| Rota | Observações |
|---|---|
| `GET /clientes` | Só clientes ativas: `slug, nome, especialidade, meta_posts_mes` |
| `GET /clientes/:slug/resumo?mes=AAAA-MM` | `mes` opcional (padrão: mês atual). Contagem por status de `posts` e de `roteiros`, `meta_posts`, `comentarios_nao_lidos` |
| `GET /clientes/:slug/blocos?de=&ate=&status=` | Tudo opcional. `status` aceita vários separados por vírgula |
| `GET /blocos/:id` | Bloco completo |
| `GET /pendencias` | `aguardando_aprovacao_ha_mais_de_48h` (com `aguardando_desde` e `horas_aguardando`), `ajustes_sugeridos`, `comentarios_novos` (com os textos) |
| `GET /blocos?...` | Todas as clientes ativas. Filtros: `data`, `de`, `ate`, `formato`, `excluir_formato`, `status`, `com_video=sim/nao`, `sem_capa=sim/nao`. **Exige ao menos um** de `data`, `de`, `ate`, `formato` ou `status` |
| `GET /novidades?desde=<ISO>` | O que mudou desde aquele momento, em ordem: `tipo` (`historico` ou `comentario`), `em`, `quem` (`cliente`, `straut` ou `bot <nome>`), `acao` ou `texto` (+ `interno`), e o bloco (`cliente, bloco_id, titulo, data, formato, status`). Filtros: `cliente=<slug>`, `autor=cliente\|straut`, `incluir_meus=sim` (por padrão esconde o que o próprio bot fez). `desde` até 14 dias atrás. Devolve `ate`: **guarde e use como o próximo `desde`**. Até 300 itens; com `limite_atingido: true`, consulte de novo a partir de `ate` |

**Use `novidades` em vez de varrer o painel.** Uma rotina que só precisa reagir (aprovação da cliente,
comentário, ajuste sugerido) consulta `GET /novidades?desde=<último ate>&autor=cliente` e, se `total`
for 0, encerra sem fazer mais nada. Guarde o último `ate` em `gestao/rotinas/registro.md`.

Exemplos das rotinas:
- Samuel, posts do dia: `GET /blocos?data=2026-12-03&excluir_formato=roteiro`
- Design, reels sem capa: `GET /blocos?formato=reels&com_video=sim&sem_capa=sim` (conta vídeos do Drive)

### Escrita
| Rota | Corpo | Regras |
|---|---|---|
| `POST /clientes/:slug/blocos` | `{ "data": "AAAA-MM-DD", "formato": "roteiro", "formato_planejado": "carrossel", "titulo": "...", "roteiro": "...", "legenda": "..." }` | Só `data` é obrigatória (`formato` padrão: roteiro). Nasce `em_producao`. Devolve 201 com o bloco |
| `PATCH /blocos/:id` | Qualquer um de `titulo`, `legenda`, `roteiro`, `data`, `link_instagram` | Em qualquer status. Guarda a versão anterior no histórico (o Guilherme pode desfazer) |
| `POST /blocos/:id/upload-url` | `{ "arquivos": [{ "extensao": "jpg" }, ...] }` (1 a 20) | Aceita jpg, jpeg, png, webp, heic, gif, mp4, mov, m4v, webm. Devolve `caminho` e `upload_url` de cada um |
| *(envio do arquivo)* | `PUT <upload_url>` com o arquivo no corpo e o `Content-Type` dele | Direto no armazenamento, sem chave |
| `POST /blocos/:id/midias` | `{ "tipo": "imagem", "caminhos": ["..."] }` ou `{ "tipo": "video", "link_drive": "https://drive.google.com/file/d/.../view" }` | Imagens só em carrossel/foto; vídeo e capa só em reels. Confere que o arquivo foi enviado. **Não substitui**: se o bloco já tem vídeo, capa ou foto, devolve 409; apague a atual antes (vai para a lixeira) |
| `PUT /blocos/:id/ordem-midias` | `{ "ids": ["id-da-imagem", ...] }` | A lista completa das imagens, na nova ordem |
| `POST /blocos/:id/avancar` | — | Só roteiro `aprovado` com `formato_planejado`. Vira o post em produção |
| `POST /blocos/:id/enviar-para-aprovacao` | — | Só a partir de `em_producao`. **Fase de testes: só com o ok do Guilherme** |
| `POST /blocos/:id/comentarios` | `{ "texto": "..." }` | **Comentário interno**: só a Straut vê, a cliente não. Para falar com a cliente, use a Lari pelo WhatsApp |
| `POST /blocos/:id/publicar` | — | Só posts (não roteiros) com status `aprovado` → `publicado` |
| `POST /blocos/:id/aceitar-sugestao` | — | Só com sugestão pendente (`ajuste_sugerido`): aplica o texto da cliente e o bloco fica `aprovado`. Guarda a versão anterior |
| `DELETE /blocos/:id` | — | Manda o bloco para a **Lixeira** (30 dias). Some do painel, da página da cliente e da API |
| `DELETE /blocos/:id/midias/:midiaId` | — | Manda a mídia para a **Lixeira** (30 dias) |

`link_instagram`: link do post publicado (instagram.com/p/... ou /reel/...). Liga o bloco às métricas;
`""` ou `null` tira. Não vale para roteiros. Só preencha com certeza: sem link, o painel liga o post ao
bloco pela data e pelo formato.

### Métricas do Instagram
A **Analista** é a única que busca números no mLabs e grava no painel. Os outros bots leem daqui
(`GET`), nunca do mLabs. Mesmas regras da página da cliente.

| Rota | Corpo | Observações |
|---|---|---|
| `GET /clientes/:slug/metricas?dias=90` | — | `sincronizado_em` (sem ele, `aguardando_sincronizacao: true` e nada mais); `resumo_do_mes` (período e comparação, `posts`, `alcance_medio` e `_variacao_pct`, `seguidores`, `seguidores_ganhos`, `salvamentos`, `compartilhamentos`, `media_alcance_90_dias`, `posts_com_estrela_no_mes`); `top3` (com `motivo`); `posts` dos últimos `dias` (até 150), cada um com `alcance, visualizacoes, curtidas, comentarios, salvamentos, compartilhamentos, estrela, bloco_id`; `seguidores` por dia |
| `PUT /clientes/:slug/metricas` | `{ "perfil_mlabs": "ext_...", "posts": [{ "link": "https://www.instagram.com/reel/...", "publicado_em": "2026-11-24T20:37:06Z", "formato": "reels \| carrossel \| foto", "alcance": 0, "visualizacoes": 0, "curtidas": 0, "comentarios": 0, "salvamentos": 0, "compartilhamentos": 0, "legenda": "...", "motivo": "..." }], "seguidores": [{ "data": "AAAA-MM-DD", "seguidores": 1198 }] }` | **Só a Analista.** Grava ou atualiza (pelo link do post e pela data); nunca apaga. `formato` aceita também os tipos do mLabs (`video`, `reel`, `carousel`, `image`). `motivo` é opcional: use só nos 3 melhores do mês que ainda não têm motivo; **um motivo escrito pela Straut nunca é trocado** (volta em `motivos_mantidos`). Até 500 posts e 400 dias por envio. Marca a cliente como sincronizada (sem isso, os gráficos dela ficam desfocados) |

Rotina da Analista (seg a sex, 9h): para cada cliente com perfil no mLabs, busque os posts e reels
publicados dos **últimos 45 dias** e o crescimento de seguidores, e mande tudo num `PUT` só por cliente.
Depois, escreva o motivo dos 3 melhores do mês que vierem com `motivo: null` no `GET`.

Regras: mês atual (dia 1 até hoje) contra os mesmos dias do mês anterior; estrela = alcance acima da
média dos últimos 90 dias; top 3 = maior alcance + salvamentos + compartilhamentos. Variação em %
pode vir `null` quando não dá para comparar.

### Dias de produção
Evento no calendário com a lista dos roteiros para gravar. Não é post: não conta na meta nem tem status.
A lista e as marcações são só visuais: não mudam a data nem o status dos blocos.

| Rota | Corpo | Regras |
|---|---|---|
| `GET /clientes/:slug/producao?de=&ate=` | — | Dias da cliente: `id, data, titulo, observacoes, link` |
| `GET /producao/:id` | — | O dia com `para_gravar` (na ordem), `gravados` e `escondidos`; cada item é um bloco com `estado`. Entram os roteiros ainda não gravados em outro dia |
| `POST /clientes/:slug/producao` | `{ "data": "AAAA-MM-DD", "titulo": "...", "observacoes": "..." }` | Só `data` é obrigatória. Devolve 201 com o dia |
| `PATCH /producao/:id` | Qualquer um de `data`, `titulo`, `observacoes` | — |
| `PUT /producao/:id/roteiros/:blocoId` | `{ "estado": "pendente \| gravado \| oculto" }` | Marca o roteiro no dia (`oculto` = não vamos gravar) |
| `PUT /producao/:id/ordem` | `{ "ids": ["id-do-bloco", ...] }` | Nova ordem da lista para gravar |
| `DELETE /producao/:id` | — | Manda o dia para a **Lixeira** (30 dias) |

### Aba Tendências
Uma semana (segunda-feira) por vez, com `tendencia_do_mes`, `referencias` e `stories`. A seção
"Para gravar" saiu: cada referência tem "Virar roteiro". Os bots leem tudo e criam ou editam
**rascunhos**; liberar a semana para a cliente é só com o Guilherme, pelo painel.

| Rota | Corpo | Regras |
|---|---|---|
| `GET /clientes/:slug/tendencias?semanas=4` ou `?semana=AAAA-MM-DD` | — | Semanas mais recentes primeiro (até 12), com `liberada`. Cada item: `id, semana, tipo, titulo, texto, perfil, link, destaque, como_adaptar, passos, posicao, criado_por, liberado` |
| `GET /tendencias/:id` | — | Um item |
| `POST /clientes/:slug/tendencias` | `{ "semana": "AAAA-MM-DD", "tipo": "mercado \| referencia \| stories", "titulo": "...", "texto": "...", "perfil": "@perfil", "link": "https://...", "destaque": "Reels · 85 mil visualizações", "como_adaptar": "...", "passos": ["..."] }` | `semana` padrão: a atual (qualquer dia vira a segunda). Referência **precisa** de `link` de um post real. Entra como rascunho, com `criado_por` = "bot <nome>". 409 se a semana já foi liberada |
| `PATCH /tendencias/:id` | Qualquer campo acima | Só rascunho (409 se já liberado) |
| `DELETE /tendencias/:id` | — | Só rascunho. Vai para a **Lixeira** (30 dias) |
| `POST /tendencias/:id/virar-roteiro` | `{ "data": "AAAA-MM-DD" }` (opcional; padrão hoje) | Cria um roteiro em produção no calendário com o texto, o "como adaptar" e o link. Formato planejado: Reels, ou carrossel/foto se a referência for post do feed. Devolve 201 com o bloco |

**Lixeira:** o Guilherme vê tudo o que foi apagado no botão **Lixeira** do painel, com quem apagou
(ex.: "bot samuel") e quantos dias faltam, e pode restaurar. Depois de 30 dias o item e
os arquivos são apagados de vez por uma rotina diária. Os bots não restauram nem apagam de vez.

### O que fica registrado
- **Histórico do bloco:** autor "Straut" e o nome do bot numa coluna própria (`block_history.bot`). No
  painel, a Straut vê "Straut · bot design"; a cliente vê só "Straut".
- **Registro de acessos:** cada chamada com chave válida grava bot, método, rota, bloco e código de
  resposta na tabela `bot_requests` (também usada no limite por minuto).
