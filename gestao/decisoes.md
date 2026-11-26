# Decisões

Registro das decisões do Guilherme que afetam o time. **Só acrescente**, nunca apague.
Formato: `AAAA-MM-DD · decisão · motivo / contexto`. A entrada mais nova fica no topo.

---

- 2026-11-26 · Prompt mestre do OpenBot reescrito (`openbot/prompt-mestre.md`) com a infraestrutura
  completa: peças do sistema, modelos de IA, forma de trabalhar, os 8 fluxos, as 17 rotinas, os
  acessos de cada bot, autorizações e o que ainda está em construção.
- 2026-11-26 · Passagem para o Straut Brain (App e Clientes) em
  `integracoes/passagem-straut-brain.md`: resumo das decisões, a migração das fichas das clientes para
  `straut-team/clientes/` e as melhorias sugeridas para o painel (a decidir com o Guilherme).
- 2026-11-24 · Criado o bot **Tráfego** (gestor de tráfego pago no Google Ads e na Meta, Opus 5.5),
  começando na **fase 0 (setup das contas)**. Implantação em fases (0 setup → 1 só leitura → 2
  rascunhos pausados → 3 otimização com limites), cada avanço com ok do Guilherme. Ativar campanha,
  aumentar verba e mexer em pagamento sempre com ok. Os detalhes de cada cliente (verba, quem paga,
  objetivo, autonomia) o Guilherme define direto com o bot.
- 2026-11-24 · Complemento das referências com o que faltava das skills `copywriting` e `social`:
  `escrita-de-copy.md` (método de escrita e fórmulas de título), `reaproveitamento-de-conteudo.md`,
  vícios de redes sociais em `texto-sem-cara-de-ia.md`, limites do Instagram em `ganchos-e-roteiros.md`
  e o "manual do nicho" (engenharia reversa) em `perfil-de-concorrentes.md`.
- 2026-11-24 · Referências de marketing adicionadas em `referencias/`, adaptadas do repositório
  `coreyhaines31/marketingskills` (licença MIT): ganchos, carrosséis, texto sem cara de IA, revisão,
  pesquisa de público, concorrentes e rotinas seguras. Só as skills úteis para a Straut, em português e
  filtradas pelo CFM. Criado o comando **"PAUSA GERAL" / "RETOMAR"**.
- 2026-11-23 · Ajuste das rotinas (pedido do Guilherme):
  - Roteiros com **um mês de antecedência**: no dia 1, roteiros de todos os conteúdos do mês seguinte
    (vídeos, carrosséis e fotos), na quantidade da meta de posts da cliente no painel. Pauta da
    Estratégia passa para o dia 20, dois meses à frente.
  - **Dia 20:** o Design cria as artes dos carrosséis do mês seguinte, mesmo sem roteiro aprovado
    (sobem no painel quando o roteiro for aprovado).
  - **Capas de reels só depois do upload do vídeo** no painel (checagem diária do Design às 11h).
  - **Samuel, todo dia às 8h:** envia os posts do dia (qualquer etapa, menos roteiro, com link no
    painel), pergunta se pode seguir e, com o ok, agenda no mLabs.
  - **Analista:** recordes só às quartas.
  - **Social Media:** stories + reels viral prontos na segunda para o Gestor avaliar. Stories
    enviados na segunda (14h, por causa da regra das 4 horas), reels viral a partir de terça.
  - **Lari, segunda às 9h:** bom dia e boa semana (só sem conversa ativa e sem mensagem sem resposta),
    com um texto diferente toda semana. Não conta no limite de avisos.
- 2026-11-23 · O Claude (Straut Brain) é a ferramenta pessoal do Guilherme para o painel e para
  trabalhos especiais. Os bots fazem a rotina. Os dois leem e escrevem neste repositório.
- 2026-11-23 · Regras de sincronização com o GitHub aprovadas (`equipe/regras-gerais.md`, seção 4).
- 2026-11-23 · Lari: até 3 avisos e 2 sugestões (1 reels viral + 1 stories) por cliente por semana,
  contados separadamente. Não interromper conversas em curso (mensagem nas últimas 4 horas ou cliente
  aguardando resposta). Envios de segunda a sexta, das 9h às 19h.
- 2026-11-23 · Lari escala mensagens longas ou que dependem de ação humana para o WhatsApp do Guilherme,
  com a natureza da mensagem e uma sugestão de resposta.
- 2026-11-23 · Tom da Lari: próximo e amigável, um meio-termo entre profissionalismo e parceria.
- 2026-11-23 · Samuel conversa com o Guilherme direto pelo app do OpenBot.
- 2026-11-23 · API dos bots do painel com **uma chave única** para todos os bots.
- 2026-11-23 · Fase de testes: conteúdos só vão para aprovação da cliente depois do ok do Guilherme
  (pedido em lote pelo Samuel).
- 2026-11-23 · Repositório `straut-team` criado (privado) como ponto de contato entre o OpenBot e o Claude.
