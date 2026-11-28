# Rotinas (agendamentos no OpenBot)

O OpenBot permite **até 20 rotinas ativas**, com intervalo mínimo de 15 minutos. Horário de Brasília.

**Mudanças de 2026-11-27 (Guilherme):**
- Os Gestores de cliente foram desativados; as tarefas foram para o Samuel e a Estratégia.
- A **Analista** passou a sincronizar as métricas do painel (rotina 19, nova). A rotina do Claude que
  fazia isso no computador do Guilherme será desligada.
- A **Social Media** passou a preencher a aba Tendências (rotina 10). A rotina do Claude que fazia isso
  será desligada.
- A checagem do Samuel usa `GET /novidades` e ganhou um horário às 11h30 (rotina 3).
- As rotinas 3 e 14 só agem se houver novidade. Sem novidade, encerram sem mensagem.

## Calendário de produção (um mês de antecedência)

```
Dia 20 do mês M-1   Estratégia  → pauta do mês M+1          (ex.: 20/dez → pauta de fevereiro)
Dia 1  do mês M     Samuel      → confere se o mês M bateu a meta → pedido de produção à Estratégia
                    Estratégia  → passo 1: calendário + perguntas para a cliente (com perguntas, espera)
                                → briefing ao Copy (um por cliente)
                    Copy        → ROTEIROS de todos os conteúdos do mês M+1 → Revisor
                                → Copy cria os blocos no painel → números ao Samuel
                    Samuel      → ok do Guilherme → aprovação da cliente (até o dia 5)
Todo dia útil       Design      → ARTES dos carrosséis com roteiro aprovado e CAPAS dos reels que já
                                   têm vídeo no painel
Todo dia            Samuel      → posts do dia → ok do Guilherme → agenda e posta no mLabs
```

## Lista de rotinas

| # | Bot | Quando | Tarefa |
|---|---|---|---|
| 1 | Samuel | **Todos os dias, 8h** | Posts do dia: enviar ao Guilherme (com links do painel) → com o ok, agendar no mLabs |
| 2 | Samuel | Segunda, 8h30 | Resumo semanal → `gestao/semanal/` → enviar ao Guilherme |
| 3 | Samuel | Segunda a sexta, **11h30 e 17h30** | Novidades do painel: avançar roteiros aprovados, encaminhar ajustes e comentários; às 17h30, também autorizações, atrasos e escalonamentos |
| 4 | Samuel | **Dia 1, 9h** | Pedido de produção do mês seguinte à Estratégia |
| 5 | Estratégia | **Dia 20, 9h** | Pauta do mês M+1 (dois meses à frente) para cada cliente |
| 6 | — | — | Removida em 2026-11-26 |
| 7 | Design | **Segunda a sexta, 11h** | Artes dos carrosséis com roteiro aprovado e capas dos reels que já têm vídeo no painel |
| 8 | Analista | Dia 1, 9h | Relatório mensal de cada cliente |
| 9 | Analista | **Quarta, 10h** | Recordes de desempenho (posts dos últimos 7 dias, lidos do painel) → Lari |
| 10 | Social Media | **Segunda, 7h** | Aba Tendências (rascunho) + stories da semana + reels viral de cada cliente → Lari |
| 11 | Lari | **Segunda, 9h** | Zerar os contadores + mensagem de bom dia e boa semana |
| 12 | Lari | **Segunda, 14h** | Enviar as ideias de stories prontas |
| 13 | Lari | **Terça, 10h** | Enviar os reels virais prontos (o que não sair fica na fila da rotina 14) |
| 14 | Lari | Segunda a sexta, 10h30 e 15h30 | Avisos de aprovação pendente, lembretes de gravação e fila |
| 15 | Tráfego | Segunda a sexta, 9h30 | Checagem de fatos: gasto × ritmo, anúncios reprovados, conta e pagamento, rastreamento |
| 16 | Tráfego | Sexta, 10h | Checagem semanal com decisão por conta → relatório → Samuel |
| 17 | Tráfego | Dia 25, 9h | Plano de mídia do mês seguinte de cada cliente que anuncia |
| 18 | Manu | **Quinta, 10h** | Referências visuais da semana + olhar de feed de cada cliente → observações ao Design |
| 19 | Analista | **Segunda a sexta, 9h** | Sincronizar o painel com o mLabs (posts, seguidores, motivo do top 3) |

As mensagens que chegam das clientes no WhatsApp acionam a Lari na hora (não precisam de rotina).
As rotinas 15 a 17 do Tráfego só são ativadas a partir da fase 1.

## Segurança das rotinas
Cada rotina segue [`referencias/rotinas-seguras.md`](../referencias/rotinas-seguras.md). Todas
obedecem à **"PAUSA GERAL"** e registram o que fizeram em `gestao/rotinas/registro.md` (só quando agem).

