# API dos bots: especificação

> **Status: 🚧 a construir pelo Straut Brain · App** no repositório `straut-sm/straut-brain`.
> Este documento é o pedido. Quando a API estiver pronta, o Straut Brain atualiza este arquivo com as
> rotas reais e muda o status para ✅.

## Por que existe
Hoje todo acesso ao painel passa pelo login da Straut ou pela senha da cliente (Server Actions em
`src/app/actions.ts`). Os bots do OpenBot precisam de uma porta própria, com regras claras e registro
de tudo o que fazem.

## Decisões
- **Uma chave única para todos os bots** (decisão do Guilherme, 2026-11-23).
  - Consequência: o sistema não diferencia um bot do outro. **Os limites de cada bot são garantidos
    pelas instruções**, não pela chave. Por isso a API **não oferece** nenhuma operação destrutiva.
  - Para o futuro: se algo sair do controle, criar chaves por bot (ex.: a Lari só com leitura).
- A chave fica guardada como segredo no OpenBot e na Vercel (`BOTS_API_KEY`). **Nunca** no GitHub.

## Autenticação e registro
- Cabeçalho `Authorization: Bearer <BOTS_API_KEY>`.
- Cabeçalho `X-Bot: <nome-do-bot>` obrigatório (`samuel`, `gestor-juliana-annunciato`, `design`, `lari`...).
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

### Escrita (sem nada destrutivo)
| Método | Rota | Faz | Regras |
|---|---|---|---|
| POST | `/clientes/:slug/blocos` | Cria um bloco (data, formato, formato planejado, título, roteiro, legenda) | Sempre nasce `em_producao` |
| PATCH | `/blocos/:id` | Edita título, legenda, roteiro e data | Só se o status for `em_producao` ou `ajuste_sugerido`; guarda a versão anterior no histórico |
| POST | `/blocos/:id/upload-url` | Gera links de upload assinados (como `createUploadUrl`) | Só imagens e vídeos |
| POST | `/blocos/:id/midias` | Anexa as mídias enviadas (como `attachMedia`), na ordem | Não remove mídias existentes |
| PUT | `/blocos/:id/ordem-midias` | Reordena os slides | — |
| POST | `/blocos/:id/enviar-para-aprovacao` | `em_producao` → `aguardando_aprovacao` | Só a partir de `em_producao` |
| POST | `/blocos/:id/comentarios` | Comentário da Straut no bloco | — |

### Fora da API (só o Guilherme, pelo painel)
Apagar blocos ou mídias, aprovar, marcar como publicado, aceitar ou recusar sugestões da cliente,
restaurar versões, editar o cadastro da cliente, ativar ou desativar páginas, arquivos da cliente.

## Quem usa o quê (garantido pelas instruções)
| Bot | Usa |
|---|---|
| Samuel, Analista, Estratégia, Social Media, Copy, Revisor, Lari | Só leitura |
| Gestores | Leitura + criar e editar blocos + enviar para aprovação (com autorização) + comentários |
| Design | Leitura + upload, anexar e reordenar mídias |
