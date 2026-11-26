# Rotinas (agendamentos no OpenBot)

O OpenBot permite **até 20 rotinas ativas**, com intervalo mínimo de 15 minutos. O time usa 16
(as 3 do Tráfego só são ativadas a partir da fase 1). A rotina 6 foi removida em 2026-11-26: as artes
de carrossel só saem depois da aprovação do roteiro e entraram na rotina 7.
Horário de Brasília.

## Calendário de produção (um mês de antecedência)

```
Dia 20 do mês M-1   Estratégia  → pauta do mês M+1          (ex.: 20/dez → pauta de fevereiro)
Dia 1  do mês M     Samuel      → confere se o mês M bateu a meta → pedido de produção a cada Gestor
                    Gestores    → passo 1: plano + perguntas para a cliente (com perguntas, espera)
                                → calendário + ROTEIROS de todos os conteúdos do mês M+1
                                   (vídeos, carrosséis e fotos; quantidade = meta de posts no painel)
                                   → Revisor → painel → ok do Guilherme → aprovação da cliente (até o dia 5)
Todo dia útil       Design      → ARTES dos carrosséis com roteiro aprovado e CAPAS dos reels que já
                                   têm vídeo no painel
Todo dia            Samuel      → posts do dia → ok do Guilherme → agenda no mLabs
```

Exemplo: no dia 1º de janeiro saem os roteiros de fevereiro. As artes dos carrosséis saem quando a cliente aprova cada roteiro.

## Lista de rotinas

| # | Bot | Quando | Tarefa |
|---|---|---|---|
| 1 | Samuel | **Todos os dias, 8h** | Posts do dia: enviar ao Guilherme (com links do painel) → com o ok, agendar no mLabs |
| 2 | Samuel | Segunda, 8h30 | Resumo semanal → `gestao/semanal/` → enviar ao Guilherme |
| 3 | Samuel | Segunda a sexta, 17h30 | Checagem do dia: autorizações pendentes, atrasos, escalonamentos sem retorno |
| 4 | Samuel | **Dia 1, 9h** | Acionar os Gestores: calendário + roteiros de todos os conteúdos do mês seguinte |
| 5 | Estratégia | **Dia 20, 9h** | Pauta do mês M+1 (dois meses à frente) para cada cliente |
| 6 | — | — | Removida em 2026-11-26 (artes de carrossel entraram na rotina 7) |
| 7 | Design | **Segunda a sexta, 11h** | Artes dos carrosséis com roteiro aprovado e capas dos reels que já têm vídeo no painel |
| 8 | Analista | Dia 1, 9h | Relatório mensal de cada cliente |
| 9 | Analista | **Quarta, 10h** | Recordes de desempenho (posts dos últimos 7 dias) → Lari |
| 10 | Social Media | **Segunda, 7h** | Ideia de stories da semana + reels viral de cada cliente → Gestor valida |
| 11 | Lari | **Segunda, 9h** | Zerar os contadores + mensagem de bom dia e boa semana |
| 12 | Lari | **Segunda, 14h** | Enviar as ideias de stories aprovadas |
| 13 | Lari | **Terça, 10h** | Enviar os reels virais aprovados (o que não sair fica na fila da rotina 14) |
| 14 | Lari | Segunda a sexta, 10h30 e 15h30 | Avisos de aprovação pendente, lembretes de gravação e fila (inclusive sugestões pendentes) |
| 15 | Tráfego | Segunda a sexta, 9h30 | Checagem de fatos: gasto × ritmo, anúncios reprovados, conta e pagamento, rastreamento |
| 16 | Tráfego | Sexta, 10h | Checagem semanal com decisão por conta → relatório → Samuel |
| 17 | Tráfego | Dia 25, 9h | Plano de mídia do mês seguinte de cada cliente que anuncia |

As mensagens que chegam das clientes no WhatsApp acionam a Lari na hora (não precisam de rotina).

## Segurança das rotinas
Cada rotina segue [`referencias/rotinas-seguras.md`](../referencias/rotinas-seguras.md). Todas
obedecem à **"PAUSA GERAL"** e registram o que fizeram em `gestao/rotinas/registro.md` (só quando agem).

