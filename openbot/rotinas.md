# Rotinas (agendamentos no OpenBot)

O OpenBot permite **até 20 rotinas ativas**, com intervalo mínimo de 15 minutos. O time usa 11.
Horário de Brasília.

| # | Bot | Quando | Tarefa |
|---|---|---|---|
| 1 | Samuel | Segunda, 8h30 | Resumo semanal → `gestao/semanal/` → enviar ao Guilherme |
| 2 | Samuel | Segunda a sexta, 17h30 | Checagem do dia: autorizações pendentes, atrasos, escalonamentos sem retorno |
| 3 | Samuel | Dia 20, 9h | Acionar os Gestores para montar o calendário do mês seguinte |
| 4 | Estratégia | Dia 15, 9h | Pauta do mês seguinte para cada cliente |
| 5 | Analista | Dia 1, 9h | Relatório mensal de cada cliente |
| 6 | Analista | Segunda a sexta, 10h | Checagem de recordes → Lari |
| 7 | Social Media | Terça, 9h | Reels viral da semana para cada cliente → Gestor |
| 8 | Social Media | Sexta, 9h | Ideia de stories da semana seguinte → Gestor |
| 9 | Lari | Segunda, 10h | Zerar os contadores da semana + enviar as ideias de stories aprovadas |
| 10 | Lari | Quarta, 10h | Enviar os reels virais aprovados |
| 11 | Lari | Segunda a sexta, 10h30 e 15h30 | Avisos de aprovação pendente, lembretes e fila de avisos |

As mensagens que chegam das clientes no WhatsApp acionam a Lari na hora (não precisam de rotina).

## Texto das rotinas (para colar no OpenBot)

1. **Samuel · resumo semanal:** "Faça o resumo semanal conforme `modelos/resumo-semanal.md`: consulte o
   painel (API dos bots) e o repositório, grave em `gestao/semanal/` e me envie."
2. **Samuel · checagem do dia:** "Verifique autorizações pendentes, conteúdos atrasados em relação à
   meta, ajustes sugeridos sem resposta e escalonamentos da Lari sem retorno. Se houver algo, me envie
   um resumo agrupado. Se não houver nada, não envie mensagem."
3. **Samuel · calendários:** "Acione cada Gestor de cliente para montar o calendário do mês seguinte
   com base na pauta da Estratégia e no último relatório do Analista."
4. **Estratégia · pautas:** "Gere a pauta do mês seguinte para cada cliente ativa, conforme
   `equipe/estrategia.md`, grave no repositório e avise cada Gestor."
5. **Analista · relatórios:** "Gere o relatório do mês anterior de cada cliente ativa conforme
   `modelos/relatorio-mensal.md`, grave no repositório e avise o Gestor e a Estratégia."
6. **Analista · recordes:** "Verifique os posts das últimas 48 horas de cada cliente. Se algum for recorde
   pelo critério de `equipe/analista.md`, envie para a Lari com cópia ao Gestor."
7. **Social Media · viral:** "Encontre um reels viral para cada cliente ativa (exceto a Straut), conforme
   `equipe/social-media.md`, grave em `sugestoes/` e envie ao Gestor para validar."
8. **Social Media · stories:** "Crie uma ideia de stories da semana seguinte para cada cliente ativa
   (exceto a Straut), grave em `sugestoes/` e envie ao Gestor para validar."
9. **Lari · segunda:** "Zere os contadores semanais em `atendimento.md` de cada cliente. Depois envie as
   ideias de stories aprovadas pelos Gestores, respeitando todas as regras de envio."
10. **Lari · quarta:** "Envie os reels virais aprovados pelos Gestores, respeitando todas as regras de envio."
11. **Lari · avisos:** "Verifique no painel os conteúdos aguardando aprovação há mais de 48 horas, os
    lembretes de gravação de amanhã e a fila de avisos. Envie o que for permitido pelas regras de envio
    e deixe o resto na fila."
