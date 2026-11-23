# Clientes

Uma pasta por cliente, com o **slug do painel** como nome (ex.: `juliana-annunciato`).

| Cliente | Especialidade | Pasta | Status da ficha |
|---|---|---|---|
| Dr. José Erasmo | Neurocirurgião | [`jose-erasmo/`](jose-erasmo/) | ⏳ aguardando informações |
| Dra. Caroline Skaf | Dermatologia | [`caroline-skaf/`](caroline-skaf/) | ⏳ aguardando informações |
| Dra. Juliana Annunciato | Dermatologia | [`juliana-annunciato/`](juliana-annunciato/) | ⏳ aguardando informações |
| WA Concept | Extensão de cílios | [`wa-concept/`](wa-concept/) | ⏳ aguardando informações |
| Straut | Perfil da própria Straut | [`straut/`](straut/) | ⏳ aguardando informações |

> As fichas foram criadas com os dados básicos do painel. O Guilherme vai completá-las com as
> informações que estão no computador dele (pasta `clientes/` do Straut Brain).

## O que tem em cada pasta

| Arquivo | Conteúdo | Quem mantém |
|---|---|---|
| `perfil.md` | Dados básicos, objetivos, público, serviços, restrições | Gestor |
| `posicionamento-e-tom.md` | Posicionamento, pilares, tom de voz, palavras a usar ou evitar | Estratégia (com aprovação) |
| `identidade-visual.md` | Cores, fontes, kit de marca e modelos do Canva | Design / Guilherme |
| `textos-aprovados.md` | Exemplos de textos aprovados pela cliente | Copy |
| `desempenho.md` | Resumo de métricas, recordes, melhores horários e formatos | Analista |
| `atendimento.md` | Contador semanal da Lari e resumos de interações | Lari |
| `historico.md` | Linha do tempo de decisões, feedbacks e aprendizados | Gestor, Samuel, Revisor |
| `estrategia/` | Diagnósticos e pautas mensais | Estratégia |
| `calendario/` | Calendário editorial de cada mês | Gestor |
| `relatorios/` | Relatórios mensais | Analista |
| `sugestoes/` | Sugestões de reels viral e stories | Social Media |

As subpastas são criadas quando o primeiro arquivo for gravado.

## Cliente nova
1. Cadastre a cliente no painel (o slug vem de lá).
2. Copie `_modelo/` para `clientes/<slug>/` e preencha o `perfil.md`.
3. Crie o bot "Gestor · \<Nome\>" no OpenBot (veja `openbot/README.md`).
4. A Estratégia faz o diagnóstico e o posicionamento → aprovação do Guilherme.
5. O Design monta o kit de marca e os modelos no Canva → aprovação do Guilherme.
6. Atualize a tabela acima e `equipe/README.md`.

## Cliente que saiu
Não apague a pasta. Mude o status na tabela para "inativa" e desative o Gestor no OpenBot.