| # | Só age quando | Memória (para não repetir) | Para / chama humano quando |
|---|---|---|---|
| 1 | Há posts com data de hoje (não roteiro) | Comentário "Agendado no mLabs" no bloco | Sem ok do Guilherme → não agenda; mLabs com erro → avisa |
| 2 | Sempre (segunda) | `gestao/semanal/` | Dados do painel indisponíveis → avisa e envia o que tiver |
| 3 | Há pendência, atraso ou escalonamento sem retorno | `gestao/rotinas/registro.md` | Nada pendente → não envia mensagem |
| 4 | Dia 1 | `calendario/AAAA-MM.md` de cada cliente | Pauta do mês ausente → avisa a Estratégia e o Guilherme; mês atual abaixo da meta → avisa o Guilherme primeiro; perguntas para a cliente → leva ao Guilherme e espera |
| 5 | Dia 20 | `estrategia/pauta-AAAA-MM.md` | Cliente sem posicionamento definido → avisa o Gestor |
| 6 | — | — | Removida |
| 7 | Há carrossel com roteiro aprovado e sem arte, ou reels com vídeo e sem capa | Comentário com o link do Canva e mídias no bloco | Cliente sem modelo no Canva → avisa o Gestor, não inventa estilo; nada pendente → não faz nada |
| 8 | Dia 1 | `relatorios/AAAA-MM.md` | mLabs sem dados → avisa, não inventa números |
| 9 | Há post que atende ao critério de recorde | Tabela de recordes em `desempenho.md` | Post já avisado → pula; número muito fora do normal → confirma antes |
| 10 | Segunda | `sugestoes/AAAA-MM-DD.md` com status | Nada adequado ao posicionamento → não sugere (melhor nada que algo ruim) |
| 11 | Cliente sem conversa ativa e sem mensagem sem resposta | "Mensagens de boa semana" em `atendimento.md` | Conversa ativa → não envia |
| 12–13 | Sugestão aprovada pelo Gestor e limite livre | Contador + status em `sugestoes/` | Limite atingido ou conversa ativa → fila |
| 14 | Pendência há mais de 48 horas, lembrete ou fila, com limite livre | Contador em `atendimento.md` | Mesmo aviso nas últimas 48 horas → não repete |
| 15 | Gasto 30% ou mais fora do ritmo, anúncio reprovado, problema de conta, pagamento ou rastreamento | `gestao/trafego/alteracoes.md` + relatórios | Nada fora do normal → não envia mensagem; acesso falhou → avisa uma vez |
| 16 | Sexta | `clientes/<slug>/trafego/relatorios/` | Dados incompletos → decisão INVESTIGAR, sem propor mudança de verba |
| 17 | Dia 25, só para clientes que anunciam | `clientes/<slug>/trafego/AAAA-MM-plano.md` | Verba ou objetivo FALTA → pergunta ao Guilherme, não inventa |

## Texto das rotinas (para colar no OpenBot)

1. **Samuel · posts do dia:** "Consulte no painel todos os conteúdos com data de postagem HOJE, de
   todas as clientes, em qualquer etapa, **menos roteiros**. Se não houver nenhum, não envie mensagem.
   Se houver, envie ao Guilherme no formato de `modelos/posts-do-dia.md` (link de cada conteúdo no
   painel, status e alertas) e pergunte se pode seguir com a programação. Só depois do ok dele,
   agende no mLabs os posts liberados, no horário indicado, e confirme o que foi agendado."
2. **Samuel · resumo semanal:** "Faça o resumo semanal conforme `modelos/resumo-semanal.md`: consulte
   o painel (API dos bots) e o repositório, grave em `gestao/semanal/` e me envie."
3. **Samuel · checagem do dia:** "Verifique autorizações pendentes, conteúdos atrasados em relação à
   meta, ajustes sugeridos sem resposta e escalonamentos da Lari sem retorno. Se houver algo, me envie
   um resumo agrupado. Se não houver nada, não envie mensagem."
