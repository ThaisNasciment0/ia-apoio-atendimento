# Testes e Resultados — IA de Apoio ao Atendimento ao Cliente

## 1. Objetivo dos testes

Avaliar o comportamento do prompt de IA desenvolvido para apoiar a triagem de reclamações e manifestações de clientes.

Os testes buscam verificar se a IA consegue:

- Identificar corretamente a categoria do problema.
- Resumir a manifestação do cliente.
- Classificar prioridade e urgência de forma independente.
- Identificar o sentimento predominante.
- Sugerir o setor responsável pelo atendimento.
- Elaborar uma resposta inicial adequada.
- Identificar situações que necessitam de avaliação humana.
- Solicitar informações adicionais relevantes.

Foram utilizados dez cenários fictícios de atendimento, divididos em duas rodadas de testes.

## 2. Primeira rodada — Testes iniciais

Foram utilizados cinco exemplos de reclamações para avaliar a primeira versão do prompt.

### Resultados da V1

| Teste | Cenário | Prioridade esperada | Resultado | Avaliação |
|---|---|---|---|---|
| 1 | Consulta sobre estoque | Baixa | Baixa | Correto |
| 2 | Atraso no pedido | Média | Média | Correto |
| 3 | Cobrança duplicada | Alta | Alta | Correto |
| 4 | Problema de acesso à conta | Média | Alta | Parcialmente correto |
| 5 | Descumprimento contratual | Alta | Alta | Correto |

**Resultado:** 4 de 5 classificações corresponderam às expectativas iniciais.

O principal problema identificado foi a classificação do teste 4. A IA atribuiu prioridade alta a uma dificuldade de acesso sem evidências suficientes de prejuízo significativo ou impedimento de uma atividade essencial.

Esse resultado demonstrou a necessidade de critérios mais claros para diferenciar a gravidade do problema de sua urgência.

## 3. Segunda versão — V3

A partir dos resultados iniciais, o prompt foi aprimorado.

As principais mudanças foram:

- Separação entre prioridade e urgência.
- Inclusão de justificativas para as classificações.
- Definição de critérios para avaliação humana.
- Identificação de setores responsáveis e setores de apoio.
- Inclusão de prazos sugeridos para o primeiro retorno.
- Orientações para evitar promessas de solução, reembolso ou prazos não confirmados.

### Resultados da V3

Os cinco casos originais foram testados novamente.

Os principais pontos identificados foram:

- Testes 1, 2, 3 e 5 apresentaram classificações coerentes em seus aspectos principais.
- No teste 4, a dificuldade de acesso continuou sendo classificada com prioridade alta, embora não houvesse evidência de impacto significativo.
- No teste 5, a ameaça de registrar reclamação no Procon influenciou a percepção de urgência, sem que houvesse necessariamente uma consequência imediata comprovada.

Esses resultados demonstraram que a separação entre prioridade e urgência precisava ser acompanhada de regras mais específicas.

## 4. Terceira versão — V4

A V4 foi desenvolvida para corrigir os problemas identificados na V3.

### Principais melhorias

**Critérios de prioridade**

Foram definidos critérios mais claros para classificar manifestações como baixa, média ou alta, considerando o impacto sobre o cliente, prejuízos financeiros, recorrência e riscos envolvidos.

**Critérios de urgência**

Foram estabelecidas regras para diferenciar situações que exigem intervenção imediata, alta, normal ou baixa.

**Regras para situações específicas**

- Problemas de acesso não devem receber prioridade alta automaticamente.
- A solicitação de resolução no mesmo dia não determina, sozinha, urgência alta.
- A ameaça de procurar o Procon não determina, por si só, urgência alta.
- Cobranças recorrentes e prejuízos financeiros significativos devem receber atenção diferenciada.
- Suspeitas de fraude, invasão ou exposição de dados exigem encaminhamento prioritário para avaliação humana.

## 5. Resultados da V4 — Primeira rodada

Os cinco cenários originais foram novamente testados.

| Teste | Cenário | Prioridade | Urgência | Avaliação |
|---|---|---|---|---|
| 1 | Consulta sobre estoque | Baixa | Baixa | Coerente |
| 2 | Atraso no pedido | Média | Normal | Coerente |
| 3 | Cobrança duplicada | Alta | Alta | Coerente |
| 4 | Problema de acesso à conta | Média | Normal | Coerente |
| 5 | Descumprimento contratual | Alta | Normal | Coerente |

**Resultado:** 5 de 5 cenários apresentaram classificações coerentes com os critérios definidos.

Dois pontos de atenção foram identificados:

- No teste 4, o prazo de até três dias úteis pode ser lento caso o cliente esteja completamente impedido de utilizar um serviço importante.
- No teste 5, a solicitação de resolução no mesmo dia precisa ser considerada na comunicação com o cliente, mesmo quando a urgência não justifica uma classificação alta.

## 6. Segunda rodada de validação — Novos cenários

Após os resultados positivos da primeira rodada, foram criados cinco novos cenários para verificar se a V4 conseguiria interpretar situações diferentes das utilizadas nos testes iniciais.

### Teste 6 — Entrega incompleta

**Resultado da IA:**
- Prioridade: Média.
- Urgência: Normal.
- Setor responsável: Logística.
- Avaliação humana: Sim.

**Avaliação:** Classificação coerente. A IA identificou a divergência na entrega e considerou a possibilidade de cobrança integral sem presumir que houve irregularidade.

**Ponto de atenção:** O prazo de três dias úteis para o primeiro retorno pode ser longo, dependendo do contexto da ocorrência.

### Teste 7 — Suspeita de acesso não autorizado

**Resultado da IA:**
- Prioridade: Alta.
- Urgência: Imediata.
- Setor responsável: Segurança.
- Avaliação humana: Sim.

