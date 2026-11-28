# Rotinas (agendamentos no OpenBot)

O OpenBot permite **até 20 rotinas ativas**, com intervalo mínimo de 15 minutos. Horário de Brasília.
**O time usa 11 rotinas.** Os números antigos foram mantidos para não quebrar referências.

**Ajuste de 2026-11-28, noite (Guilherme):** rotina 3 com **um horário só, 13h** (avanços, pedidos ao
Design e pendências na mesma mensagem); rotina 19 às **7h**; todas as rotinas **ativas, menos a 18**.

**Mudanças de 2026-11-28 (Guilherme):**
- **Excluídas:** 1 (posts do dia do Samuel), 2 (resumo semanal do Samuel), 7 (artes e capas do
  Design), 14 (avisos da Lari) e 15, 16 e 17 (todas do Tráfego, por enquanto).
  - Posts do dia, agendamento no mLabs e resumo semanal: o Samuel faz **quando o Guilherme pedir**.
  - Artes e capas: o Design trabalha **quando o Samuel pedir** (o Samuel vê na rotina 3 o que precisa).
  - Avisos às clientes (aprovação pendente, lembrete de gravação, recorde): a Lari envia **quando o
    Guilherme pedir**.
  - Tráfego: sem rotinas; trabalha só quando o Guilherme ou o Samuel pedir.
- **Social Media (rotina 10):** pesquisa as tendências e preenche a aba Tendências do painel com
  **3 virais do nicho e 4 ideias de stories** por cliente.
- **Lari (rotinas 12 e 13):** envia as ideias de stories e os reels virais **direto da aba Tendências
  do painel**, nos mesmos dias e horários.

**Mudanças de 2026-11-27 (com o Claude):** os Gestores de cliente foram desativados (tarefas com o
Samuel e a Estratégia); a Analista sincroniza as métricas do painel (rotina 19); a checagem do Samuel
usa `GET /novidades` e roda às 11h30 e às 17h30 (rotina 3).

## Calendário de produção (um mês de antecedência)

```
Dia 20 do mês M-1   Estratégia  → pauta do mês M+1          (ex.: 20/dez → pauta de fevereiro)
Dia 1  do mês M     Samuel      → confere se o mês M bateu a meta → pedido de produção à Estratégia
                    Estratégia  → passo 1: calendário + perguntas para a cliente (com perguntas, espera)
                                → briefing ao Copy (um por cliente)
                    Copy        → ROTEIROS de todos os conteúdos do mês M+1 → Revisor
                                → Copy cria os blocos no painel → números ao Samuel
                    Samuel      → ok do Guilherme → aprovação da cliente (até o dia 5)
Dias úteis 13h      Samuel      → novidades do painel: roteiro aprovado → avança e pede ao Design a arte;
                                   reels com vídeo e sem capa → pede a capa ao Design
Quando você pedir   Samuel      → posts do dia → seu ok → agenda e posta no mLabs
```

## Semana de tendências

```
Segunda 7h    Social Media → aba Tendências (rascunho): 3 virais do nicho + 4 ideias de stories por cliente
              Guilherme    → revisa e LIBERA a semana no painel (antes das 14h)
Segunda 14h   Lari         → envia as ideias de stories da semana liberada
Terça 10h     Lari         → envia os reels virais da semana liberada
```

## Lista de rotinas

| # | Bot | Quando | Tarefa |
|---|---|---|---|
| 3 | Samuel | Segunda a sexta, **13h** | Novidades do painel: avançar roteiros aprovados, pedir artes e capas ao Design, encaminhar ajustes e comentários; na mesma execução, autorizações, atrasos e escalonamentos (uma mensagem só) |
| 4 | Samuel | **Dia 1, 9h** | Pedido de produção do mês seguinte à Estratégia |
| 5 | Estratégia | **Dia 20, 9h** | Pauta do mês M+1 (dois meses à frente) para cada cliente |
| 8 | Analista | Dia 1, 9h | Relatório mensal de cada cliente |
| 9 | Analista | **Quarta, 10h** | Recordes de desempenho (posts dos últimos 7 dias, lidos do painel) → Lari |
| 10 | Social Media | **Segunda, 7h** | Pesquisa de tendências → aba Tendências do painel: 3 virais do nicho + 4 ideias de stories por cliente |
| 11 | Lari | **Segunda, 9h** | Zerar os contadores + mensagem de bom dia e boa semana |
| 12 | Lari | **Segunda, 14h** | Enviar as ideias de stories da aba Tendências (semana liberada) |
| 13 | Lari | **Terça, 10h** | Enviar os reels virais da aba Tendências (semana liberada) |
| 18 | Manu | **Quinta, 10h** | Referências visuais da semana + olhar de feed de cada cliente → observações ao Design |
| 19 | Analista | **Segunda a sexta, 7h** | Sincronizar o painel com o mLabs (posts, seguidores, motivo do top 3) |

