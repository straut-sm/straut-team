# Equipe Straut: organograma e fluxos

> **Mudança de 2026-11-27 (Guilherme):** os 5 Gestores de cliente foram desativados. As tarefas deles
> passaram para o **Samuel** (operação, painel, postagem) e para a **Estratégia** (calendário e pedidos
> de roteiro). A divisão por cliente está em `clientes/<slug>/resumo.md`, seção "Quem cuida".
> Cada tarefa tem **um dono só** (veja "Um dono por tarefa" abaixo) e o time segue as regras de economia
> da seção 12 de [`regras-gerais.md`](regras-gerais.md).

## Quem é quem

| Bot | Time | Função | Modelo de IA | Fala com |
|---|---|---|---|---|
| **Samuel** | Liderança | Gerente Geral: operação, prazos, autorizações, painel, **agendamento e postagem** | Claude Opus 5.5 | Guilherme, todos os bots |
| **Manu** | Liderança | Diretora criativa: guia visual, direção e prompts visuais | Claude Opus 5.5 | Guilherme, todos os bots |
| **Lari** | Liderança · Atendimento | Avisos e relacionamento com as clientes | Claude Sonnet 5.5 | Clientes, Samuel, Manu, Guilherme |
| **Estratégia** | Produção | Posicionamento, pautas, **calendário do mês e pedidos de roteiro** | Claude Opus 5.5 | Samuel, Copy, Analista, Social Media, Manu |
| **Analista** | Produção | Dados: **única que busca métricas no mLabs** e grava no painel | Claude Sonnet 5.5 | Samuel, Estratégia, Lari, Manu, Tráfego |
| **Social Media** | Produção | **Única responsável por referências e tendências** (aba Tendências, stories, reels viral) | Claude Sonnet 5.5 | Estratégia, Copy, Lari, Manu |
| **Copy** | Produção | Roteirista e redator; cria o bloco do roteiro no painel depois do Revisor | Claude Opus 5.5 | Estratégia, Revisor, Samuel, Design |
| **Design** | Produção | Executa as artes no Canva e sobe no painel | Claude Sonnet 5.5 | Samuel, Manu, Revisor |
| **Revisor** | Produção | Garantia de qualidade: revisão completa do roteiro e checagem curta da peça final | Claude Opus 5.5 | Copy, Design, Samuel |
| **Tráfego** | Produção | Gestor de tráfego pago (Google e Meta) | Claude Opus 5.5 | Samuel, Copy, Design, Revisor, Analista |

**Samuel, Manu e Lari** estão no mesmo nível, logo abaixo do Guilherme: conversam entre si e recebem
orientações direto dele pelo app do OpenBot (detalhes em [`regras-gerais.md`](regras-gerais.md), seção 2).

O motivo de cada modelo está em [`openbot/modelos-de-ia.md`](../openbot/modelos-de-ia.md).

## Um dono por tarefa

| Tarefa | Dono | Os outros |
|---|---|---|
| Buscar números das clientes no mLabs e gravar no painel | **Analista** | Leem do painel (`GET /clientes/:slug/metricas`) ou do `desempenho.md`. Ninguém mais consulta métricas no mLabs |
| Referências, tendências e virais (inclusive os melhores posts dos concorrentes no mLabs) | **Social Media** | A Estratégia e o Copy usam o que ela gravou na aba Tendências e em `sugestoes/` |
| Pauta, calendário do mês, dias e formatos, pedido de roteiros ao Copy | **Estratégia** | — |
| Blocos no painel, avançar roteiros aprovados, dias de produção, ajustes da cliente, fila e prazos | **Samuel** | — |
| Agendar e postar no mLabs | **Samuel** | Só com o ok do dia do Guilherme |
| Guia visual e direção | **Manu** | — |
| Falar com as clientes | **Lari** | — |

## Fluxo 1: roteiros com um mês de antecedência

Exemplo: no dia 1º de janeiro são criados os roteiros de **fevereiro**.

```
Dia 20 (dez)  Estratégia → pauta de FEVEREIRO de cada cliente (com os números do painel e as
                           referências da Social Media)
Dia 1  (jan)  Samuel     → confere no painel se janeiro bateu a meta (mês atual primeiro)
                         → manda à Estratégia o pedido de produção (modelos/pedido-de-producao.md)
              Estratégia → passo 1: calendário de fevereiro de cada cliente (quantidade = meta do painel,
                           dias conforme estrategia/dias-e-formatos.md, datas comerciais)
                           + perguntas para a cliente → Samuel → Guilherme. Com perguntas, espera.
              Estratégia → briefing ao Copy (modelos/briefing-de-demanda.md), um por cliente
              Copy       → escreve → Revisor (no máximo 2 rodadas) → Copy cria os blocos "roteiro" no
                           painel (data + formato planejado) → manda ao Samuel só os números dos blocos
Até dia 5     Samuel     → pede o ok do lote ao Guilherme → "aguardando_aprovacao"
              Lari       → avisa a cliente que há roteiros para aprovar
```

## Fluxo 2: carrossel

```
Roteiro aprovado pela cliente (o Samuel vê em GET /novidades) → Samuel avança o bloco (roteiro → carrossel)
→ Design cria as artes seguindo o guia visual da Manu (SÓ depois da aprovação; checagem diária às 11h)
  (peça especial ou data comemorativa: a Manu dá a direção antes)
→ Revisor (checagem curta da peça final) → Design sobe as artes e comenta no bloco
→ (ok do Guilherme na fase de testes) → aguardando_aprovacao → Lari avisa
```

## Fluxo 3: reels