**Avaliação:** Classificação coerente. A IA identificou o risco potencial à segurança da conta e dos dados pessoais, diferenciando o caso de uma simples dificuldade de acesso.

**Ponto de atenção:** A resposta sugerida afirmou que a ocorrência já havia sido encaminhada. A IA deve sugerir o encaminhamento, sem afirmar que uma ação foi realizada quando isso ainda depende de uma pessoa ou integração.

### Teste 8 — Falha recorrente no serviço

**Resultado da IA:**
- Prioridade: Alta.
- Urgência: Alta.
- Setor responsável: Suporte técnico.
- Avaliação humana: Sim.

**Avaliação:** A prioridade alta foi considerada coerente devido à recorrência das falhas e ao impacto na rotina profissional do cliente.

A urgência alta merece ressalva. O relato não esclarece se o serviço está indisponível naquele momento ou se existe uma atividade essencial impedida. A urgência normal também seria defensável com as informações disponíveis.

**Ponto de atenção:** A recorrência aumenta a relevância do problema, mas não deve determinar automaticamente uma urgência alta.

### Teste 9 — Insatisfação com a experiência de compra

**Resultado da IA:**
- Prioridade: Baixa.
- Urgência: Baixa.
- Setor responsável: Atendimento.
- Avaliação humana: Não.

**Avaliação:** Classificação coerente. A IA identificou uma manifestação de insatisfação sem prejuízo financeiro ou impedimento de compra relatado.

Também reconheceu que o feedback pode contribuir para melhorias na experiência de outros consumidores.

**Ponto de atenção:** A resposta sugerida deve evitar afirmar que o feedback já foi encaminhado, caso a IA esteja apenas realizando a triagem.

### Teste 10 — Dúvida sobre cobrança

**Resultado da IA:**
- Prioridade: Média.
- Urgência: Normal.
- Setor responsável: Financeiro.
- Avaliação humana: Sim.

**Avaliação:** Classificação coerente. A IA reconheceu a necessidade de investigação financeira sem presumir que houve cobrança indevida.

A solicitação de informações sobre a fatura e as condições contratuais foi adequada.

## 7. Comparativo geral das versões

| Etapa | Resultado observado |
|---|---|
| V1 | 4 de 5 classificações coerentes |
| V3 | Melhor estrutura, mas com dificuldades na diferenciação entre prioridade e urgência |
| V4 — Primeira rodada | 5 de 5 classificações coerentes |
| V4 — Segunda rodada | 4 coerentes e 1 com ressalva na urgência |

Os resultados indicam uma evolução na capacidade do prompt de interpretar diferentes manifestações e aplicar critérios mais consistentes.

A segunda rodada também permitiu identificar situações que merecem novos ajustes, principalmente na análise de urgência e na redação das respostas sugeridas.

## 8. Aprendizados identificados

Durante os dez testes, foram identificados os seguintes aprendizados:

1. Prioridade e urgência precisam ser avaliadas separadamente.
2. A intensidade do sentimento do cliente não determina automaticamente a prioridade.
3. A recorrência de um problema deve ser considerada, mas não significa necessariamente urgência imediata.
4. Ameaças de reclamação em órgãos de defesa do consumidor não devem determinar sozinhas a urgência.
5. Suspeitas de fraude, invasão ou exposição de dados exigem tratamento prioritário.
6. A IA não deve presumir cobranças indevidas sem investigação.
7. A avaliação humana é importante em situações financeiras, contratuais e de segurança.
8. A resposta sugerida não deve afirmar que uma ação já foi realizada quando a IA apenas recomenda seu encaminhamento.
9. Os prazos de primeiro retorno precisam ser compatíveis com o impacto da ocorrência, e não apenas com sua classificação de prioridade.

## 9. Limitações dos testes

Os dez testes foram realizados com mensagens fictícias e representam uma etapa inicial de validação.

Os resultados não comprovam a precisão do sistema em situações reais de atendimento.

Ainda será necessário avaliar:

- Mensagens mais curtas e pouco detalhadas.
- Clientes que apresentam várias reclamações na mesma mensagem.
- Informações contraditórias ou incompletas.
- Reclamações com diferentes níveis de impacto.
- Variações de linguagem, erros de escrita e mensagens informais.
- Comportamento do prompt em diferentes modelos de IA.
- Consistência dos resultados em testes repetidos.

Também será necessário validar os prazos sugeridos conforme as regras e os níveis de serviço de cada empresa.

## 10. Próximas etapas do projeto

1. Revisar os pontos de atenção identificados na segunda rodada.
2. Avaliar a necessidade de ajustes no Prompt V4.
3. Ampliar a quantidade e a variedade de mensagens de teste.
4. Estruturar a saída da IA em formato JSON para facilitar integrações.
5. Iniciar a construção do fluxo de automação no n8n.
6. Testar a integração entre recebimento de mensagens, análise da IA e encaminhamento para atendimento humano.

## 11. Conclusão

O desenvolvimento das versões V1, V3 e V4 demonstrou a importância de testar, identificar falhas e aprimorar continuamente as instruções fornecidas à IA.

A V4 apresentou resultados coerentes nos dez cenários avaliados, embora um deles tenha revelado uma ressalva importante na classificação de urgência.

O projeto ainda está em fase de prototipação e validação. O próximo objetivo é transformar a classificação textual em uma estrutura organizada de dados e iniciar sua integração com o n8n.

A proposta é desenvolver uma ferramenta de apoio à equipe de atendimento, capaz de organizar manifestações, identificar situações prioritárias e facilitar o encaminhamento das demandas, mantendo a avaliação humana nas decisões que exigem análise especializada.
