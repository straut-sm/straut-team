# Decisões

Registro das decisões do Guilherme que afetam o time. **Só acrescente**, nunca apague.
Formato: `AAAA-MM-DD · decisão · motivo / contexto`. A entrada mais nova fica no topo.

---

- 2026-11-28 · **Rotinas, ajuste da noite** (Guilherme): a rotina 3 roda uma vez, às 13h, com os
  avanços, os pedidos ao Design e as pendências numa só mensagem. A rotina 19 passa para as 7h e
  monta o envio por script, sem redigitar números. O texto da rotina 11 foi atualizado (a Lari está
  no WhatsApp). **Todas as rotinas ficam ativas, menos a 18.** Apagadas as rotinas avulsas da Lari já
  concluídas ou canceladas e a "Dra. Carol · conferir respostas". Fica ativa a checagem de hora em
  hora do WhatsApp da Lari (só leitura).
- 2026-11-28 · **Ajuste das rotinas** (Guilherme): o time passa a ter **11 rotinas**.
  - **Excluídas:** 1 (posts do dia do Samuel), 2 (resumo semanal), 7 (artes e capas do Design), 14
    (avisos da Lari) e 15, 16 e 17 (todas do Tráfego, por enquanto). Posts do dia, resumo semanal e
    avisos às clientes só quando o Guilherme pedir. O Design trabalha quando o Samuel pedir (o Samuel
    vê na rotina 3 os carrosséis aprovados e os reels com vídeo e sem capa). O Tráfego só trabalha
    quando pedido.
  - **Social Media (rotina 10, segunda 7h):** pesquisa as tendências e preenche a aba Tendências do
    painel com **3 virais do nicho e 4 ideias de stories** por cliente (sem a "tendência do mês" e sem
    arquivo em `sugestoes/`).
  - **Lari (rotinas 12 e 13, mesmos horários):** envia os stories e os reels virais **direto da aba
    Tendências**, só de semana liberada pelo Guilherme. Recordes da Analista: a Lari pergunta ao
    Guilherme antes de enviar.
- 2026-11-27 · **Reorganização do time para economizar tokens** (Guilherme, com o Claude):
  1. **Os 5 Gestores de cliente foram desativados.** A parte operacional (painel, roteiros aprovados,
     dias de produção, ajustes da cliente) foi para o **Samuel**; o planejamento (calendário do mês,
     perguntas para a cliente, pedido de roteiros) foi para a **Estratégia**. O Copy cria os blocos de
     roteiro no painel depois do Revisor. Mapa completo em `equipe/gestor-de-cliente.md`; divisão
     por cliente em `clientes/<slug>/resumo.md`.
  2. **Um dono por tarefa:** métricas das clientes no mLabs só com a **Analista** (grava no painel pela
     nova rota `PUT /clientes/:slug/metricas`; os outros leem do painel); referências e tendências só
     com a **Social Media** (inclusive a aba Tendências do painel); agendar e postar só com o **Samuel**.
     As duas rotinas do Claude que faziam métricas e tendências serão desligadas quando as dos bots
     estiverem rodando.
  3. **Regras de economia** (`equipe/regras-gerais.md`, seção 12): passar o número do bloco e não o
     texto; usar `GET /novidades` em vez de varrer o painel; não reler regras e ficha a cada tarefa;
     ler primeiro o `resumo.md` da cliente.
  4. **Revisor em dois modos:** revisão completa no roteiro; checagem curta na peça final.
  5. **Sem validação das sugestões semanais:** a Social Media aplica os filtros e manda direto à Lari.
  6. O ok em lote pelo painel **não** será implementado por enquanto: o Samuel continua pedindo o ok
     do lote ao Guilherme pela conversa.

- 2026-11-27 · **mLabs conectado ao OpenBot** pelo MCP oficial (`https://mcp.mlabs.io/mcp`, beta,
  incluído na assinatura), com o login da Straut autorizado pelo Guilherme. Os perfis com Instagram
  conectado são WA Concept e Dr. José. A Dra. Juliana tem só o TikTok, a Dra. Caroline não tem
  nenhuma rede, e a Straut não tem perfil. Regras de uso em `equipe/regras-gerais.md`, seção 5.2:
  só leitura; o agendamento é só do Samuel, com o ok do dia; nenhum bot apaga nada.
- 2026-11-27 · **Google Drive no computador:** o Guilherme vai instalar o Google Drive para
  computador neste PC, para os bots conferirem os conteúdos do Drive da Straut (uso imediato: as fotos
  dos produtos da WA Concept para o post de 28/11). Regra dele: **"nenhum bot pode excluir arquivos
  do drive"**. Registrado em `equipe/regras-gerais.md`, seção 5.1. Orientação passada pela Manu.
  Perguntado se também devia proibir mover e renomear, o Guilherme respondeu que a regra é **só não
  excluir**.
