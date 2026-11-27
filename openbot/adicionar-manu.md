# Mensagem para o OpenBot: criar a Manu

Cole o texto abaixo na conversa com o assistente do OpenBot (ou com o Samuel).

```
Olá! Vamos adicionar uma nova integrante ao time: a MANU, diretora criativa da Straut. Antes de
começar, rode git pull em ~/straut-team. Tudo já está no repositório.

1. LEIA
• equipe/manu-diretora-criativa.md: a ficha completa da Manu
• equipe/regras-gerais.md, seção 2: a hierarquia nova
• equipe/README.md: o Fluxo 9 (direção criativa) e a tabela de handoff
• gestao/decisoes.md: a decisão de 2026-11-27

2. O QUE MUDA
• HIERARQUIA: Samuel (operação), Manu (criação visual) e Lari (atendimento) ficam no MESMO NÍVEL,
  logo abaixo de mim. Os três conversam entre si e recebem orientações direto de mim aqui no app.
  Os demais bots levam pedidos ao Samuel (operação) ou à Manu (assuntos visuais).
• A MANU cuida do guia visual de cada cliente (aprovado só por mim; a cliente não aprova), do banco
  de referências, da direção de foto e de gravação, dos prompts visuais otimizados e do olhar de feed.
  Objetivo: conteúdos mais bonitos e AUTÊNTICOS. Nunca gera nem pede imagens de IA de pessoas,
  pacientes ou resultados.
• O DESIGN passa a ser o designer: executa no Canva o guia visual da Manu.

3. CRIE A MANU
• Nome: Manu
• Modelo: claude-opus-5-5 (effort high, se houver a opção)
• Instruções: o texto da seção "11. Manu · Diretora criativa" de openbot/prompts.md, trocando
  "<cole aqui o BLOCO COMUM>" pelo BLOCO COMUM do mesmo arquivo.
• Handoff: a Manu repassa para TODOS. TODOS os bots passam a poder repassar para a Manu.
• Ferramentas: Instagram de pesquisa (SÓ LEITURA), pesquisa na web, Canva (só leitura), API dos bots
  do painel (só leitura, X-Bot: manu) e o repositório. Ela precisa VER imagens: me diga se o OpenBot
  permite isso.
• Primeira configuração: clonar o repositório em ~/straut-team, git config com o nome
  "Manu (bot Straut)" e um teste: ela explica com as próprias palavras o que faz, o que pode acessar
  e o que precisa do meu ok.

4. ATUALIZE OS OUTROS BOTS
Troque as instruções de SAMUEL, LARI e DESIGN pelos textos novos das seções 1, 9 e 7 de
openbot/prompts.md (com o BLOCO COMUM). Os demais bots não mudam de texto: eles leem as regras novas
no repositório a cada tarefa.

5. ROTINA NOVA
Crie a rotina 18 de openbot/rotinas.md (Manu · quinta 10h · referências da semana + olhar de feed),
DESATIVADA até eu liberar.

6. PRIMEIRA TAREFA DA MANU (depois do teste)
Montar o rascunho do guia visual da WA Concept em clientes/wa-concept/identidade-visual.md,
partindo do que já existe ali, e me mandar para aprovação.

7. AO TERMINAR, me mande:
✅ o que foi feito · ⚠️ o que não foi possível e por quê · ❓ dúvidas para eu decidir.
```