**Excluídas:** 1, 2, 6, 7, 14, 15, 16 e 17. As mensagens que chegam das clientes no WhatsApp acionam
a Lari na hora (não precisam de rotina).

## Segurança das rotinas
Cada rotina segue [`referencias/rotinas-seguras.md`](../referencias/rotinas-seguras.md). Todas
obedecem à **"PAUSA GERAL"** e registram o que fizeram em `gestao/rotinas/registro.md` (só quando agem).

| # | Só age quando | Memória (para não repetir) | Para / chama humano quando |
|---|---|---|---|
| 3 | `GET /novidades` trouxe algo, há reels com vídeo e sem capa, ou há pendência ou escalonamento sem retorno | Último `ate` em `gestao/rotinas/registro.md` | Nada novo → não faz nada e não envia mensagem |
| 4 | Dia 1 | `calendario/AAAA-MM.md` de cada cliente | Pauta do mês ausente → avisa a Estratégia e o Guilherme; mês atual abaixo da meta → avisa o Guilherme primeiro |
| 5 | Dia 20 | `estrategia/pauta-AAAA-MM.md` | Cliente sem posicionamento definido → avisa o Samuel |
| 8 | Dia 1 | `relatorios/AAAA-MM.md` | mLabs sem dados → avisa, não inventa números |
| 9 | Há post que atende ao critério de recorde | Tabela de recordes em `desempenho.md` | Post já avisado → pula; número muito fora do normal → confirma antes |
| 10 | Segunda | A semana na aba Tendências do painel | Nada adequado ao posicionamento → grava menos itens (melhor nada que algo ruim); semana já liberada → não mexe |
| 11 | Cliente sem conversa ativa e sem mensagem sem resposta | "Mensagens de boa semana" em `atendimento.md` | Conversa ativa → não envia |
| 12–13 | Semana liberada pelo Guilherme, limite livre e conversa livre | Contador em `atendimento.md` | Semana não liberada → não envia e avisa o Guilherme uma vez; conversa ativa ou limite atingido → fica pendente até o Guilherme pedir |
| 18 | Quinta | `criativo/referencias.md` + referências das clientes | Nada fora do guia no feed → não manda mensagem; imagem que não abriu → avisa, não avalia |
| 19 | Dias úteis, para cada cliente com perfil no mLabs | `sincronizado_em` no painel | mLabs fora do ar → tenta na próxima; 2 dias seguidos sem sincronizar → avisa o Samuel |

## Texto das rotinas (para colar no OpenBot)