| # | Só age quando | Memória (para não repetir) | Para / chama humano quando |
|---|---|---|---|
| 1 | Há posts com data de hoje (não roteiro) | Comentário "Agendado no mLabs" no bloco | Sem ok do Guilherme → não agenda; mLabs com erro → avisa |
| 2 | Sempre (segunda) | `gestao/semanal/` | Dados do painel indisponíveis → avisa e envia o que tiver |
| 3 | `GET /novidades` trouxe algo, ou há pendência ou escalonamento sem retorno (17h30) | Último `ate` em `gestao/rotinas/registro.md` | Nada novo → não faz nada e não envia mensagem |
| 4 | Dia 1 | `calendario/AAAA-MM.md` de cada cliente | Pauta do mês ausente → avisa a Estratégia e o Guilherme; mês atual abaixo da meta → avisa o Guilherme primeiro |
| 5 | Dia 20 | `estrategia/pauta-AAAA-MM.md` | Cliente sem posicionamento definido → avisa o Samuel |
| 6 | — | — | Removida |
| 7 | Há carrossel com roteiro aprovado e sem arte, ou reels com vídeo e sem capa | Comentário com o link do Canva e mídias no bloco | Cliente sem modelo no Canva → avisa a Manu, não inventa estilo; nada pendente → não faz nada |
| 8 | Dia 1 | `relatorios/AAAA-MM.md` | mLabs sem dados → avisa, não inventa números |
| 9 | Há post que atende ao critério de recorde | Tabela de recordes em `desempenho.md` | Post já avisado → pula; número muito fora do normal → confirma antes |
| 10 | Segunda | Semana na aba Tendências + `sugestoes/AAAA-MM-DD.md` | Nada adequado ao posicionamento → não sugere (melhor nada que algo ruim) |
| 11 | Cliente sem conversa ativa e sem mensagem sem resposta | "Mensagens de boa semana" em `atendimento.md` | Conversa ativa → não envia |
| 12–13 | Sugestão marcada como pronta e limite livre | Contador + status em `sugestoes/` | Limite atingido ou conversa ativa → fila |
| 14 | Pendência há mais de 48 horas, lembrete ou fila, com limite livre | Contador em `atendimento.md` | Mesmo aviso nas últimas 48 horas → não repete |
| 15 | Gasto 30% ou mais fora do ritmo, anúncio reprovado, problema de conta, pagamento ou rastreamento | `gestao/trafego/alteracoes.md` + relatórios | Nada fora do normal → não envia mensagem; acesso falhou → avisa uma vez |
| 16 | Sexta | `clientes/<slug>/trafego/relatorios/` | Dados incompletos → decisão INVESTIGAR, sem propor mudança de verba |
| 17 | Dia 25, só para clientes que anunciam | `clientes/<slug>/trafego/AAAA-MM-plano.md` | Verba ou objetivo FALTA → pergunta ao Guilherme, não inventa |
| 18 | Quinta | `criativo/referencias.md` + referências das clientes | Nada fora do guia no feed → não manda mensagem; imagem que não abriu → avisa, não avalia |
| 19 | Dias úteis, para cada cliente com perfil no mLabs | `sincronizado_em` no painel | mLabs fora do ar → tenta na próxima; 2 dias seguidos sem sincronizar → avisa o Samuel |

## Texto das rotinas (para colar no OpenBot)

1. **Samuel · posts do dia:** "Consulte no painel todos os conteúdos com data de postagem HOJE, de
   todas as clientes, em qualquer etapa, **menos roteiros**. Se não houver nenhum, não envie mensagem.
   Se houver, envie ao Guilherme no formato de `modelos/posts-do-dia.md` (link de cada conteúdo no
   painel, status e alertas) e pergunte se pode seguir com a programação. Só depois do ok dele,
   agende no mLabs os posts liberados, no horário indicado, e confirme o que foi agendado."
2. **Samuel · resumo semanal:** "Faça o resumo semanal conforme `modelos/resumo-semanal.md`: consulte
   o painel (API dos bots) e o repositório, grave em `gestao/semanal/` e me envie."
