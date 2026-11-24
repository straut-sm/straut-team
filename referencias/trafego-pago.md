# Tráfego pago: como operar Google e Meta

> Referência para o bot **Tráfego**. Adaptado das skills `ads` e `conversion-tracking` do
> marketingskills (que por sua vez credita os trabalhos de Daniel Agrici/claude-ads, Marek Dąbrowski
> e Ivan Falco). Os originais são de software B2B. Aqui estão adaptados para **consultórios e clínicas**.
> **Todos os números são pontos de partida:** recalibre com os dados de cada conta depois de 30 dias.
> As regras de `regras-do-setor/anuncios-saude.md` sempre prevalecem.

## 1. A medida que importa
- **Resultado da plataforma:** conversa iniciada no WhatsApp, ligação, clique, formulário.
- **Resultado real:** **agendamento**, e se a pessoa compareceu. A plataforma não vê isso, então é
  preciso perguntar à cliente (ou à secretária) quantas conversas viraram agendamento.
- **Custo-alvo por agendamento:** é a âncora das decisões. Defina com o Guilherme:
  1. pela conta (quanto vale um paciente novo e quanto a cliente aceita pagar por um agendamento);
  2. pelo histórico (custo dos últimos 30 dias × 0,8);
  3. conta nova: um valor provisório, revisto depois de 30 dias.
- **Taxa de qualidade** = agendamentos ÷ conversas. Dois anúncios com o mesmo custo por conversa
  podem ter custos reais por agendamento muito diferentes.

## 2. Regras de evidência
- Cada item checado tem um de quatro resultados: **OK** (viu e está certo), **Problema** (viu e está
  errado), **Não verificado** (não teve acesso) ou **Não se aplica**. "Não consegui ver o pixel" ≠
  "o pixel está quebrado".
- Dado que falta = **FALTA**, fora de qualquer conta.
- **Não some Meta + Google.** Mostre lado a lado, com a janela de atribuição de cada uma.
- Dias recentes têm conversões incompletas. **Um período contra um período não é tendência:** compare
  com as últimas 6 a 8 semanas.
- Média de mercado é só direção. A ordem de confiança é: a própria conta → teste da própria conta →
  dados da cliente → pesquisa independente → média de mercado.
- **Nunca invente palavras negativas** sem o relatório de termos de pesquisa.
- **Não pause um anúncio só porque o custo dobrou** com poucas conversões. Confira o tamanho da
  amostra e o atraso das conversões antes.

## 3. A checagem semanal (sexta-feira)
Siga esta ordem e pare na primeira causa real (os problemas de cima explicam os sintomas de baixo):

| # | Pergunta | Onde olhar | Causa típica |
|---|---|---|---|
| 1 | **O gasto mudou?** | Ritmo × orçamento, limites batidos | Mudança de orçamento, limite, pagamento |
| 2 | **O tráfego mudou?** | Cliques, custo por clique, CTR, CPM, termos novos | Concorrência, palavra-chave saindo do foco |
| 3 | **As conversões mudaram?** | Taxa de conversão, custo por conversa, qualidade (agendamentos) | Sazonalidade, oferta, atraso de conversões |
| 4 | **O criativo cansou?** | Frequência, CTR em relação ao pico do anúncio | Público saturado, sem criativos novos |
| 5 | **O destino quebrou?** | WhatsApp, site, formulário no celular | Número trocado, site fora do ar |
| 6 | **O rastreamento quebrou?** | Conversões × o que a cliente informa | Tag removida, evento duplicado |

Sempre compare com o **histórico de alterações** (`gestao/trafego/alteracoes.md`): uma métrica que
mudou um dia depois de uma alteração provavelmente mudou por causa dela.

**Cada checagem termina em UMA decisão por conta:**

| Decisão | Quando |
|---|---|
| **MANTER** | A variação está dentro do normal das últimas 6 a 8 semanas, há poucos dados, está em aprendizado ou é atraso. Diga o porquê e o que mudaria a decisão |
| **CORRIGIR** | Um problema conhecido com solução conhecida: anúncio reprovado, conversão que parou, orçamento limitando uma campanha que funciona |
| **TESTAR** | Uma hipótese que vale verba: criativo novo contra fadiga, nova palavra-chave. Diga a métrica e **a regra de parada** |
| **INVESTIGAR** | Os dados não são confiáveis (rastreamento em dúvida, números que não batem). **Vence tudo:** nenhuma decisão de desempenho até resolver |

Nenhuma decisão move dinheiro sozinha: vira proposta (`modelos/proposta-de-alteracao.md`) para o ok
do Guilherme, salvo o que estiver liberado em "Autonomia".

## 4. Meta
- **O criativo é a segmentação.** Público amplo na região + criativo específico. O algoritmo usa o
  conteúdo do anúncio para achar quem se interessa. Evite empilhar interesses.
- **Volume de criativos:** o algoritmo cansa rápido. Tenha sempre de 2 a 3 criativos novos prontos.
  Estáticos e reels simples costumam render tanto quanto produções caras.
