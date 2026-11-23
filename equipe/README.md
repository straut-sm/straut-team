# Equipe Straut: organograma e fluxos

## Quem é quem

| Bot | Time | Função | Modelo de IA | Fala com |
|---|---|---|---|---|
| **Samuel** | Gestão | Gerente Geral, principal contato do Guilherme | Claude Opus 5.5 | Guilherme, todos os bots |
| **Gestor · \<Cliente\>** | Gestão | Gestor de projeto de uma cliente | Claude Sonnet 5.5 | Samuel, produção, Lari |
| **Estratégia** | Produção | Planejamento: nicho, posicionamento, pautas | Claude Opus 5.5 | Gestores, Analista, Samuel |
| **Analista** | Produção | Dados e BI: desempenho e recordes | Claude Sonnet 5.5 | Gestores, Estratégia, Lari |
| **Social Media** | Produção | Caçador de tendências | Claude Sonnet 5.5 | Gestores, Copy, Lari |
| **Copy** | Produção | Roteirista e redator | Claude Opus 5.5 | Gestores, Design, Revisor |
| **Design** | Produção | Diretor de arte: Canva e painel | Claude Sonnet 5.5 | Gestores, Copy, Revisor |
| **Revisor** | Produção | Garantia de qualidade (diretor de criação) | Claude Opus 5.5 | Gestores, Copy, Design |
| **Lari** | Atendimento | Avisos e relacionamento com as clientes | Claude Sonnet 5.5 | Clientes, Gestores, Samuel, Guilherme |

O motivo de cada modelo está em [`openbot/modelos-de-ia.md`](../openbot/modelos-de-ia.md).

### Gestores de cliente ativos

| Bot | Cliente | Pasta |
|---|---|---|
| Gestor · Dr. José Erasmo | Neurocirurgião | [`clientes/jose-erasmo/`](../clientes/jose-erasmo/) |
| Gestor · Dra. Caroline Skaf | Dermatologia | [`clientes/caroline-skaf/`](../clientes/caroline-skaf/) |
| Gestor · Dra. Juliana Annunciato | Dermatologia | [`clientes/juliana-annunciato/`](../clientes/juliana-annunciato/) |
| Gestor · WA Concept | Extensão de cílios | [`clientes/wa-concept/`](../clientes/wa-concept/) |
| Gestor · Straut | Perfil da própria Straut | [`clientes/straut/`](../clientes/straut/) |

Todos usam a mesma ficha: [`gestor-de-cliente.md`](gestor-de-cliente.md). Só muda a pasta da cliente.

## Fluxo 1: roteiros com um mês de antecedência

Exemplo: no dia 1º de janeiro são criados os roteiros de **fevereiro**.

```
Dia 20 (dez)  Estratégia → pauta de FEVEREIRO para cada cliente (com base no relatório do Analista)
Dia 1  (jan)  Samuel     → aciona os Gestores
              Gestor     → calendário de fevereiro: quantidade = meta de posts da cliente no painel,
                           com datas e formatos (reels, carrossel, foto)
              Gestor     → pede ao Copy os ROTEIROS de todos os conteúdos (briefing: modelos/briefing-de-demanda.md)
              Copy       → escreve → Revisor (no máximo 2 rodadas, depois escala ao Gestor)
              Gestor     → cria os blocos "roteiro" no painel (com data e formato planejado)
Até dia 5     Samuel     → pede o ok do lote ao Guilherme → "aguardando_aprovacao"
              Lari       → avisa a cliente que há roteiros para aprovar
```

## Fluxo 2: carrossel

```
Dia 20 (jan)  Design → artes de TODOS os carrosséis de fevereiro no Canva, mesmo sem roteiro aprovado
              → Revisor
Roteiro aprovado → Gestor avança o bloco (roteiro → carrossel) → Design sobe as artes
                   (ajustando se o texto aprovado mudou) → Gestor confere
                   → (ok do Guilherme na fase de testes) → aguardando_aprovacao → Lari avisa
```

## Fluxo 3: reels

```
Roteiro aprovado → Gestor avança o bloco (roteiro → reels) → gravação presencial (equipe humana)
→ edição (equipe humana) → vídeo no painel
→ Design faz a capa (SÓ depois do vídeo no painel; checagem diária às 11h) → Revisor → capa no bloco
→ aprovação da cliente → postagem
```

## Fluxo 3b: foto

```
Roteiro aprovado → Gestor avança o bloco (roteiro → foto) → foto (equipe humana) + legenda
→ Revisor → aprovação da cliente → postagem
```

Gravação e edição de vídeo são feitas por pessoas, não pelos bots.

## Fluxo 4: ajuste sugerido pela cliente

```
Cliente sugere ajuste no painel → Gestor vê no painel → encaminha a quem fez (Copy ou Design)
→ Revisor → Gestor avisa o Samuel → Guilherme aceita ou recusa a sugestão no painel
```

## Fluxo 5: atendimento (Lari)

```
Cliente manda mensagem no WhatsApp
  ├── Dúvida simples (posts da semana, status, links) → Lari responde com dados do painel ou do Gestor
  ├── Pedido de gravação → Lari coleta datas possíveis → escala ao Guilherme → confirma com a cliente
  └── Mensagem longa, reclamação, dinheiro, contrato ou algo que precise de ação humana
        → Lari responde "recebi, já te retorno" → manda ao WhatsApp do Guilherme:
          natureza + resumo + sugestão de resposta → Guilherme aprova ou edita → Lari envia
```

## Fluxo 6: avisos e sugestões

```
Segunda 9h      Lari → bom dia e boa semana (se não houver conversa ativa nem mensagem sem resposta)
Segunda 7h      Social Media → stories da semana + reels viral → Gestor valida (segunda de manhã)
Segunda 14h     Lari → stories da semana
Terça em diante Lari → reels viral
Quarta 10h      Analista → recordes dos últimos 7 dias → Lari
Dias úteis      Lari → avisos de aprovação pendente e lembretes (até 3 avisos por semana)
```
Sugestões: até 2 por semana. A mensagem de boa semana não conta no limite.

## Fluxo 7: postagem do dia

```
Todo dia, 8h   Samuel → posts de hoje de todas as clientes (qualquer etapa, menos roteiro),
                        com link no painel → Guilherme
               Guilherme → "ok" (ou ajustes)
               Samuel → agenda no mLabs os posts liberados → confirma → comenta no bloco
```

## Quem pode repassar trabalho para quem (handoff no OpenBot)

| Bot | Repassa para |
|---|---|
| Samuel | Todos |
| Gestores | Samuel, Estratégia, Analista, Social Media, Copy, Design, Revisor, Lari |
| Estratégia | Samuel, Gestores, Analista |
| Analista | Samuel, Gestores, Estratégia, Lari |
| Social Media | Gestores, Copy, Lari |
| Copy | Gestores, Design, Revisor |
| Design | Gestores, Revisor |
| Revisor | Gestores, Copy, Design |
| Lari | Samuel, Gestores |