4. **Samuel · roteiros do mês seguinte:** "Para cada cliente, confira no painel se o mês atual bateu a
   meta; se não, avise o Guilherme primeiro. Depois acione cada Gestor com
   `modelos/pedido-de-producao.md` preenchido: roteiros de TODOS os conteúdos do mês seguinte
   (vídeos, carrosséis e fotos), na quantidade da meta de posts de cada cliente no painel, com a
   pauta da Estratégia, dias da semana conforme `estrategia/dias-e-formatos.md` e datas comerciais do
   mês. Junte as perguntas para as clientes que os Gestores trouxerem no passo 1, envie ao Guilherme
   numa só mensagem e espere as respostas antes de liberar a produção. O Design não entra nessa etapa.
   Meta: roteiros revisados no painel e lote pronto para o ok do Guilherme até o dia 5."
5. **Estratégia · pautas:** "Gere a pauta do mês M+1 (dois meses à frente: hoje é dia 20 do mês M-1)
   para cada cliente ativa, conforme `equipe/estrategia.md`, grave no repositório e avise cada Gestor."
6. *(Removida em 2026-11-26.)*
7. **Design · artes e capas:** "Procure no painel (1) os carrosséis cujo roteiro a cliente já aprovou
   e que ainda não têm arte e (2) os reels que já têm vídeo e ainda não têm capa. Para cada um, crie
   a arte ou a capa no modelo da cliente, com o texto aprovado, mande ao Revisor e suba no painel
   depois de aprovada. Nunca crie arte de roteiro não aprovado. Se não houver nada, não faça nada."
8. **Analista · relatórios:** "Gere o relatório do mês anterior de cada cliente ativa conforme
   `modelos/relatorio-mensal.md`, grave no repositório e avise o Gestor e a Estratégia."
9. **Analista · recordes:** "Verifique os posts dos últimos 7 dias de cada cliente. Se algum for
   recorde pelo critério de `equipe/analista.md`, envie para a Lari com cópia ao Gestor."
10. **Social Media · sugestões da semana:** "Para cada cliente ativa (exceto a Straut), crie a ideia
    de stories da semana e escolha um reels viral, conforme `equipe/social-media.md`. Grave em
    `sugestoes/` e envie ao Gestor para validar ainda hoje de manhã."
11. **Lari · boa semana:** "Zere os contadores semanais em `atendimento.md` de cada cliente. Depois,
    para cada cliente (exceto a Straut) que NÃO tenha mensagem sem resposta nem conversa ativa, envie
    uma mensagem de bom dia e boa semana de trabalho, diferente das últimas 4 semanas (veja
    `atendimento.md`), e registre o texto enviado."
12. **Lari · stories:** "Envie as ideias de stories da semana aprovadas pelos Gestores, respeitando
    todas as regras de envio."
13. **Lari · reels viral:** "Envie os reels virais da semana aprovados pelos Gestores, respeitando
    todas as regras de envio. O que não puder sair agora fica na fila."
14. **Lari · avisos:** "Verifique no painel os conteúdos aguardando aprovação há mais de 48 horas, os
    lembretes de gravação de amanhã e a fila (avisos e sugestões pendentes). Envie o que for permitido
    pelas regras de envio e deixe o resto na fila."
15. **Tráfego · checagem de fatos:** "Para cada conta ativa, confira só fatos: gasto em relação ao ritmo
    previsto, anúncios reprovados, problemas de conta ou pagamento e rastreamento parado. Se algo
    estiver fora do normal, avise o Samuel (urgente: o Guilherme). Se não houver nada, não envie
    mensagem. Não faça alterações."
16. **Tráfego · checagem semanal:** "Faça a checagem semanal de `referencias/trafego-pago.md` em cada
    conta, termine com uma decisão por conta, grave o relatório (`modelos/relatorio-de-trafego.md`) e
    envie o resumo e as propostas que precisam de ok ao Samuel."
17. **Tráfego · plano de mídia:** "Para cada cliente que anuncia, prepare o plano de mídia do mês
    seguinte (`modelos/plano-de-midia.md`) e envie ao Gestor e ao Samuel para o ok do Guilherme."
