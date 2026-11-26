# Passagem para o Straut Brain

> Para as conversas **Straut Brain · App** e **Straut Brain · Clientes**.
> Escrito em 2026-11-26 pela conversa "Chatbots Straut", a pedido do Guilherme. Resume o que foi
> decidido sobre o time de bots e o papel do painel nesse sistema.

## 1. O que existe agora

O repositório **`straut-sm/straut-team`** (privado) é a memória compartilhada entre os bots do
**OpenBot** e as conversas do Claude. Os bots leem e gravam tudo aqui. Comece por:

| Leia | Para saber |
|---|---|
| [`CLAUDE.md`](../CLAUDE.md) | Como o Claude usa este repositório |
| [`equipe/regras-gerais.md`](../equipe/regras-gerais.md) | Sincronização, segurança, autorizações, PAUSA GERAL |
| [`equipe/README.md`](../equipe/README.md) | Organograma e os 8 fluxos de trabalho |
| [`gestao/decisoes.md`](../gestao/decisoes.md) | Todas as decisões do Guilherme, com data |
| [`openbot/rotinas.md`](../openbot/rotinas.md) | As 17 rotinas automáticas |
| [`integracoes/api-dos-bots.md`](api-dos-bots.md) | **O pedido da API para o painel** |

## 2. Resumo do que foi decidido

- **Time de 14 bots:** Samuel (gerente geral, fala com o Guilherme pelo app do OpenBot), um Gestor por
  cliente, Estratégia, Analista, Social Media, Copy, Design, Revisor, Lari (atendimento no WhatsApp da
  Straut) e Tráfego (Google Ads e Meta, começando pelo setup das contas).
- **Modelos:** Opus 5.5 para Samuel, Estratégia, Copy, Revisor e Tráfego; Sonnet 5.5 para os demais.
  A API do Claude é cobrada à parte do plano Pro.
- **Calendário com um mês de antecedência:** no dia 1, roteiros de todos os conteúdos do mês seguinte,
  na quantidade de `contract_posts` da cliente no painel. Lote completo até o dia 5.
- **Dia 20:** o Design cria as artes dos carrosséis do mês seguinte, mesmo sem roteiro aprovado.
  **Capa de reels só depois que o vídeo estiver no painel.**
- **Samuel, todo dia às 8h:** manda ao Guilherme os posts do dia (qualquer etapa menos roteiro, com
  link do bloco no painel), pergunta se pode seguir e, com o ok, agenda no **mLabs**.
- **Fase de testes:** nada vai para `aguardando_aprovacao` sem o ok do Guilherme.
- **API com chave única** para todos os bots. Os limites de cada bot vêm das instruções, por isso a API
  não tem nenhuma operação destrutiva.
- **Lari:** até 3 avisos e 2 sugestões por cliente por semana, nunca interrompe conversa em curso e
  escala mensagens longas ao WhatsApp do Guilherme com uma sugestão de resposta.
- **Segurança:** as regras do `straut-brain` continuam valendo e os bots seguem as mesmas. Nunca há
  segredos no GitHub, os bots nunca apagam nada e dados de pacientes nunca são gravados.

## 3. O que cada conversa faz agora

### Straut Brain · App
1. **Construir a API dos bots** conforme [`api-dos-bots.md`](api-dos-bots.md) (já aprovada pelo
   Guilherme). Ao terminar, atualizar esse arquivo com as rotas reais e o status ✅.
2. **Atualizar o `CLAUDE.md` do `straut-brain`:** a memória da conversa Clientes passa a ser
   `straut-team/clientes/` (a pasta local `clientes/` deixa de ser a fonte).
3. Manter [`straut/painel.md`](../straut/painel.md) atualizado quando o painel mudar.
4. Avaliar com o Guilherme as melhorias da seção 4.