3. **Samuel · novidades do painel:** "Consulte `GET /novidades?desde=<último ate de
   gestao/rotinas/registro.md>&autor=cliente` e `GET /blocos?formato=reels&com_video=sim&sem_capa=sim`.
   Roda uma vez por dia útil, às 13h. Para cada roteiro
   aprovado, avance o bloco para o formato planejado e acione quem vem depois: carrossel → peça a arte
   ao Design; reels → dia de produção no painel e direção da Manu; foto → Manu. Para cada reels com
   vídeo e sem capa, peça a capa ao Design (só o número do bloco). Para cada ajuste sugerido ou
   comentário, encaminhe a quem fez só com o número do bloco. Grave o novo `ate`. Na mesma execução,
   verifique autorizações pendentes, conteúdos atrasados em relação à meta e escalonamentos da Lari
   sem retorno e me envie UMA mensagem agrupada (o que foi avançado ou pedido + pendências) só se
   houver algo. Se não houver nada, encerre sem mensagem."
4. **Samuel · pedido de produção:** "Para cada cliente, confira no painel se o mês atual bateu a meta;
   se não, avise o Guilherme primeiro. Depois mande à Estratégia o `modelos/pedido-de-producao.md`
   preenchido de cada cliente: roteiros de TODOS os conteúdos do mês seguinte, na quantidade da meta
   de posts no painel. Junte as perguntas para as clientes que a Estratégia trouxer no passo 1, envie
   ao Guilherme numa só mensagem e espere as respostas antes de liberar a produção. O Design não entra
   nessa etapa. Meta: lote revisado no painel e pronto para o ok do Guilherme até o dia 5."
5. **Estratégia · pautas:** "Gere a pauta do mês M+1 (dois meses à frente: hoje é dia 20 do mês M-1)
   para cada cliente ativa, conforme `equipe/estrategia.md`, e grave no repositório."
8. **Analista · relatórios:** "Gere o relatório do mês anterior de cada cliente ativa conforme
   `modelos/relatorio-mensal.md`, grave no repositório e avise a Estratégia e o Samuel com o caminho
   do arquivo e as 3 recomendações principais."
9. **Analista · recordes:** "Leia do painel (`GET /clientes/:slug/metricas?dias=90`) os posts dos
   últimos 7 dias de cada cliente. Se algum for recorde pelo critério de `equipe/analista.md`, envie
   para a Lari."
10. **Social Media · tendências da semana:** "Pesquise as tendências da semana e, para cada cliente
    ativa (exceto a Straut), preencha a semana atual da aba Tendências do painel como rascunho
    (`POST /clientes/<slug>/tendencias`): **3 virais do nicho** (`tipo: referencia`: post real com
    `link` e `perfil`, `destaque` começando pelo formato e com os números, `titulo` = o gancho,
    `como_adaptar` para a cliente) e **4 ideias de stories** (`tipo: stories`, com `passos` que a
    cliente faz sozinha). Fonte principal: os melhores posts das contas de referência no mLabs; complete
    com o Instagram de pesquisa e a web. Aplique os filtros de `equipe/social-media.md`. Não libere a
    semana (é do Guilherme) e não envie mensagem."
11. **Lari · boa semana:** "Zere os contadores semanais em `atendimento.md` de cada cliente. Depois,
    no WhatsApp Web já conectado, para cada cliente (exceto a Straut) que NÃO tenha mensagem sem
    resposta nem conversa ativa, envie no grupo dela uma mensagem curta de bom dia e boa semana de
    trabalho, diferente das últimas 4 semanas (veja `atendimento.md`), com as suas regras de escrita,
    e registre o texto enviado. WhatsApp fora do ar → não envia e avisa o Samuel uma vez."
12. **Lari · stories da semana:** "Para cada cliente (exceto a Straut), leia a semana atual da aba
    Tendências (`GET /clientes/<slug>/tendencias?semana=<segunda desta semana>`). Se a semana estiver
    LIBERADA, envie as ideias de stories numa só mensagem curta, no tom de WhatsApp, com o link
    https://painel.strautmarketing.com/p/<slug> (conta como a sugestão de stories da semana). Respeite
    todas as regras de envio e registre em `atendimento.md`. Se a semana não estiver liberada, não
    envie e mande ao Guilherme uma única mensagem com as clientes que estão esperando liberação."
13. **Lari · reels virais da semana:** "Para cada cliente (exceto a Straut), leia a semana atual da aba
    Tendências. Se estiver LIBERADA, envie os reels virais numa só mensagem curta (link de cada um, por
    que funciona e como adaptar, em uma linha cada), com o link da página da cliente (conta como a
    sugestão de reels viral da semana). Se os stories não saíram na segunda, podem ir junto. Respeite
    todas as regras de envio e registre em `atendimento.md`. Semana não liberada → avise o Guilherme
    uma vez. Conversa ativa ou limite atingido → fica pendente até o Guilherme pedir."
18. **Manu · referências visuais e olhar de feed:** "Salve de 3 a 5 referências VISUAIS da semana
    (link, o que observar, por que funciona, para qual cliente serve) em `criativo/referencias.md` ou
    na pasta da cliente, só links, nunca imagens. Referência de tema e gancho é da Social Media: não
    repita. Depois veja no painel os posts publicados e os próximos de cada cliente e compare com o
    guia visual. Se houver quebra de consistência, texto ilegível ou cara de IA, mande uma observação
    objetiva ao Design. Se não houver nada, não envie mensagem."
19. **Analista · sincronizar métricas:** "Para cada cliente ativa com perfil no mLabs, busque os posts
    e reels publicados dos últimos 45 dias e o crescimento de seguidores e grave tudo num único
    `PUT /clientes/<slug>/metricas`, **montado por script a partir do retorno bruto do mLabs (nunca
    redigitar números)**. Depois leia `GET /clientes/<slug>/metricas`, confira com o mesmo script que
    todos os números batem e, para os posts do top 3 sem motivo, escreva o motivo (1 a 2 frases) e mande só esses posts de novo com `motivo`.
    Não envie mensagem, a não ser que uma cliente fique 2 dias úteis sem sincronizar."
