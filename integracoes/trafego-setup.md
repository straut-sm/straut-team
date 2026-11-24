# Setup de contas de tráfego pago (Google Ads e Meta)

> Guia do bot **Tráfego** para conduzir o setup com o Guilherme. O Guilherme (ou a cliente) faz o que
> exige login e pagamento. O bot orienta, confere e registra o status em `clientes/<slug>/trafego.md`.
> **Nenhuma chave, senha ou token vai para este repositório.** Tudo fica no cofre de credenciais do OpenBot.
> Informações de acesso conferidas em 24/11/2026. As plataformas mudam: em caso de diferença, vale a
> documentação oficial.

---

## Parte A: estrutura da Straut (uma vez só)

### A1. Google
- [ ] **Conta de administrador (MCC) da Straut** criada no Google Ads (fuso `America/Sao_Paulo`, moeda BRL).
- [ ] Guilherme como administrador. Nenhum bot com login de usuário.
- [ ] **Projeto no Google Cloud** da Straut com a **Google Ads API** ativada.
  - Desde **9/9/2026 o Google aposentou o *developer token***. O nível de acesso à API (teste,
    Explorer, Basic) agora fica **no projeto do Google Cloud**. Peça o nível de acesso no próprio
    projeto (página "Google Ads API Overview" do Cloud Console).
  - Projeto com acesso só de teste não chama contas reais (erro `CLOUD_PROJECT_NOT_APPROVED_FOR_PRODUCTION`).
- [ ] Credenciais OAuth (ou conta de serviço) do projeto, com o escopo `https://www.googleapis.com/auth/adwords`.
  As chamadas pela MCC usam o cabeçalho `login-customer-id` com o ID da MCC.
- [ ] **Leitura:** conector MCP oficial do Google Ads (`github.com/googleads/google-ads-mcp`). Na
  versão atual ele é **só leitura** (relatórios e diagnósticos). Conferir o README antes de usar.
- [ ] **Alterações (fases 2 e 3):** chamadas da Google Ads API pelo mesmo projeto.

### A2. Meta
- [ ] **Gerenciador de Negócios (portfólio empresarial) da Straut** criado e **verificado**.
- [ ] Guilherme como administrador. Autenticação de dois fatores ligada para todos.
- [ ] **Acesso dos bots**, uma das duas opções:
  - **Meta Ads AI Connectors (MCP oficial):** `https://mcp.facebook.com/ads`. Em **beta desde
    29/04/2026**, com ferramentas de relatório, criação e gestão de campanhas. Login pelo Facebook Login
    for Business. Pode não estar liberado para todas as contas ainda.
  - **Marketing API:** um app da Meta da Straut e um **usuário do sistema** no Gerenciador de Negócios,
    com token e permissões `ads_read` (fase 1) e `ads_management` (fases 2 e 3). Pode exigir revisão do app.
- [ ] **Começar só com leitura.** Conferir as respostas do bot com o Gerenciador de Anúncios por algumas
  semanas antes de liberar escrita.

### A3. OpenBot
- [ ] Cadastrar as credenciais (Google e Meta) no cofre de credenciais do OpenBot.
- [ ] Criar o bot Tráfego (`openbot/prompts.md`) e as rotinas (`openbot/rotinas.md`), **desativadas**
  até a fase 1.

---

## Parte B: por cliente: Google Ads

### B1. Conta
- [ ] A cliente tem conta? Se sim, **mantenha a dela** (o histórico vale). Se não, crie em nome dela.
- [ ] **A conta pertence à cliente.** A Straut entra como administradora pela **vinculação à MCC**
  (a cliente aceita o convite).
- [ ] Fuso `America/Sao_Paulo`, moeda **BRL** (não dá para mudar depois).
- [ ] **Pagamento: cartão ou boleto da própria cliente**, cadastrado por ela.
- [ ] **Orçamento da conta** ou controle de gasto definido com o Guilherme. O Google pode gastar até
  **2x o orçamento diário** num dia, compensando no mês.

### B2. Medição
- [ ] **Google Analytics 4** da cliente (se houver site) vinculado ao Google Ads, com marcação automática ligada.
- [ ] **Ações de conversão** (só as que importam):
  - clique para o WhatsApp (botão no site ou anúncio);
  - ligações a partir do anúncio (recurso de ligação);
  - formulário ou agendamento no site, se houver.
- [ ] **Testar cada conversão com uma conversão real** antes de anunciar.
- [ ] ⚠️ **Conversões aprimoradas e importação de conversões off-line:** envolvem dados pessoais. Para
  clientes de saúde, só com o ok do Guilherme e **sem nenhuma informação de saúde**
  (`regras-do-setor/anuncios-saude.md`).
- [ ] **Perfil da Empresa no Google** da clínica vinculado (recurso de local nos anúncios).

