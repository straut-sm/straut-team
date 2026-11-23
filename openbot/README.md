# Como configurar o time no OpenBot (openbot.run)

Passo a passo para o Guilherme. Marque cada item quando terminar.

> **Atalho:** depois do passo 2, cole o [`prompt-mestre.md`](prompt-mestre.md) no OpenBot para ele criar o time inteiro (passos 3 e 4).

## 1. Contas e chaves
- [ ] **Claude Console** (platform.claude.com): conta, créditos, limite de gasto mensal e uma chave de
      API. Detalhes em [`modelos-de-ia.md`](modelos-de-ia.md). O plano Claude Pro **não** cobre a API.
- [ ] **GitHub:** token fino só para `straut-sm/straut-team`, com *Contents: Read and write*
      (veja [`../integracoes/github.md`](../integracoes/github.md)).
- [ ] **API dos bots do painel:** pedir ao Straut Brain · App para construir
      ([`../integracoes/api-dos-bots.md`](../integracoes/api-dos-bots.md)) e gerar a chave.
- [ ] **WhatsApp:** definir o número e a integração da Lari ([`../integracoes/whatsapp.md`](../integracoes/whatsapp.md)).
- [ ] **mLabs e Canva:** conectar no OpenBot (MCP ou integrações) para Analista, Estratégia, Social
      Media e Design. O **Samuel** precisa do mLabs com permissão de **agendar posts**.

## 2. No OpenBot
- [ ] Conferir a licença e o plano para **uso comercial** (a página do OpenBot diz que o uso em
      produção exige licença).
- [ ] Ativar o login (não deixar no modo de usuário único sem senha).
- [ ] Cadastrar as credenciais (chave do Claude, token do GitHub, chave da API dos bots, WhatsApp)
      no cofre de credenciais. **Nunca** colar chaves nas instruções dos bots.
- [ ] Escolher o provedor **Anthropic (Claude)**.

## 3. Criar os bots
Para cada bot: nome, **instruções** (texto em [`prompts.md`](prompts.md)), modelo
([`modelos-de-ia.md`](modelos-de-ia.md)) e **para quem repassa trabalho** (handoff; tabela em
[`../equipe/README.md`](../equipe/README.md)).

| Ordem | Bot | Modelo |
|---|---|---|
| 1 | Samuel | Opus 5.5 |
| 2 | Revisor | Opus 5.5 |
| 3 | Copy | Opus 5.5 |
| 4 | Estratégia | Opus 5.5 |
| 5 | Analista | Sonnet 5.5 |
| 6 | Social Media | Sonnet 5.5 |
| 7 | Design | Sonnet 5.5 |
| 8–12 | Gestor · Dr. José Erasmo / Dra. Caroline Skaf / Dra. Juliana Annunciato / WA Concept / Straut | Sonnet 5.5 |
| 13 | Lari | Sonnet 5.5 |

Em cada bot, peça na primeira conversa:
> "Clone o repositório straut-sm/straut-team em ~/straut-team, configure o git com o seu nome de bot
> e leia equipe/regras-gerais.md e a sua ficha. Depois me diga com suas palavras o que você faz e o
> que precisa de autorização."

Se a resposta estiver certa, o bot está pronto.

## 4. Rotinas
Criar as 14 rotinas de [`rotinas.md`](rotinas.md).

## 5. Teste antes de ligar para as clientes
1. **Samuel:** peça "o que tem pendente nas clientes?" e confira se ele delega e responde certo.
2. **Uma demanda completa:** peça ao Samuel um carrossel para uma cliente e acompanhe o fluxo
   Gestor → Copy → Design → Revisor → painel (`em_producao`) → pedido de autorização.
3. **Lari em teste:** conecte a Lari **ao seu número** primeiro e simule uma cliente: dúvida simples,
   mensagem longa, reclamação, pedido de gravação e a pergunta "você é um robô?".
4. **Repositório:** confira no GitHub se os bots gravaram e fizeram commit do que deviam.
5. Só depois ligue a Lari no número da Straut, uma cliente por vez.

## 6. Manutenção
- O Samuel lembra de renovar o token do GitHub (90 dias).
- Ao mudar uma regra: atualize `equipe/`, depois `prompts.md` e o OpenBot, e registre em
  `gestao/decisoes.md`.
