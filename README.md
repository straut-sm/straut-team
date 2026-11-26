# Straut Team

Base de conhecimento e instruções do **time de bots da Straut Marketing**.

> 🔒 **Repositório privado.** Contém informações das clientes. Nunca torne este repositório público
> e nunca grave aqui senhas, chaves ou tokens.

## Para que serve

Este repositório é o **ponto de contato entre todas as IAs da Straut**:

- os bots do **OpenBot** (Samuel, Gestores, time de produção e Lari);
- as conversas do **Claude** (Straut Brain · App e Straut Brain · Clientes).

Todos leem e escrevem aqui. O que um bot aprende e não grava aqui se perde: **sincronizar com o
repositório é obrigatório** (veja [`equipe/regras-gerais.md`](equipe/regras-gerais.md)).

## Estrutura

```
equipe/              Quem é quem: regras gerais e as instruções de cada bot
  regras-gerais.md   ← todo bot lê antes de qualquer tarefa
  README.md          Organograma, fluxos e quem fala com quem
  samuel-gerente.md, gestor-de-cliente.md, estrategia.md, analista.md,
  social-media.md, copy.md, design.md, revisor.md, lari-atendimento.md, trafego.md

clientes/            Uma pasta por cliente (perfil, posicionamento, identidade visual...)
  _modelo/           Modelo para cadastrar uma cliente nova

straut/              Sobre a Straut: serviços, processos, painel
regras-do-setor/     Regras de publicidade (CFM para médicos, regras gerais para os demais)
modelos/             Formatos padrão: briefing, roteiro, carrossel, relatório, escalonamento...
referencias/         Métodos de marketing adaptados: ganchos, carrosséis, texto sem cara de IA,
                     revisão, pesquisa de público, concorrentes, rotinas seguras
gestao/              Decisões, resumos semanais e registros do Samuel
integracoes/         GitHub, WhatsApp, tráfego, passagem ao Straut Brain
openbot/             Como configurar o time no OpenBot: prompt, modelos de IA, rotinas
```

## Por onde começar

**Se você é um bot:**
1. Rode `git pull` para pegar a versão mais recente.
2. Leia [`equipe/regras-gerais.md`](equipe/regras-gerais.md).
3. Leia a sua ficha em [`equipe/`](equipe/).
4. Para trabalhar com uma cliente, leia a pasta dela em [`clientes/`](clientes/).

**Se você é o Guilherme:** o passo a passo de configuração está em [`openbot/README.md`](openbot/README.md).

## Links

| O quê | Onde |
|---|---|
| Painel da Straut | https://painel.strautmarketing.com |
| Código do painel | `straut-sm/straut-brain` (Straut Brain · App) |
| Instagram de pesquisa | Só leitura: não curtir, seguir, comentar nem mandar mensagem |
