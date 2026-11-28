# Modelos de IA de cada bot

## ⚠️ Primeiro: o plano Claude Pro não cobre os bots
O **Claude Pro** vale para usar o Claude no site e nos apps (claude.ai). O OpenBot usa o Claude pela
**API**, que é cobrada à parte, por uso, no **Claude Console** (platform.claude.com):

1. Crie uma conta em platform.claude.com (pode ser com o mesmo e-mail).
2. Em **Billing**, adicione créditos (ex.: US$ 50 para começar).
3. Em **Limits**, defina um **limite de gasto mensal** (sugestão inicial: US$ 100).
4. Em **API Keys**, crie uma chave chamada `openbot-straut`.
5. Cole a chave **só** no OpenBot (credenciais / `ANTHROPIC_API_KEY`). Nunca no GitHub nem no chat.

O Pro continua útil para você e para o Straut Brain no claude.ai.

## Família Claude (preços da API, novembro de 2026)
| Modelo | Para quê | Entrada (por 1 milhão de tokens) | Saída (por 1 milhão de tokens) |
|---|---|---|---|
| **Claude Opus 5.5** (`claude-opus-5-5`) | Raciocínio, escrita e julgamento de alto nível | US$ 4 | US$ 20 |
| **Claude Sonnet 5.5** (`claude-sonnet-5-5`) | Equilíbrio entre qualidade, velocidade e custo; ótimo com ferramentas | US$ 2 | US$ 10 |
| **Claude Haiku 5.5** (`claude-haiku-5-5`) | Tarefas simples e em grande volume, muito barato | US$ 0,10 | US$ 0,50 |
| Claude Fable 5.2 (`claude-fable-5-2`) | O mais capaz, para tarefas muito difíceis e longas | US$ 8 | US$ 40 |

*1 milhão de tokens ≈ 750 mil palavras. Confira os preços atuais no Console.*

## Modelo de cada bot
| Bot | Modelo | Por quê |
|---|---|---|
| **Samuel** | **Opus 5.5** | É quem decide prioridades, interpreta os seus pedidos e coordena o time. Erros dele se espalham. Volume baixo. |
| **Estratégia** | **Opus 5.5** | Pensamento estratégico profundo, pouco volume (pautas mensais e diagnósticos). |
| **Analista** | **Sonnet 5.5** | Leitura de métricas e relatórios estruturados. Não precisa do Opus. |
| **Social Media** | **Sonnet 5.5** | Muita navegação e pesquisa. O Sonnet é rápido e bom com ferramentas. |
| **Copy** | **Opus 5.5** | O texto é o coração do produto: tom de voz, nuance e criatividade. Vale o investimento. |
| **Design** | **Sonnet 5.5** | O trabalho é operar o Canva e o painel (ferramentas). O estilo vem dos modelos prontos. |
| **Revisor** | **Opus 5.5** | Última barreira antes da cliente. Precisa pegar erros sutis e riscos éticos (CFM). |
| **Lari** | **Sonnet 5.5** | Conversa natural e empática, classifica bem o que escalar e responde rápido. |
| **Manu** | **Opus 5.5** | Diretora criativa: gosto visual, análise de imagens e prompts precisos. Erros de estilo se repetem em todo o feed. Volume baixo. |
| **Tráfego** | **Opus 5.5** | Mexe em dinheiro: precisa do melhor julgamento com números, amostras pequenas e regras de anúncio. Volume baixo. |

**Por que não o Haiku?** Ele seria suficiente para avisos simples, mas a Lari também conversa e decide o
que escalar, e uma resposta ruim para uma cliente custa mais que a economia. Ele pode entrar depois, se
o OpenBot permitir subtarefas com outro modelo.

**Por que não o Fable 5.2?** É o dobro do preço do Opus 5.5 e nenhuma tarefa do time precisa desse nível.

**Se o OpenBot só permitir um modelo para todos:** use o **Sonnet 5.5**.

## Configuração recomendada
- **Esforço (effort):** `medium` para Lari, Analista, Social Media e Design; `high` para
  Samuel, Manu, Estratégia, Copy e Revisor (se o OpenBot tiver essa opção).
- **Cache de prompt:** se o OpenBot permitir, deixe ligado. As regras e fichas se repetem em toda
  tarefa, e o cache reduz bastante o custo.

## Economia (2026-11-27)
- Com o fim dos 5 Gestores, o time caiu de 15 para 10 bots.
- Se o OpenBot permitir escolher o modelo **por rotina**, rode no **Sonnet 5.5** as rotinas mecânicas
  dos bots Opus (Samuel: 3 novidades). Se permitir **Haiku 5.5** por rotina, ele serve para a 19 da
  Analista (sincronizar métricas). Conversas e
  decisões continuam no modelo do bot.
- As regras de economia de tokens do time estão em `equipe/regras-gerais.md`, seção 12.

## Estimativa de custo (grosseira)
Com 5 clientes, cerca de 70 conteúdos por mês, mais atendimento e rotinas: **de US$ 150 a US$ 350 por
mês**. O valor depende muito de quantas idas e vindas cada tarefa tem. Comece com o limite de
**US$ 100** no Console, acompanhe o gasto por 2 semanas e ajuste. O Samuel informa o gasto quando o
Guilherme pedir o resumo semanal, se tiver acesso a essa informação.
