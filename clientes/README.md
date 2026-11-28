# Clientes

Uma pasta por cliente, com o **slug do painel** como nome (ex.: `juliana-annunciato`).

| Cliente | Especialidade | Pasta | Status da ficha |
|---|---|---|---|
| Dr. José Erasmo | Neurocirurgião | [`jose-erasmo/`](jose-erasmo/) | ✅ migrada (2026-11-26) |
| Dra. Caroline Skaf | Dermatologia | [`caroline-skaf/`](caroline-skaf/) | ✅ migrada (2026-11-26) |
| Dra. Juliana Annunciato | Dermatologia | [`juliana-annunciato/`](juliana-annunciato/) | ✅ migrada (2026-11-26) |
| WA Concept | Extensão de cílios | [`wa-concept/`](wa-concept/) | ✅ migrada (2026-11-26) |
| Straut | Perfil da própria Straut | [`straut/`](straut/) | ✅ migrada (2026-11-26) |

> As fichas foram criadas com os dados básicos do painel. O Guilherme vai completá-las com as
> informações que estão no computador dele (pasta `clientes/` do Straut Brain).

## O que tem em cada pasta

| Arquivo | Conteúdo | Quem mantém |
|---|---|---|
| `resumo.md` | **Leia primeiro.** Até ~20 linhas: quem é, público, pilares, tom, proibições e "Quem cuida" | Estratégia ("Quem cuida": Samuel) |
| `perfil.md` | Dados básicos, objetivos, público, serviços, restrições | Estratégia |
| `posicionamento-e-tom.md` | Posicionamento, pilares, tom de voz, palavras a usar ou evitar | Estratégia (com aprovação) |
| `identidade-visual.md` | Cores, fontes, kit de marca e modelos do Canva | Design / Guilherme |
| `textos-aprovados.md` | Exemplos de textos aprovados pela cliente | Copy |
| `desempenho.md` | Resumo de métricas, recordes, melhores horários e formatos | Analista |
| `atendimento.md` | Contador semanal da Lari e resumos de interações | Lari |
| `historico.md` | Linha do tempo de decisões, feedbacks e aprendizados | Samuel, Revisor |
| `estrategia/` | Diagnósticos e pautas mensais | Estratégia |
| `calendario/` | Calendário editorial de cada mês (listas de gravação: Samuel) | Estratégia |
| `relatorios/` | Relatórios mensais | Analista |
| `sugestoes/` | Sugestões de reels viral e stories | Social Media |

> Desde 2026-11-27 não há Gestores de cliente. O que era deles foi para o Samuel e a Estratégia
> (`equipe/gestor-de-cliente.md`). Entradas antigas do histórico e dos calendários que citam o
> "Gestor" ficam como estão: são registro.
| `trafego.md` e `trafego/` | Contas de anúncio, verba, metas, autonomia, planos e relatórios de tráfego pago | Tráfego |

As subpastas são criadas quando o primeiro arquivo for gravado.

## Cliente nova
1. Cadastre a cliente no painel (o slug vem de lá).
2. Copie `_modelo/` para `clientes/<slug>/` e preencha o `perfil.md` e o `resumo.md`.
3. Não há bot por cliente: o Samuel e a Estratégia passam a cuidar dela (seção "Quem cuida" do `resumo.md`).
4. A Estratégia faz o diagnóstico e o posicionamento → aprovação do Guilherme.
5. O Design monta o kit de marca e os modelos no Canva → aprovação do Guilherme.
6. Atualize a tabela acima e `equipe/README.md`.

## Cliente que saiu
Não apague a pasta. Mude o status na tabela para "inativa" e avise o Samuel.
