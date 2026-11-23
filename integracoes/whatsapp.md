# WhatsApp: canal da Lari

> **Status: 🚧 a definir.** A documentação pública do OpenBot cita Slack, Microsoft Teams e mensagem
> de texto como canais, mas **não cita WhatsApp**. É preciso confirmar com o OpenBot ou ligar o WhatsApp
> por uma integração (MCP ou webhook).

## Números
| Uso | Número |
|---|---|
| Lari ↔ clientes | Número comercial da Straut (_a definir_) |
| Lari → Guilherme (escalonamentos) | WhatsApp pessoal do Guilherme (guardado como segredo no OpenBot, não aqui) |

## Opções de integração
1. **Integração nativa do OpenBot**, se existir. Verificar primeiro.
2. **WhatsApp Business Platform (API oficial da Meta)** por um provedor (ex.: Twilio, 360dialog,
   Z-API), ligado ao OpenBot por MCP ou webhook. É o caminho mais estável e sem risco de bloqueio do número.
3. Evite soluções "não oficiais" que simulam o WhatsApp Web: elas podem levar ao **bloqueio do número**.

## Regras da API oficial que afetam a Lari
- **Janela de 24 horas:** a Lari pode responder livremente até 24 horas depois da última mensagem da cliente.
- **Fora da janela**, toda mensagem iniciada pela Straut precisa usar um **modelo aprovado pela Meta**:
  - Categoria **Utilidade**: avisos (conteúdos para aprovar, lembrete de gravação).
  - Categoria **Marketing**: sugestões de conteúdo e comemoração de recorde (provavelmente). O custo é diferente.
- Cadastrar os modelos com antecedência. Rascunhos:

| Nome | Categoria | Texto |
|---|---|---|
| `aprovacao_pendente` | Utilidade | "Oi, {{1}}! Tem {{2}} conteúdos esperando sua aprovação no painel: {{3}}. Qualquer coisa, é só me chamar! 😊" |
| `lembrete_gravacao` | Utilidade | "Oi, {{1}}! Passando pra lembrar da nossa gravação {{2}}, às {{3}}. Até lá! ✨" |
| `recorde_post` | Marketing | "{{1}}, notícia boa! 🎉 Seu post \"{{2}}\" bateu recorde: {{3}}. O público adorou!" |
| `sugestao_semana` | Marketing | "Oi, {{1}}! Separei uma ideia de conteúdo pra essa semana: {{2}}. O que acha? 😊" |
