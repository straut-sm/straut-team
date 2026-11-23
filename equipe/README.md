# Equipe Straut: organograma e fluxos

## Quem é quem

| Bot | Time | Função | Modelo de IA | Fala com |
|---|---|---|---|---|
| **Samuel** | Gestão | Gerente Geral, principal contato do Guilherme | Claude Opus 5.5 | Guilherme, todos os bots |
| **Gestor · \<Cliente\>** | Gestão | Gestor de projeto de uma cliente | Claude Sonnet 5.5 | Samuel, produção, Lari |
| **Estratégia** | Produção | Planejamento: nicho, posicionamento, pautas | Claude Opus 5.5 | Gestores, Analista, Samuel |
| **Analista** | Produção | Dados e BI: desempenho e recordes | Claude Sonnet 5.5 | Gestores, Estratégia, Lari |
| **Social Media** | Produção | Caçador de tendências | Claude Sonnet 5.5 | Gestores, Copy, Lari |
| **Copy** | Produção | Roteirista e redator | Claude Opus 5.5 | Gestores, Design, Revisor |
| **Design** | Produção | Diretor de arte: Canva e painel | Claude Sonnet 5.5 | Gestores, Copy, Revisor |
| **Revisor** | Produção | Garantia de qualidade (diretor de criação) | Claude Opus 5.5 | Gestores, Copy, Design |
| **Lari** | Atendimento | Avisos e relacionamento com as clientes | Claude Sonnet 5.5 | Clientes, Gestores, Samuel, Guilherme |

O motivo de cada modelo está em [`openbot/modelos-de-ia.md`](../openbot/modelos-de-ia.md).

### Gestores de cliente ativos

| Bot | Cliente | Pasta |
|---|---|---|
| Gestor · Dr. José Erasmo | Neurocirurgião | [`clientes/jose-erasmo/`](../clientes/jose-erasmo/) |
| Gestor · Dra. Caroline Skaf | Dermatologia | [`clientes/caroline-skaf/`](../clientes/caroline-skaf/) |
| Gestor · Dra. Juliana Annunciato | Dermatologia | [`clientes/juliana-annunciato/`](../clientes/juliana-annunciato/) |
| Gestor · WA Concept | Extensão de cílios | [`clientes/wa-concept/`](../clientes/wa-concept/) |
| Gestor · Straut | Perfil da própria Straut | [`clientes/straut/`](../clientes/straut/) |

Todos usam a mesma ficha: [`gestor-de-cliente.md`](gestor-de-cliente.md). Só muda a pasta da cliente.

## Fluxo 1: conteúdo do mês

```
Dia 15  Estratégia   → pauta do mês seguinte para cada cliente (com base no relatório do Analista)
Dia 20  Samuel       → aciona os Gestores para montar os calendários
        Gestor       → monta o calendário (datas + formatos + pautas) → Samuel pede ok ao Guilherme
        Gestor       → pede os roteiros e textos ao Copy (briefing: modelos/briefing-de-demanda.md)
        Copy         → escreve → Revisor
        Revisor      → aprova ou devolve com ajustes (no máximo 2 rodadas, depois escala ao Gestor)
        Gestor       → cria os blocos no painel (status "em_producao")
        Samuel       → pede ok do lote ao Guilherme → blocos vão para "aguardando_aprovacao"
        Lari         → avisa a cliente que há conteúdos para aprovar
```

## Fluxo 2: carrossel e capa

```
Gestor → Copy (texto slide a slide) → Design (arte no modelo do Canva da cliente)
       → Revisor (texto + arte) → Design sobe as imagens no bloco do painel
       → Gestor confere → (ok do Guilherme na fase de testes) → aguardando_aprovacao → Lari avisa
```

## Fluxo 3: reels

```
Roteiro aprovado pela cliente → gravação presencial (equipe humana) → edição (equipe humana)
→ Design faz a capa → Revisor → vídeo + capa no bloco → aprovação da cliente → postagem
```

Gravação e edição de vídeo são feitas por pessoas, não pelos bots.

## Fluxo 4: ajuste sugerido pela cliente

```
Cliente sugere ajuste no painel → Gestor vê no painel → encaminha a quem fez (Copy ou Design)
→ Revisor → Gestor avisa o Samuel → Guilherme aceita ou recusa a sugestão no painel
```

## Fluxo 5: atendimento (Lari)

```
Cliente manda mensagem no WhatsApp
  ├── Dúvida simples (posts da semana, status, links) → Lari responde com dados do painel ou do Gestor
  ├── Pedido de gravação → Lari coleta datas possíveis → escala ao Guilherme → confirma com a cliente
  └── Mensagem longa, reclamação, dinheiro, contrato ou algo que precise de ação humana
        → Lari responde "recebi, já te retorno" → manda ao WhatsApp do Guilherme:
          natureza + resumo + sugestão de resposta → Guilherme aprova ou edita → Lari envia
```

## Fluxo 6: avisos e sugestões

```
Analista detecta recorde ─────────────┐
Painel: conteúdos aguardando aprovação ┼→ Lari → cliente  (até 3 avisos por semana)
Social Media: viral + stories da semana → Gestor valida → Lari → cliente  (até 2 sugestões por semana)
```

## Quem pode repassar trabalho para quem (handoff no OpenBot)

| Bot | Repassa para |
|---|---|
| Samuel | Todos |
| Gestores | Samuel, Estratégia, Analista, Social Media, Copy, Design, Revisor, Lari |
| Estratégia | Samuel, Gestores, Analista |
| Analista | Samuel, Gestores, Estratégia, Lari |
| Social Media | Gestores, Copy, Lari |
| Copy | Gestores, Design, Revisor |
| Design | Gestores, Revisor |
| Revisor | Gestores, Copy, Design |
| Lari | Samuel, Gestores |