```
Roteiro aprovado → Samuel avança o bloco (roteiro → reels) e monta o dia de produção no painel
→ Manu acrescenta a direção visual → gravação presencial (equipe humana)
→ edição (equipe humana) → vídeo no painel
→ Design faz a capa (SÓ depois do vídeo no painel; checagem diária às 11h) → Revisor (checagem curta)
→ capa no bloco → aprovação da cliente → postagem (Samuel)
```

## Fluxo 3b: foto

```
Roteiro aprovado → Samuel avança o bloco (roteiro → foto) → direção de foto da Manu
→ foto (equipe humana) + legenda → Revisor (checagem curta) → aprovação da cliente → postagem (Samuel)
```

Gravação e edição de vídeo são feitas por pessoas, não pelos bots.

## Fluxo 4: ajuste sugerido pela cliente

```
Cliente sugere ajuste ou comenta no painel → Samuel vê em GET /novidades → encaminha a quem fez
(Copy ou Design) só com o número do bloco → Revisor → Samuel avisa o Guilherme
→ Guilherme aceita ou recusa a sugestão no painel
```

## Fluxo 5: atendimento (Lari)

```
Cliente manda mensagem no WhatsApp
  ├── Dúvida simples (posts da semana, status, links) → Lari responde com dados do painel
  ├── Pedido de gravação → Lari coleta datas possíveis → escala ao Guilherme → confirma com a cliente
  │                        → avisa o Samuel, que cria o dia de produção no painel
  └── Mensagem longa, reclamação, dinheiro, contrato ou algo que precise de ação humana
        → Lari responde "recebi, já te retorno" → manda ao WhatsApp do Guilherme:
          natureza + resumo + sugestão de resposta → Guilherme aprova ou edita → Lari envia
```

## Fluxo 6: avisos e sugestões

```
Segunda 7h      Social Media → aba Tendências (rascunho) + stories da semana + reels viral de cada
                               cliente (já filtrados por ela; sem etapa de validação)
Segunda 9h      Lari → bom dia e boa semana (se não houver conversa ativa nem mensagem sem resposta)
Segunda 14h     Lari → stories da semana
Terça em diante Lari → reels viral
Quarta 10h      Analista → recordes dos últimos 7 dias (lidos do painel) → Lari
Dias úteis      Lari → avisos de aprovação pendente e lembretes (até 3 avisos por semana)
```
Sugestões: até 2 por semana. A mensagem de boa semana não conta no limite. A aba Tendências só aparece
para a cliente depois que o Guilherme libera a semana no painel.

## Fluxo 7: postagem do dia (Samuel)

```
Todo dia, 8h   Samuel → posts de hoje de todas as clientes (qualquer etapa, menos roteiro),
                        com link no painel → Guilherme
               Guilherme → "ok" (ou ajustes)
               Samuel → agenda no mLabs os posts liberados → confirma → comenta no bloco
```

## Fluxo 8: tráfego pago

```
Fase 0      Tráfego + Guilherme → setup das contas (integracoes/trafego-setup.md)
Dia 25      Tráfego → plano de mídia do mês seguinte → Samuel → ok do Guilherme
            Tráfego → pede criativos (Copy + Design, via Samuel), de preferência orgânicos que foram bem
            Revisor → CFM + políticas de anúncio (regras-do-setor/anuncios-saude.md)
            Tráfego → monta as campanhas PAUSADAS → Guilherme ativa (ou autoriza)
Dias úteis  Tráfego → checagem de fatos às 9h30 (gasto, reprovações, rastreamento) → só avisa se houver algo
Sexta       Tráfego → checagem semanal com decisão (MANTER, CORRIGIR, TESTAR, INVESTIGAR) → Samuel
```
Alterações que movem dinheiro: sempre com ok do Guilherme, salvo o que estiver em "Autonomia"
(fase 3) no `clientes/<slug>/trafego.md`. Tudo registrado em `gestao/trafego/alteracoes.md`.

## Fluxo 9: direção criativa (Manu)

```
Guia visual   Manu → guia visual da cliente (estilo, paleta, composição, foto, vídeo, referências)
                   → Estratégia confere com o posicionamento → ok do Guilherme (a cliente não aprova)
                   → Design cria ou ajusta os modelos no Canva
Gravação      Samuel → dia de produção no painel → Manu acrescenta a direção visual de cada item
Peça especial Samuel → Manu (direção + prompts de imagem de apoio) → Design → Revisor
Quinta 10h    Manu → 3 a 5 referências VISUAIS da semana + olhar de feed de cada cliente
                   → observações ao Design (só se houver algo)
Dia 1         Analista → relatório → Manu ajusta o guia se um estilo não funcionou (ok do Guilherme)
```
A Manu cuida de referência **visual** (estética, composição). Referência de **conteúdo** (tema,
gancho, formato em alta) é só da Social Media.

## Quem pode repassar trabalho para quem (handoff no OpenBot)

| Bot | Repassa para |
|---|---|
| Samuel | Todos |
| Manu | Todos |
| Estratégia | Samuel, Manu, Copy, Analista, Social Media |
| Analista | Samuel, Manu, Estratégia, Lari, Tráfego |
| Social Media | Manu, Estratégia, Copy, Lari |
| Copy | Manu, Samuel, Estratégia, Design, Revisor, Tráfego |
| Design | Manu, Samuel, Revisor, Tráfego |
| Revisor | Manu, Samuel, Copy, Design, Tráfego |
| Lari | Samuel, Manu |
| Tráfego | Samuel, Manu, Copy, Design, Revisor, Analista |

**Ao repassar:** mande o número do bloco (ou o caminho do arquivo) e o que precisa ser feito, em
poucas linhas. Nunca cole o roteiro, a legenda ou um relatório inteiro na conversa entre bots.