- 2026-11-27 · Criada a **Manu, diretora criativa** (Opus 5.5): guia visual de cada cliente,
  banco de referências, direção de foto e de gravação, prompts visuais otimizados e olhar de feed
  (rotina 18, quinta às 10h). **Samuel, Manu e Lari ficam no mesmo nível**, logo abaixo do
  Guilherme: conversam entre si e recebem orientações direto dele. O guia visual precisa só do ok do
  Guilherme (a cliente não aprova). O Design passa a ser o designer que executa o guia. Nunca imagens
  de IA de pessoas, pacientes ou resultados.
- 2026-11-26 · Dra. Caroline Skaf: pilares aprovados pelo Guilherme, com procedimentos 50%, complicações 25%, prevenção 19% e Natal 6%. Motivo: dar menos peso a complicações, porque ultimamente o foco tem sido procedimentos. Dezembro tem foco em conversão para janeiro e para as férias (detalhes em clientes/caroline-skaf/historico.md).
- 2026-11-26 · O formato novo dos roteiros e as lições do teste da WA Concept passam a ser o
  **padrão para todos os Gestores e clientes** ("Padrão de qualidade" em
  `modelos/pedido-de-producao.md`).
- 2026-11-26 · **Novo formato dos roteiros** (feedback da Bia, da equipe da Straut, encaminhado pelo
  Guilherme pela Lari): cabeçalho limpo (título, formato, intenção e gancho); sem minutagem nem
  tabela; vídeo com fala com texto completo para o teleprompter; vídeo sem fala com cenas essenciais
  e 2 frases de apoio; carrossel com textos curtos e 2 sugestões de foto; foto com opções flexíveis;
  conteúdo que responde ao que promete, mostra o benefício e não parece comercial. Modelos
  `roteiro-reels.md` e `carrossel.md` reescritos; feedback completo em
  `OpenBot/Shared/feedback-bia-wa-concept-2026-11-26/feedback.md`.
- 2026-11-26 · **Fim de semana:** sábado pode ter post. Domingo, só quando for comemoração de uma data
  específica que cai no domingo (ex.: Dia das Mães). Vale para o calendário de todas as clientes.
- 2026-11-26 · WA Concept, dezembro: incluir o post extra "Feliz 2027" em 31/12 (13º do mês, acima
  da meta, por decisão do Guilherme).
- 2026-11-26 · Correções do processo de produção, depois do teste da WA Concept (pedido do Guilherme):
  1. **Mês atual primeiro:** antes de produzir o mês seguinte, o mês atual precisa bater a meta.
  2. **Datas variadas:** os conteúdos são distribuídos pelos dias da semana conforme o melhor formato
     de cada dia (`clientes/<slug>/estrategia/dias-e-formatos.md`, mantido pela Estratégia com dados
     do Analista). Nada de usar sempre os mesmos dias da semana.
  3. **Quantidade = meta:** se o Guilherme pedir outro número, o Samuel corrige e recomenda a meta
     antes de delegar.
  4. **Informação da cliente:** se algum bot precisa de algo que só a cliente sabe, o Samuel manda
     primeiro as perguntas ao Guilherme e espera as respostas. Ninguém produz com `[FALTA]`.
  5. **Calendário comercial obrigatório** na pauta da Estratégia (Natal, Ano Novo etc.).
  6. **Design só depois da aprovação do roteiro pela cliente.** A rotina 6 (artes no dia 20) foi
     removida; as artes de carrossel entraram na rotina 7 (seg a sex, 11h).
  7. **Ganchos:** o Copy cria 3 opções, escolhe a melhor e só ela vai para o roteiro.
  8. **Ambiente real:** roteiros viáveis no espaço e na rotina da cliente, sem produção externa.
  9. Novo modelo `modelos/pedido-de-producao.md` para todo pedido do Samuel aos Gestores.
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
- 2026-11-26 · API dos bots publicada no painel. Os bots podem criar, editar (em qualquer status), anexar e
  reordenar mídias, avançar roteiros, enviar para aprovação, comentar (comentários internos), marcar como
  publicado, aceitar sugestões e apagar. Só o Guilherme aprova, restaura versões e edita o cadastro das clientes.
- 2026-11-26 · Lixeira no painel: tudo o que é apagado (pelo Guilherme ou pelos bots) fica 30 dias, pode ser
  restaurado e depois é apagado de vez.
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