### B3. Campanhas (padrão inicial de rede de Pesquisa)
- [ ] **Local:** endereço + raio combinado, com a opção **"Presença"** (pessoas que estão na região),
  e não "presença ou interesse".
- [ ] **Idioma:** português.
- [ ] **Parceiros de pesquisa e Rede de Display: desligados** no começo.
- [ ] **Campanha de marca** (nome da médica ou da clínica) com orçamento próprio e baixo.
- [ ] **Campanha de alta intenção local** ("dermatologista em [cidade]", "neurocirurgião coluna [bairro]")
  com orçamento próprio, nunca compartilhado com a de marca.
- [ ] **Palavras negativas iniciais:** emprego, vaga, salário, curso, faculdade, residência, concurso,
  "como ser", pdf, grátis/gratuito. Decida **com o Guilherme** termos como "SUS", "convênio" e
  "plano de saúde", conforme a cliente atenda ou não.
- [ ] **Recursos do anúncio:** sitelinks (de 4 a 6), frases de destaque, local, ligação, snippets
  estruturados (serviços).
- [ ] **Anúncios responsivos de pesquisa:** até 15 títulos (30 caracteres) e 4 descrições (90
  caracteres), revisados pelo Revisor.

---

## Parte C: por cliente: Meta (Facebook e Instagram)

### C1. Acessos
- [ ] A cliente tem um **Gerenciador de Negócios** próprio (ou cria um). **Os ativos pertencem a ela.**
- [ ] A cliente dá **acesso de parceiro** ao Gerenciador da Straut para: **conta de anúncios**,
  **página do Facebook**, **conta do Instagram**, **conjunto de dados/pixel** e **conta do WhatsApp
  Business** (se for usar anúncios para o WhatsApp).
- [ ] Conta de anúncios com fuso `America/Sao_Paulo` e moeda **BRL**.
- [ ] **Pagamento da própria cliente.**
- [ ] **Limite de gastos da conta** configurado (é a trava que nenhum bot ultrapassa). Valor definido pelo Guilherme.

### C2. Canais
- [ ] Instagram profissional conectado à página.
- [ ] **WhatsApp Business** da clínica conectado à página, para os anúncios que abrem conversa no
  WhatsApp. Confirmar **quem atende** essas conversas: elas vão para o WhatsApp da clínica, **não para
  o da Straut (Lari)**.

### C3. Medição
- [ ] Se houver site: **Pixel/conjunto de dados** instalado + **API de Conversões** (do lado do
  servidor), com eventos simples (`Contact`, `Lead`). **Nenhum evento ou parâmetro que revele
  condição de saúde**, procedimento ou especialidade procurada pela pessoa.
- [ ] Domínio do site verificado no Gerenciador de Negócios.
- [ ] Testar os eventos no Gerenciador de Eventos.
- [ ] ⚠️ A Meta restringe alguns eventos de conversão e otimizações para anunciantes de saúde e bem-estar.
  Conferir no Gerenciador de Eventos o que está disponível para a conta.

### C4. Públicos
- [ ] Públicos de **engajamento do Instagram** (30, 90 e 365 dias) e de **visualização de vídeo**
  (50% e 75%).
- [ ] Semelhantes (1% a 3%) a partir dos públicos de engajamento.
- [ ] ⛔ **Não subir listas de pacientes** (dado de saúde é dado sensível pela LGPD).
- [ ] Segmentação principal: **região + público amplo**, deixando o criativo "escolher" quem se interessa.
  ⛔ Nunca por condição de saúde.

### C5. Criativos (formatos)
- [ ] Feed: 1080 × 1350 (4:5) ou 1080 × 1080 (1:1). Stories e Reels: 1080 × 1920 (9:16).
- [ ] Prioridade: **reels e carrosséis que já foram bem no orgânico**, rodando como anúncio.
- [ ] Todo criativo passa pelo Revisor (CFM + políticas).

---

## Parte D: checklist antes de ativar qualquer campanha
- [ ] Conversão testada com um evento real
- [ ] Página de destino ou WhatsApp funcionando no celular (página carrega em menos de 3 segundos)
- [ ] Parâmetros UTM nos links do site
- [ ] Orçamento (diário ou total), datas de início e fim conferidos
- [ ] Região e público conferidos
- [ ] Criativos aprovados pelo Revisor **e** pela plataforma
- [ ] Plano de mídia aprovado pelo Guilherme
- [ ] Registro em `gestao/trafego/alteracoes.md`

---

## Parte E: registro
Cada item concluído vai para `clientes/<slug>/trafego.md` (seção "Status do setup"), com data e quem fez.
Os IDs das contas podem ser anotados. **Senhas, tokens e dados de cartão nunca.**
