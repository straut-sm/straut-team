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
Pela **API dos bots** ([`integracoes/api-dos-bots.md`](../integracoes/api-dos-bots.md)). Os bots não usam o login da Straut.

- No histórico do bloco, a Straut vê qual bot fez cada ação ("Straut · bot design"); a cliente vê só "Straut".
- Comentários dos bots são **internos**: aparecem para a Straut com o selo "interno, a cliente não vê".
- Vídeos podem vir de um link do Google Drive (o arquivo precisa estar em "Qualquer pessoa com o link pode ver").
- Fotos do carrossel podem ser reordenadas arrastando as miniaturas (no painel) ou pela API.
- **Lixeira:** apagar (pelo painel ou pela API) manda blocos, mídias e arquivos para a Lixeira (botão no topo
  do painel). Ficam 30 dias, podem ser restaurados e depois somem de vez.
