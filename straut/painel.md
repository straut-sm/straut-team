# Painel da Straut: como funciona

https://painel.strautmarketing.com. Código em `straut-sm/straut-brain`. Mantido pelo Straut Brain · App.

## Páginas
| Rota | Quem acessa | O que é |
|---|---|---|
| `/` | Straut | Painel de controle: todas as clientes, calendário geral, "Precisa da sua atenção" |
| `/c/<slug>` | Straut | Página da cliente em modo de edição |
| `/p/<slug>` | Cliente | Página da cliente (link + senha, sem conta). **Este é o link que a Lari envia.** |

## Blocos (cada conteúdo do calendário)
Um bloco acompanha o conteúdo do início ao fim:
roteiro → aprovado → gravado → vira reels/carrossel/foto → recebe mídias → aprovado → publicado.

### Formatos
`roteiro` · `reels` · `carrossel` · `foto`. Um roteiro também tem o **formato planejado** (o que ele vai virar).

### Status
| Status | Significado | Quem muda |
|---|---|---|
| `em_producao` | A Straut está trabalhando | Straut / bots |
| `aguardando_aprovacao` | Esperando a cliente aprovar | Straut / bots (**com autorização na fase de testes**) |
| `ajuste_sugerido` | A cliente sugeriu uma alteração | Cliente |
| `aprovado` | A cliente aprovou | Cliente |
| `publicado` | Foi postado | Guilherme (manual) |

### O que a cliente pode fazer
Aprovar, sugerir alteração (aparece como "controle de alterações" e a Straut aceita ou recusa) e comentar.

### Contagem da meta
A barra de progresso compara os posts do mês com a meta do contrato. **Roteiros não contam como post.**

## Acesso dos bots
Os bots não acessam o painel. Eles trabalham pelo calendário em `clientes/<slug>/calendario/` no straut-team.
Como esse calendário chega ao painel ainda será decidido pelo Guilherme. Os bots não usam o login da Straut.