### Straut Brain · Clientes
1. **Migrar as fichas** da pasta local `clientes/` (ou do backup) para `straut-team/clientes/<slug>/`,
   seguindo [`clientes/_modelo/`](../clientes/_modelo/). As pastas `jose-erasmo`, `caroline-skaf`,
   `juliana-annunciato`, `wa-concept` e `straut` já existem com campos `FALTA`.
2. **Não migrar:** senhas, contratos, valores, dados bancários, CPF, endereço ou dados de pacientes.
3. Daqui em diante, gravar o que descobrir sobre as clientes em `straut-team/clientes/`, porque os
   bots leem dali.

## 4. Como o painel contribui com o sistema

### O que o painel já resolve
O painel é a **fonte da verdade dos conteúdos**: cada bloco acompanha o post do roteiro à publicação,
com status, aprovação da cliente, sugestões no estilo controle de alterações, comentários, histórico de
versões e mídias (inclusive vídeo pelo Drive). A meta do contrato (`contract_posts`) define quantos
roteiros os Gestores criam. O link direto do bloco (`/c/<slug>?bloco=<id>`) já existe e é o que o
Samuel envia ao Guilherme.

| Onde fica | O quê |
|---|---|
| **Painel** | Conteúdos, status, aprovações, comentários, mídias, meta de posts |
| **straut-team** | Conhecimento: perfil, tom, histórico, regras, decisões, relatórios |
| **mLabs** | Métricas e agendamento dos posts |
| **OpenBot** | Os bots e as conversas com o Guilherme |
| **WhatsApp da Straut** | Conversas com as clientes (só a Lari) |

### Melhorias sugeridas (a decidir com o Guilherme)

**Prioridade 1: necessário para ligar os bots**
- **API dos bots** ([`api-dos-bots.md`](api-dos-bots.md)).
- **Registro das ações dos bots:** uma tabela com o bot, a rota, o bloco e o horário. Hoje o
  `block_history.author` só aceita `Straut` ou `Cliente`, e o nome do bot ficaria só no texto. Com o
  registro, dá para saber qual bot fez o quê e desfazer erros.
- **Filtro "reels com vídeo e sem capa"** contando também os vídeos do Drive (`drive:<id>`).
- **A API nunca devolve** a senha da página, o dia de pagamento, os arquivos da cliente (contratos)
  nem chaves do sistema.

**Prioridade 2: economiza rotinas e evita erros**
- **`GET /api/bots/novidades?desde=<data e hora>`:** o que mudou desde a última checagem (cliente
  aprovou, sugeriu, comentou ou um vídeo foi enviado). Uma chamada barata no lugar de varrer todos os
  blocos, que serve às rotinas do Samuel, dos Gestores e do Design.
- **Marca "agendado no mLabs"** (data e hora do agendamento, com um selo no bloco). O Guilherme vê no
  calendário o que já está agendado e o Samuel nunca agenda o mesmo post duas vezes.
- **Link direto do bloco na página da cliente** (`/p/<slug>?bloco=<id>`), se ainda não existir,
  para a Lari mandar à cliente o link exato do conteúdo que aguarda aprovação.

**Prioridade 3: depois que o time estiver rodando**
- **Caixa "Pedidos dos bots" no painel:** os pedidos de autorização do Samuel aparecem ao lado de
  "Precisa da sua atenção", e o Guilherme aprova com um clique.
- **Sugestão de "publicado":** o Samuel confere no mLabs e sugere marcar o post como publicado; o
  Guilherme confirma com um clique (marcar publicado continua sendo dele).
- **Selo "usado em anúncio"** no bloco, para o Tráfego e o Analista.
- **Números do post no bloco** (alcance, visualizações e salvamentos vindos do mLabs depois da
  publicação), para a Analista e para as clientes verem o resultado no mesmo lugar.

## 5. Como responder
Grave as respostas e o andamento neste repositório: a API em `api-dos-bots.md`, as decisões em
`gestao/decisoes.md` e as fichas em `clientes/`. Os bots e a conversa "Chatbots Straut" leem daqui.
