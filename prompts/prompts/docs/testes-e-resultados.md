# Testes e resultados — IA de Apoio ao Atendimento

## 1. Objetivo dos testes

Avaliar a capacidade do prompt de analisar reclamações fictícias, identificar o problema apresentado e sugerir uma classificação adequada para o atendimento.

Foram utilizadas cinco mensagens fictícias, com diferentes níveis de impacto e complexidade.

A segunda rodada de testes foi realizada com a versão 3 do prompt, que passou a considerar os seguintes critérios:

- Categoria da ocorrência.
- Resumo do problema.
- Prioridade.
- Justificativa da prioridade.
- Urgência.
- Justificativa da urgência.
- Sentimento predominante.
- Setor responsável.
- Prazo sugerido para primeiro retorno.
- Resposta sugerida ao cliente.
- Necessidade de avaliação humana.

## 2. Resultados da primeira versão (V1)

- **Teste 1 — Consulta sobre estoque:** prioridade esperada baixa; resultado da IA baixo. Avaliação: correto.
- **Teste 2 — Atraso no pedido:** prioridade esperada média; resultado da IA médio. Avaliação: correto.
- **Teste 3 — Cobrança duplicada:** prioridade esperada alta; resultado da IA alto. Avaliação: correto.
- **Teste 4 — Problema de acesso:** prioridade esperada média; resultado da IA alto. Avaliação: parcialmente correto.
- **Teste 5 — Serviço não cumprido:** prioridade esperada alta; resultado da IA alto. Avaliação: correto.

**Resultado:** 4 das 5 classificações de prioridade corresponderam às expectativas iniciais.

## 3. Resultados da segunda versão (V3)

### Teste 1 — Consulta sobre estoque

- Prioridade: baixa.
- Urgência: baixa.
- Setor: comercial.
- Avaliação humana: não.

**Avaliação:** correto. A IA identificou uma solicitação de informação, sem prejuízo ou necessidade de atendimento imediato.

### Teste 2 — Atraso no pedido

- Prioridade: média.
- Urgência: normal.
- Setor: logística.
- Avaliação humana: sim.

**Avaliação:** correto. A IA identificou o descumprimento do prazo de postagem e encaminhou a ocorrência para o setor responsável verificar o pedido.

### Teste 3 — Cobrança duplicada

- Prioridade: alta.
- Urgência: alta.
- Setor: financeiro.
- Avaliação humana: sim.

**Avaliação:** correto. A IA identificou o possível prejuízo financeiro recorrente e considerou as quatro tentativas anteriores de resolução.

### Teste 4 — Problema de acesso

- Prioridade: alta.
- Urgência: alta.
- Setor: suporte técnico.
- Avaliação humana: sim.

**Avaliação:** parcialmente correto. A IA identificou corretamente o problema técnico, o setor responsável e a necessidade de avaliação humana.

Entretanto, classificou a prioridade como alta sem confirmar o impacto real da indisponibilidade do painel. A informação de que o cliente precisa acessar o sistema imediatamente indica urgência percebida, mas não comprova, isoladamente, um prejuízo significativo.

### Teste 5 — Serviço contratado e não cumprido

- Prioridade: alta.
- Urgência: alta.
- Setor: atendimento.
- Avaliação humana: sim.

**Avaliação:** parcialmente correto. A prioridade alta é justificável pelo pagamento antecipado e pelo possível descumprimento do serviço contratado.

Porém, a IA considerou a ameaça de reclamação no Procon e o prazo exigido pelo cliente como elementos suficientes para classificar a urgência como alta. É necessário distinguir a insatisfação e o prazo solicitado pelo cliente da existência de um risco operacional imediato.

## 4. Comparação entre V1 e V3

A versão 3 ampliou a capacidade de análise ao incluir urgência, setor responsável e avaliação humana.

Na primeira versão, o foco estava principalmente na identificação da categoria, prioridade e sentimento.

Na terceira versão, a IA passou a apresentar informações mais úteis para a organização do atendimento e para o encaminhamento das ocorrências.

Os testes também demonstraram que ainda é necessário aprimorar os critérios de prioridade e urgência, especialmente em situações nas quais faltam informações sobre o impacto real do problema.

## 5. Oportunidades de melhoria identificadas

### Melhoria 1 — Diferenciar indisponibilidade de serviço e impacto real (Teste 4)

A IA deve verificar se o acesso bloqueado impede uma atividade essencial do cliente ou se representa uma dificuldade que pode ser resolvida sem prejuízo significativo.

Sugestões:
- Considerar prioridade média quando o cliente não consegue acessar a conta, mas não há informação suficiente sobre o impacto.
- Considerar prioridade alta quando a indisponibilidade impede uma atividade essencial ou provoca prejuízo significativo.
- Considerar urgência alta quando existe uma necessidade concreta de acesso em curto prazo.
- Quando o impacto não estiver claro, solicitar informações adicionais ou encaminhar para avaliação humana.

**Informação adicional que poderia ser solicitada:** O painel é essencial para alguma atividade que precisa ser realizada agora? A impossibilidade de acesso está causando algum prejuízo ou impedindo uma operação importante?

### Melhoria 2 — Não confundir prazo exigido com urgência operacional (Teste 5)

A IA deve registrar o prazo solicitado pelo cliente sem assumir que ele representa automaticamente uma emergência.

Sugestões:
- Manter prioridade alta quando houver pagamento antecipado e possível descumprimento do serviço contratado.
- Não classificar a urgência como alta somente porque o cliente exige uma solução para hoje.
- Considerar urgência alta quando houver prazo contratual ou legal próximo, consequência concreta ou risco de agravamento.
- Encaminhar para avaliação humana quando houver necessidade de verificar contrato, pagamento, reembolso ou compensação.
- Nunca prometer uma solução ou prazo que não tenha sido confirmado pela empresa.

**Informação adicional que poderia ser solicitada:** Existe uma data contratual para a prestação do serviço? O descumprimento está causando algum prejuízo imediato ao cliente?

## 6. Próximas melhorias para a versão 4

- [ ] Refinar os critérios de prioridade e urgência.
- [ ] Diferenciar o prazo solicitado pelo cliente de um prazo operacional real.
- [ ] Incluir perguntas para identificar o impacto da ocorrência.
- [ ] Orientar a IA a sinalizar informações insuficientes.
- [ ] Repetir os cinco testes para comparar os resultados.
- [ ] Criar novos testes com situações mais complexas.
- [ ] Avaliar a consistência das respostas e dos encaminhamentos.

## 7. Conclusão

Os testes demonstraram uma evolução entre a primeira e a terceira versão do prompt.

A versão 3 apresenta uma análise mais completa das manifestações dos clientes, mas ainda precisa de ajustes para evitar classificações baseadas apenas na linguagem utilizada pelo consumidor, sem considerar o impacto real da ocorrência.

O próximo passo será aprimorar os critérios de decisão e validar a nova versão com os mesmos casos de teste, mantendo as mensagens originais para permitir uma comparação justa.

## 8. Observação

Os resultados representam testes experimentais realizados com mensagens fictícias. As classificações esperadas são referências definidas para este exercício e devem ser adaptadas às regras de negócio, aos contratos e aos níveis de serviço de cada empresa.

Os prazos sugeridos pelo prompt são referências para triagem e não representam compromissos reais de atendimento.
