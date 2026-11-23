# GitHub: como os bots acessam este repositório

## Acesso
- Repositório **privado** `straut-sm/straut-team`.
- Os bots usam um **token de acesso fino** (fine-grained personal access token) do GitHub:
  - Repositório: **só** `straut-sm/straut-team`.
  - Permissão: **Contents: Read and write** (nada mais).
  - Validade: 90 dias, com renovação lembrada pelo Samuel.
- O token fica guardado como **segredo no OpenBot**. Nunca no repositório, nunca no chat.

## Configuração no computador de cada bot (workspace do OpenBot)
```bash
git clone https://github.com/straut-sm/straut-team.git
cd straut-team
git config user.name "<Nome do bot> (bot Straut)"
git config user.email "<o e-mail noreply da conta do GitHub>"
```

## Ciclo de trabalho
```bash
git pull --rebase            # antes de ler e antes de editar
# ... edita os arquivos da sua área ...
git add <arquivos>
git commit -m "[Bot] cliente: o que mudou"
git push                     # se recusar: git pull --rebase e push de novo (nunca --force)
```

## Claude (Straut Brain)
As conversas do Claude acessam o mesmo repositório pela conexão com o GitHub e seguem as mesmas regras
(`equipe/regras-gerais.md`).