3. **Samuel · novidades do painel:** "Consulte `GET /novidades?desde=<último ate de
   gestao/rotinas/registro.md>&autor=cliente`. Se `total` for 0 e não for a checagem das 17h30,
   encerre sem fazer nada. Para cada roteiro aprovado, avance o bloco para o formato planejado e acione
   quem vem depois (Design, dia de produção ou Manu). Para cada ajuste sugerido ou comentário, encaminhe
   a quem fez só com o número do bloco. Grave o novo `ate`. Às 17h30, verifique também autorizações
   pendentes, conteúdos atrasados em relação à meta e escalonamentos da Lari sem retorno e me envie um
   resumo agrupado só se houver algo."
4. **Samuel · pedido de produção:** "Para cada cliente, confira no painel se o mês atual bateu a meta;
   se não, avise o Guilherme primeiro. Depois mande à Estratégia o `modelos/pedido-de-producao.md`
   preenchido de cada cliente: roteiros de TODOS os conteúdos do mês seguinte, na quantidade da meta
   de posts no painel. Junte as perguntas para as clientes que a Estratégia trouxer no passo 1, envie
   ao Guilherme numa só mensagem e espere as respostas antes de liberar a produção. O Design não entra
   nessa etapa. Meta: lote revisado no painel e pronto para o ok do Guilherme até o dia 5."
5. **Estratégia · pautas:** "Gere a pauta do mês M+1 (dois meses à frente: hoje é dia 20 do mês M-1)
   para cada cliente ativa, conforme `equipe/estrategia.md`, e grave no repositório."
6. *(Removida em 2026-11-26.)*
7. **Design · artes e capas:** "Procure no painel (1) os carrosséis cujo roteiro a cliente já aprovou
   e que ainda não têm arte e (2) os reels que já têm vídeo e ainda não têm capa. Para cada um, crie
   a arte ou a capa no modelo da cliente, com o texto aprovado, mande ao Revisor só o número do bloco
   e suba no painel depois de aprovada. Nunca crie arte de roteiro não aprovado. Se não houver nada,
   não faça nada."
8. **Analista · relatórios:** "Gere o relatório do mês anterior de cada cliente ativa conforme
   `modelos/relatorio-mensal.md`, grave no repositório e avise a Estratégia e o Samuel com o caminho
   do arquivo e as 3 recomendações principais."
9. **Analista · recordes:** "Leia do painel (`GET /clientes/:slug/metricas?dias=90`) os posts dos
   últimos 7 dias de cada cliente. Se algum for recorde pelo critério de `equipe/analista.md`, envie
   para a Lari."
10. **Social Media · tendências e sugestões da semana:** "Para cada cliente ativa (exceto a Straut):
    grave a semana na aba Tendências como rascunho (1 tendência do mês, 3 a 5 referências de outros
    perfis com link real, 3 ideias de stories), usando primeiro os melhores posts das contas de
    referência no mLabs; depois crie a ideia de stories da semana e escolha um reels viral, conforme
    `equipe/social-media.md`. Aplique os filtros, grave em `sugestoes/` como pronto e avise a Lari só
    com o caminho do arquivo."
11. **Lari · boa semana:** "Zere os contadores semanais em `atendimento.md` de cada cliente. Depois,
    para cada cliente (exceto a Straut) que NÃO tenha mensagem sem resposta nem conversa ativa, envie
    uma mensagem de bom dia e boa semana de trabalho, diferente das últimas 4 semanas (veja
    `atendimento.md`), e registre o texto enviado."
12. **Lari · stories:** "Envie as ideias de stories da semana marcadas como prontas pela Social Media,
    respeitando todas as regras de envio."
13. **Lari · reels viral:** "Envie os reels virais da semana marcados como prontos, respeitando todas
    as regras de envio. O que não puder sair agora fica na fila."
14. **Lari · avisos:** "Verifique em `GET /pendencias` os conteúdos aguardando aprovação há mais de 48
    horas, os lembretes de gravação de amanhã (dias de produção no painel) e a fila (avisos e sugestões
    pendentes). Envie o que for permitido pelas regras de envio e deixe o resto na fila. Nada a enviar
    → não faça mais nada."
15. **Tráfego · checagem de fatos:** "Para cada conta ativa, confira só fatos: gasto em relação ao ritmo
    previsto, anúncios reprovados, problemas de conta ou pagamento e rastreamento parado. Se algo
    estiver fora do normal, avise o Samuel (urgente: o Guilherme). Se não houver nada, não envie
    mensagem. Não faça alterações."
16. **Tráfego · checagem semanal:** "Faça a checagem semanal de `referencias/trafego-pago.md` em cada
    conta, termine com uma decisão por conta, grave o relatório (`modelos/relatorio-de-trafego.md`) e
    envie o resumo e as propostas que precisam de ok ao Samuel."
17. **Tráfego · plano de mídia:** "Para cada cliente que anuncia, prepare o plano de mídia do mês
    seguinte (`modelos/plano-de-midia.md`) e envie ao Samuel para o ok do Guilherme."
18. **Manu · referências visuais e olhar de feed:** "Salve de 3 a 5 referências VISUAIS da semana
    (link, o que observar, por que funciona, para qual cliente serve) em `criativo/referencias.md` ou
    na pasta da cliente, só links, nunca imagens. Referência de tema e gancho é da Social Media: não
    repita. Depois veja no painel os posts publicados e os próximos de cada cliente e compare com o
    guia visual. Se houver quebra de consistência, texto ilegível ou cara de IA, mande uma observação
    objetiva ao Design. Se não houver nada, não envie mensagem."
19. **Analista · sincronizar métricas:** "Para cada cliente ativa com perfil no mLabs, busque os posts
    e reels publicados dos últimos 45 dias e o crescimento de seguidores e grave tudo num único
    `PUT /clientes/<slug>/metricas`. Depois leia `GET /clientes/<slug>/metricas` e, para os posts do
    top 3 sem motivo, escreva o motivo (1 a 2 frases) e mande só esses posts de novo com `motivo`.
    Não envie mensagem, a não ser que uma cliente fique 2 dias úteis sem sincronizar."