- **Conteúdo orgânico que foi bem é o melhor anúncio.** Reels e carrosséis com muitos salvamentos e
  compartilhamentos → rodar como anúncio (o Analista indica).
- **Não pareça anúncio:** conteúdo nativo do Instagram funciona melhor, sempre dentro do CFM.
- **Palavra de identidade:** a mesma peça com a região ou o público no texto ("em Moema", "para quem
  tem pele oleosa", cuidando da regra de atributos pessoais) pode baixar o custo.
- **Estrutura simples:** uma campanha principal (cerca de 80% da verba, só com o que funciona) e uma
  campanha de teste (cerca de 20%, com criativos novos), para os novos não ficarem sem verba.
- **Aprendizado:** a Meta sai da fase de aprendizado com cerca de **50 conversões por semana** no
  evento otimizado. Com verba pequena, otimize um evento mais frequente (ex.: conversa iniciada).
- **Não edite um anúncio que está funcionando** (reinicia o aprendizado). Lance o novo ao lado. Pausar
  não reinicia, editar sim.
- **Fadiga (público frio):** frequência de 1 a 2,5 ok · de 2,5 a 4 atenção · acima de 4 crítica.
  Outros sinais: CTR caindo 20% ou mais em 7 dias, CPM subindo 30% ou mais em 2 semanas. Nunca pause
  sem um substituto pronto.
- **Escala:** no máximo **+20% de orçamento a cada 5 dias**. Nunca +30% ou mais de uma vez. Se o
  custo piorar 50% depois de um aumento, volte de 20% a 30% e estabilize por 2 semanas.
- **Dê cerca de 5 dias** antes de julgar um anúncio novo.

## 5. Google (Pesquisa)
- **A escada da intenção:** a verba sobe degrau por degrau, e cada degrau só abre depois que o de baixo
  mostra agendamentos:
  1. **Marca** (nome da médica ou da clínica): barato, sempre ligado, com orçamento próprio.
  2. **Alta intenção local** ("dermatologista [bairro/cidade]", "neurocirurgião coluna [cidade]"):
     onde fica a maior parte da verba.
  3. **Problema** ("tratamento para melasma", "hérnia de disco tratamento"): depois que 1 e 2 funcionarem.
  4. Display, YouTube e Performance Max: por último, só com verba sobrando e rastreamento confiável.
- **A pesquisa colhe a demanda que existe, ela não cria demanda.** Pouca busca na região → a verba vai para a Meta.
- **Orçamentos separados** por campanha. Nunca compartilhado com a de marca (ela engole o resto).
- **Grupos de anúncios por tema** (de 5 a 15 palavras com a mesma intenção). De 2 a 3 anúncios por grupo.
- **Correspondência:** comece com **frase e exata**. Ampla só com 30 ou mais conversões por mês,
  lances inteligentes e lista de negativas firme.
- **Ritual semanal dos termos de pesquisa:** 1) desperdício (3 ou mais cliques e zero conversão,
  irrelevante → negativa); 2) achados (termo que converte e não é palavra-chave → adicionar);
  3) desvio (correspondência puxando sentido errado → apertar).
- **Negativas:** negativa ampla exige todas as palavras ("consulta gratuita" não bloqueia só "gratuita").
  Não exagere: negative o claramente errado, não o incerto.
- **Lances por volume de conversões (por campanha, por mês):** de 0 a 15 → CPC manual ou maximizar
  conversões · de 15 a 30 → maximizar conversões · mais de 30 estáveis → CPA desejado perto do real.
  Mude metas em passos de 10% a 15% e espere de 1 a 2 semanas.
- **Índice de qualidade:** baixo = pagar mais pela mesma posição. Corrija o anúncio ou a página antes de subir o lance.
- **Diagnóstico:** parcela de impressões perdida por **orçamento** (falta verba) × por **classificação**
  (anúncio ou página fracos) são problemas diferentes.

## 6. Frequência das checagens
| O quê | Frequência |
|---|---|
| Gasto, reprovações, rastreamento | Diário (dias úteis), só fatos |
| Decisão por conta (checagem semanal) | Semanal |
| Fadiga de criativo | Semanal (a cada 2 ou 3 dias em contas com verba alta) |
| Termos de pesquisa (Google) | Semanal |
| Plano de mídia e custo-alvo | Mensal |
Checar demais gera alterações demais, e alteração demais piora o resultado.

## 7. Relatório de sexta (um minuto de leitura)
1. **Resultado × meta:** uma linha por conta (🟢 🟡 🔴).
2. **O que mudou e por quê:** os 2 ou 3 maiores movimentos, com a causa provável e a confiança.
3. **Decisões para a próxima semana:** MANTER, CORRIGIR, TESTAR ou INVESTIGAR, uma linha cada.
4. **Fatos · Hipóteses · Faltando.**
Deixe de fora números que ninguém vai usar para decidir algo.
