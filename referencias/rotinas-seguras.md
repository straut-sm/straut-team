# Rotinas seguras

> Referência para o Samuel e para todos os bots com rotinas (`openbot/rotinas.md`).
> Uma rotina automática que não sabe **quando agir, o que já fez e quando parar** é um risco, não uma ajuda.

## As 9 partes de uma rotina
Toda rotina do time precisa ter estas partes definidas:

| Parte | O que define |
|---|---|
| **Quando checa** | O horário ou o gatilho (ex.: segunda às 9h) |
| **Quando age** | A condição para fazer algo. **A maioria das execuções boas termina em "checado, nada a fazer".** |
| **Objetivo** | O resultado que a rotina protege |
| **Usa** | Quais fichas, referências e ferramentas |
| **Passos** | O que faz, em ordem |
| **Checagem antes de agir** | A verificação que evita agir em cima de erro, dado incompleto ou coincidência |
| **Memória (não repetir)** | O que ela lembra entre uma execução e outra para não repetir, não mandar duas vezes e não cobrar de novo |
| **Parada** | Quando pula, para, chama um humano ou se desliga, e o que faz se der erro |
| **Saída** | Onde o resultado vai: arquivo, mensagem, painel, mLabs |

**Checar não é agir.** Ex.: a rotina de avisos da Lari **checa** duas vezes por dia, mas só **age**
se houver conteúdo parado há mais de 48 horas, se o limite semanal permitir e se a conversa estiver
livre.

## Frequência certa
Combine a frequência com a velocidade real do que está sendo medido:

| O quê | Frequência | Por quê |
|---|---|---|
| Recordes de desempenho | Semanal | Números de um dia oscilam demais |
| Relatório de métricas | Mensal | Tendência só aparece no mês |
| Tendências e virais | Semanal | O que viraliza dura dias |
| Concorrentes | Trimestral | Posicionamento muda devagar |
| Posts do dia, aprovações pendentes | Diário | O prazo é curto |

Rotina frequente demais gera trabalho inútil, gasta dinheiro de API e ensina todo mundo a ignorar o resultado.

## Dois níveis de ação

| Nível | Exemplos | Pode fazer sozinho? |
|---|---|---|
| **1. Seguro** | Ler, analisar, comparar, rascunhar, preparar para revisão, gravar no repositório | ✅ Sim |
| **2. Com autorização** | **Enviar** mensagem para cliente, **publicar ou agendar** post, **gastar**, **apagar**, mudar configurações | Só com o ok do Guilherme **ou** dentro de uma regra já autorizada, com limites claros (ex.: os limites semanais da Lari) |

## Sempre para um humano (mesmo com autorização)
- Reclamação, crise ou assunto delicado (médico, jurídico, financeiro).
- Qualquer coisa que pareça ferir o CFM.
- Mudança em algo que a cliente já aprovou.
- Números muito fora do normal (pode ser erro de dado): avise, não "corrija".
- Qualquer ação que apague dados ou fale com muitas clientes ao mesmo tempo fora da rotina.

## Memória entre execuções
A memória fica **no repositório** (nunca só na cabeça do bot, que esquece ao reiniciar):

| Rotina | Onde fica a memória |
|---|---|
| Avisos, sugestões e boa semana da Lari | `clientes/<slug>/atendimento.md` (contador, últimas mensagens, casos em aberto) |
| Sugestões do Social Media | `clientes/<slug>/sugestoes/` (status: pendente, aprovada, enviada) |
| Recordes do Analista | `clientes/<slug>/desempenho.md` (tabela de recordes: não avisar duas vezes o mesmo post) |
| Posts do dia do Samuel | Comentário "Agendado no mLabs" no bloco + `gestao/` |
| Demais rotinas | `gestao/rotinas/registro.md` (data, rotina, resultado em uma linha) |

Padrões:
- **Marca d'água:** processe só o que é novo desde a última execução.
- **Lista de já feitos:** antes de agir sobre um item, veja se ele já foi tratado.
- **Intervalo de descanso:** não contatar a mesma cliente pelo mesmo motivo dentro do intervalo
  (ex.: o mesmo aviso de aprovação só a cada 48 horas).

**Nada de dados pessoais** na memória ou nos registros.

## Botão de pausa: "PAUSA GERAL"
- Se o Guilherme escrever **"PAUSA GERAL"** para o Samuel, **todas as rotinas param**. O Samuel
  desativa as rotinas no OpenBot e registra a pausa em `gestao/decisoes.md`.
- Nenhum bot envia mensagem para cliente, agenda post ou mexe no painel até o Guilherme escrever
  **"RETOMAR"**.
- O Guilherme também pode pausar uma rotina só ("pausa a rotina de avisos da Lari").

## Em caso de erro
- Erro de ferramenta (painel, mLabs, GitHub fora do ar): **não insista em loop**. Tente de novo uma
  vez e, se falhar, registre e avise o Samuel.
- Dado estranho ou incompleto: não aja. Avise.
- O OpenBot desliga sozinho uma rotina que falha 10 vezes seguidas. O Samuel deve notar e avisar o Guilherme.

## Checklist antes de ativar uma rotina
- [ ] Cada ação classificada em nível 1 (seguro) ou 2 (com autorização)
- [ ] Ações de nível 2 só com ok ou dentro de limites já autorizados
- [ ] Rotinas de envio checam os limites semanais e a regra de não interromper
- [ ] Memória definida (onde fica e o que guarda)
- [ ] Casos que sempre vão para um humano estão encaminhados
- [ ] Ela obedece à "PAUSA GERAL"
