# REGISTRO DE TESTES E EVOLUÇÃO
## Projeto: IA de Apoio ao Atendimento ao Cliente

**Autora:** Thais Nascimento  
**Área:** Inteligência Artificial | Experiência do Cliente | Automação  
**Status:** Protótipo em desenvolvimento  
**Início do projeto:** Outubro de 2026

---

# 1. Objetivo dos testes

Os testes têm como objetivo avaliar a capacidade de um modelo de inteligência artificial de analisar mensagens de clientes e apoiar uma equipe de atendimento na triagem de reclamações.

A avaliação considera:

- Identificação da categoria da ocorrência.
- Resumo do problema.
- Classificação da prioridade.
- Classificação da urgência.
- Identificação do sentimento do cliente.
- Indicação do setor responsável.
- Justificativa das classificações.
- Separação entre fatos, hipóteses e informações pendentes.
- Identificação de situações que exigem avaliação humana.

Foram utilizadas mensagens fictícias, sem dados pessoais ou informações reais de clientes.

# 2. Histórico das versões testadas

| Versão | Etapa | Objetivo |
|---|---|---|
| V1 | Testes manuais | Avaliar a classificação inicial das reclamações. |
| V3 | Testes manuais | Diferenciar prioridade, urgência e setor responsável. |
| V4 / V4.1 | Testes manuais | Refinar critérios de prioridade, urgência e encaminhamento humano. |
| V4.2 | Testes automatizados no n8n | Acrescentar justificativas para as classificações. |
| V4.3 | Testes automatizados no n8n | Separar fatos, hipóteses e informações pendentes; melhorar sentimento e segurança. |
| V4.4 | Planejada | Refinar a interpretação da urgência e evitar classificações baseadas apenas em expressões de pressa. |

# 3. Primeira bateria de testes — Cinco reclamações

## Teste 1 — Consulta sobre estoque

**Mensagem utilizada:**

"Gostaria de saber se vocês possuem uma previsão para disponibilizar novamente o produto que está esgotado no site."

**Resultado esperado:** Prioridade baixa.

**Resultados registrados:**

| Critério | Resultado |
|---|---|
| V1 | Baixa |
| V4.2 | Baixa |
| Urgência na V4.2 | Normal |
| Avaliação | Correto quanto à prioridade e urgência |

**Observações:**

A IA identificou corretamente uma solicitação de informação, sem impacto imediato. Na versão automatizada, houve uma pequena imprecisão na escolha de palavras ao descrever a reposição do produto.

## Teste 2 — Atraso no pedido

**Mensagem utilizada:**

"Realizei minha compra há cinco dias e o pedido ainda não foi enviado. No site, consta que o prazo de postagem era de dois dias."

**Resultado esperado:** Prioridade média.

**Resultados registrados:**

| Critério | Resultado |
|---|---|
| V1 | Média |
| V4 | Alta |
| V4.2 | Média |
| Urgência na V4.2 | Normal |
| Avaliação | Melhora na classificação |

**Observações:**

A primeira versão apresentou classificação adequada. Em um teste posterior, a IA elevou a prioridade e a urgência sem justificativa suficiente.

Na V4.2, a classificação voltou a ser média, considerando o atraso informado e a ausência de evidências de um impacto mais grave.

A IA ainda atribuiu sentimento de frustração sem uma manifestação emocional explícita.

## Teste 3 — Cobrança duplicada

**Mensagem utilizada:**

"Já entrei em contato quatro vezes sobre uma cobrança duplicada. Vocês continuam descontando o valor da minha conta e ninguém resolve. Quero meu dinheiro de volta."

**Resultado esperado:** Prioridade alta.

**Resultados registrados:**

| Critério | Resultado |
|---|---|
| V1 | Alta |
| V4 | Alta |
| V4.2 | Alta |
| Urgência na V4.2 | Alta |
| Avaliação | Classificação adequada, com ajustes necessários na resposta |

**Observações:**

A IA identificou corretamente a recorrência do problema, as tentativas anteriores de resolução e a continuidade dos descontos.

A versão automatizada apresentou justificativa mais detalhada, mas teve problemas na descrição do sentimento, chegando a apresentar termos contraditórios.

Também foi identificada a necessidade de evitar solicitações desnecessárias de informações financeiras sensíveis.

## Teste 4 — Dificuldade de acesso à conta

**Mensagem utilizada:**

"Não consigo entrar na minha conta de jeito nenhum. Coloco meu e-mail e senha e dá 'credenciais inválidas'. Já cliquei em 'esqueci minha senha' duas vezes e o link de redefinição nunca chega na minha caixa de entrada, nem no spam. Preciso acessar meu painel agora."

**Resultado esperado:** Prioridade média, até que o impacto seja confirmado.

**Resultados registrados:**

| Critério | Resultado |
|---|---|
| V1 | Alta |
| V4.1 | Média |
| V4.2 | Alta |
| V4.3 | Alta |
| Urgência na V4.3 | Imediata |
| Avaliação | Problema de classificação ainda não resolvido |

**Observações:**

Este teste demonstrou uma dificuldade recorrente da IA: interpretar a expressão "preciso acessar meu painel agora" como evidência suficiente de urgência imediata.

Mesmo após a inclusão de regras para diferenciar prioridade e urgência, o modelo continuou presumindo que o acesso ao painel era essencial para as atividades do cliente.

A V4.3 melhorou a separação entre fatos, hipóteses e informações pendentes, mas ainda apresentou uma justificativa contraditória.

Também classificou o sentimento como frustração sem evidências emocionais suficientemente claras.

## Teste 5 — Serviço contratado e não entregue

**Mensagem utilizada:**

"Estou muito decepcionado. Contratei o serviço, paguei antecipadamente e a empresa não cumpriu o que prometeu. Se ninguém resolver hoje, vou registrar uma reclamação no Procon."

**Resultado esperado:** Prioridade alta.

**Resultados registrados:**

| Critério | Resultado |
|---|---|
| V1 | Alta |
| V4 | Alta |
| Avaliação | Correto |

**Observações:**

A IA identificou o descumprimento do serviço contratado e o pagamento antecipado. A ocorrência exige avaliação humana para verificar o contrato, as condições da contratação e as providências cabíveis.

---

# 4. Segunda bateria de testes — Novas situações

Nesta etapa, foram acrescentadas situações diferentes para ampliar a avaliação do comportamento da IA.

## Teste 6 — Entrega parcial do pedido

**Mensagem utilizada:**

O cliente relata que recebeu apenas parte dos produtos comprados e que alguns itens não estavam na embalagem.

**Resultado esperado:** Prioridade média.

**Resultado da IA:** Prioridade média | Urgência normal.

**Setor indicado:** Logística.

**Avaliação:** Adequado.

**Observações:**

A IA identificou corretamente uma divergência na entrega e indicou o setor responsável. A ocorrência precisa ser verificada antes de qualquer promessa de envio dos itens faltantes.

## Teste 7 — Suspeita de acesso não autorizado

**Mensagem utilizada:**

O cliente relata ter identificado acessos à conta que não reconhece.

**Resultado esperado:** Prioridade alta, com necessidade de avaliação imediata da segurança.

**Resultado da IA:** Prioridade alta | Urgência imediata.

**Setor indicado:** Segurança / Suporte técnico.

**Avaliação:** Adequado quanto à necessidade de avaliação humana.

**Observações:**

O caso demonstrou a importância de identificar situações relacionadas à segurança da conta e não permitir que a IA execute ou recomende alterações sensíveis sem validação humana.

Também foi identificada a necessidade de não afirmar que a ocorrência já foi encaminhada sem confirmação.

## Teste 8 — Indisponibilidade recorrente do serviço

**Mensagem utilizada:**

O cliente relata que o serviço ficou indisponível várias vezes durante a semana.

**Resultado da IA na V4:** Prioridade alta | Urgência imediata.

**Resultado da IA na V4.1:** Prioridade alta | Urgência normal, enquanto o impacto atual não estiver confirmado.

**Avaliação:** Melhora após o ajuste.

**Observações:**

O teste demonstrou que a recorrência deve influenciar a prioridade, mas não determina automaticamente a urgência imediata.

É necessário verificar se o serviço continua indisponível, qual atividade foi afetada e se existe prejuízo ou risco atual.

## Teste 9 — Insatisfação com a experiência de compra

**Mensagem utilizada:**

"Estou bastante insatisfeito com a experiência de compra. Achei o processo confuso, o site é difícil de navegar e não gostei da forma como as informações dos produtos são apresentadas. Gostaria que melhorassem isso."

**Resultado da IA:** Prioridade baixa | Urgência baixa.

**Setor indicado:** Atendimento / Experiência do Cliente.

**Avaliação:** Adequado.

**Observações:**

A IA identificou uma manifestação de insatisfação e uma oportunidade de melhoria na experiência de compra.

O caso pode ser registrado como feedback, sem necessidade automática de intervenção humana.

## Teste 10 — Cobrança não reconhecida

**Mensagem utilizada:**

"Consultei minha fatura e encontrei um valor que não reconheço. Ainda não sei se é uma cobrança indevida ou alguma taxa prevista no contrato. Gostaria de entender do que se trata."

**Resultado da IA:** Prioridade média | Urgência normal.

**Setor indicado:** Financeiro / Cobrança.

**Avaliação:** Adequado.

**Observações:**

A IA identificou corretamente que ainda não existe confirmação de cobrança indevida. O caso precisa de análise do setor financeiro, sem antecipar conclusões ou prometer estorno.

---

# 5. Testes automatizados com n8n e Groq

Após a validação inicial dos prompts manualmente, o projeto avançou para uma etapa de automação.

Foi criado um fluxo no n8n para receber uma mensagem fictícia, enviá-la ao modelo de IA e retornar uma análise estruturada.

**Componentes utilizados:**

- n8n: ferramenta de automação.
- Edit Fields: entrada da mensagem.
- Basic LLM Chain: estrutura do processamento do prompt.
- Groq Chat Model: modelo de linguagem utilizado nos testes.

**Objetivo desta etapa:**

Verificar se as regras definidas no prompt seriam respeitadas também durante a execução automatizada.

## Principais observações dos testes automatizados

1. A IA conseguiu identificar categorias e setores responsáveis de maneira consistente.
2. A classificação de prioridade melhorou após a inclusão de critérios mais claros.
3. A urgência ainda apresentou interpretações excessivas em situações com expressões de pressa.
4. O sentimento do cliente foi identificado incorretamente em mensagens sem manifestação emocional explícita.
5. A justificativa ajudou a visualizar os critérios utilizados, mas também revelou contradições.
6. A separação entre fatos, hipóteses e informações pendentes melhorou a organização das respostas.

---

# 6. Comparativo da evolução

| Aspecto avaliado | Problema identificado | Ajuste realizado |
|---|---|---|
| Prioridade | Classificação influenciada pelo tom emocional | Inclusão de critérios objetivos de impacto |
| Urgência | Recorrência ou pressa interpretadas como urgência imediata | Separação entre prioridade e urgência |
| Setor responsável | Encaminhamento pouco detalhado | Inclusão de setores responsáveis |
| Justificativa | Pouca transparência sobre a classificação | Inclusão de justificativas |
| Fatos e hipóteses | Possibilidade de apresentar suposições como fatos | Separação das informações |
| Sentimento | Emoções presumidas a partir de reclamações | Regra para identificar apenas sentimentos evidenciados |
| Segurança | Risco de recomendações envolvendo operações sensíveis | Inclusão de regras de proteção e validação humana |

# 7. Principais aprendizados

Durante os testes, foram identificados alguns pontos importantes:

- Um prompt precisa ser testado com diferentes situações para revelar falhas que não aparecem em exemplos simples.
- A classificação de prioridade não deve depender exclusivamente do sentimento do cliente.
- Prioridade e urgência são critérios diferentes e precisam ser avaliados separadamente.
- Uma justificativa detalhada não garante que a classificação esteja correta.
- A IA precisa reconhecer quando não possui informações suficientes.
- A intervenção humana continua sendo necessária em situações financeiras, de segurança e de alterações de conta.
- A automação precisa respeitar limites de atuação e não afirmar que procedimentos foram executados sem confirmação.

# 8. Próximas etapas

- [ ] Desenvolver a versão 4.4 do prompt.
- [ ] Repetir o teste de acesso à conta.
- [ ] Repetir o teste de indisponibilidade recorrente.
- [ ] Verificar se a IA diferencia sentimento de urgência.
- [ ] Avaliar a consistência das justificativas.
- [ ] Testar novas mensagens fictícias.
- [ ] Definir um formato de saída estruturado em JSON.
- [ ] Preparar a integração com uma planilha para registrar as ocorrências.
- [ ] Avaliar o encaminhamento de casos prioritários para uma equipe humana.

# 9. Considerações finais

O desenvolvimento deste protótipo tem demonstrado que a utilização de inteligência artificial no atendimento ao cliente exige mais do que a criação de um prompt.

É necessário testar, observar os resultados, identificar inconsistências e realizar ajustes continuamente.

A experiência com os testes também permitiu aplicar conhecimentos de Experiência do Cliente na construção de regras para classificação de reclamações, identificação de prioridades e organização das informações.

O projeto ainda está em desenvolvimento e os resultados apresentados são experimentais, baseados em mensagens fictícias. As funcionalidades e os critérios serão aprimorados antes de qualquer aplicação em um ambiente real.

**Registro de evolução:** este documento deverá ser atualizado a cada nova versão do prompt e a cada bateria de testes realizada.

---

# 10. Histórico de atualizações do documento

| Data | Versão do prompt | Atualização |
|---|---|---|
| Outubro/2026 | V1 | Primeiros testes de classificação |
| Novembro/2026 | V3 e V4 | Refinamento dos critérios |
| Novembro/2026 | V4.1 | Ajustes na diferenciação entre prioridade e urgência |
| Novembro/2026 | V4.2 | Testes automatizados e inclusão de justificativas |
| Novembro/2026 | V4.3 | Separação entre fatos, hipóteses e informações pendentes |
| A definir | V4.4 | Próxima etapa de aprimoramento |
## Teste 13 — Indisponibilidade recorrente do serviço (V4.5)

**Resultado da IA:**
- Categoria: Serviço indisponível.
- Prioridade: Alta.
- Urgência: Normal.
- Sentimento: Neutro.
- Setor: Suporte Técnico / Equipe de Disponibilidade de Serviços.

**Avaliação:** Satisfatório.

**Evolução em relação à V4.4:**

A V4.5 corrigiu a classificação da prioridade, considerando a recorrência do problema e as tentativas anteriores de resolução sem solução definitiva.

A urgência permaneceu normal, pois não foram apresentados elementos que comprovassem um impacto crítico imediato.

O sentimento também foi corrigido, passando de frustrado/insatisfeito para neutro, uma vez que o cliente não demonstrou explicitamente uma emoção.

**Pontos positivos:**
- Considerou corretamente a recorrência.
- Diferenciou prioridade e urgência.
- Apresentou justificativa coerente.
- Separou fatos, hipóteses e informações pendentes.

**Pontos a melhorar:**
- Aprimorar a revisão gramatical.
- Formular perguntas mais simples e adequadas ao cliente.
- Evitar solicitar informações técnicas que podem ser verificadas internamente.

**Conclusão:**

A versão 4.5 apresentou evolução consistente na classificação de problemas recorrentes, demonstrando maior aderência aos critérios definidos para o protótipo.

## Teste 14 — Cobrança não reconhecida (V4.5)

**Mensagem utilizada:**

"Consultei minha fatura e encontrei uma cobrança de R$ 189,90 que não reconheço. Não me lembro de ter contratado nenhum serviço nesse valor. Ainda não sei se é uma cobrança indevida ou alguma taxa prevista no contrato. Gostaria de entender do que se trata antes de realizar qualquer pagamento."

**Resultado da IA:**
- Categoria: Cobrança / Fatura – Cobrança não reconhecida.
- Prioridade: Baixa.
- Urgência: Normal.
- Sentimento: Neutro.
- Setor: Financeiro / Cobrança.

**Avaliação:** Parcialmente satisfatório.

**Pontos positivos:**
- Identificou corretamente a categoria e o setor.
- Não afirmou que a cobrança era indevida.
- Diferenciou fatos de hipóteses.
- Não classificou a situação como urgente sem evidências.
- Identificou a necessidade de análise financeira.

**Pontos a melhorar:**
- A prioridade deveria ser média, conforme os critérios deste protótipo.
- Melhorar a qualidade gramatical e a clareza do texto.
- Orientar o fornecimento de informações financeiras somente por canais seguros.
- Evitar solicitar dados desnecessários.

**Conclusão:**

A V4.5 demonstrou cautela ao interpretar uma cobrança ainda não identificada, evitando conclusões precipitadas. Entretanto, classificou a prioridade abaixo do esperado, indicando a necessidade de critérios mais específicos para ocorrências financeiras.

A urgência normal foi considerada adequada, pois não havia evidência de prejuízo imediato ou prazo crítico.

## Teste 14 — Cobrança não reconhecida (V4.6)

**Mensagem utilizada:**

"Consultei minha fatura e encontrei uma cobrança de R$ 189,90 que não reconheço. Não me lembro de ter contratado nenhum serviço nesse valor. Ainda não sei se é uma cobrança indevida ou alguma taxa prevista no contrato. Gostaria de entender do que se trata antes de realizar qualquer pagamento."

**Resultados:**

- Categoria: Cobrança não confirmada / Divergência na fatura.
- Prioridade esperada: Média.
- Prioridade da IA: Média.
- Urgência: Normal.
- Sentimento: Neutro.
- Setor responsável: Financeiro / Cobrança.

**Avaliação:**

A classificação foi considerada correta. A nova regra financeira da V4.6 corrigiu o resultado anterior, que havia classificado a ocorrência como baixa prioridade.

A IA reconheceu que uma cobrança não identificada precisa de análise, mesmo sem confirmação de pagamento ou prejuízo financeiro. Também diferenciou corretamente prioridade e urgência, sem presumir que a cobrança fosse indevida.

**Pontos positivos:**
- Aplicação correta da regra de prioridade média.
- Separação adequada entre fatos, hipóteses e informações pendentes.
- Encaminhamento coerente ao setor Financeiro/Cobrança.
- Respeito às orientações de segurança.

**Oportunidades de melhoria:**
- Corrigir erros gramaticais no resumo.
- Utilizar expressões mais claras e naturais.
- Solicitar somente as informações necessárias para a análise, preferencialmente por canal seguro.

**Conclusão:**

A V4.6 apresentou evolução em relação à V4.5. A nova regra financeira funcionou conforme esperado. Os ajustes de escrita e objetividade das perguntas serão acompanhados nos próximos testes.

## Teste 15 — Cobrança recorrente sem solução

**Mensagem testada:**

"Já é a segunda vez que aparece essa cobrança de R$ 189,90 na minha fatura. Entrei em contato com o atendimento na semana passada e me informaram que iriam verificar, mas até agora não tive retorno. A cobrança apareceu novamente e não quero continuar pagando por algo que não reconheço. Preciso que verifiquem essa situação."

**Resultado da IA — V4.6:**

- **Categoria:** Cobrança não reconhecida – fatura
- **Prioridade:** Alta
- **Urgência:** Normal
- **Sentimento:** Neutro
- **Setor responsável:** Financeiro / Cobrança

**Avaliação:** Classificação correta.

**Pontos positivos:**
- Identificou a recorrência da cobrança e a tentativa anterior sem solução.
- Elevou a prioridade para alta, conforme os critérios da seção 16.
- Diferenciou prioridade alta de urgência imediata.
- Não presumiu que a cobrança era indevida.
- Não prometeu estorno ou cancelamento.
- Separou fatos, hipóteses e informações pendentes.

**Oportunidades de melhoria:**
- Evitar acrescentar informações não confirmadas, como afirmar que as cobranças ocorreram em faturas consecutivas.
- Manter os resumos e fatos sempre em terceira pessoa.
- Não associar recorrência automaticamente à insatisfação do cliente.
- Solicitar somente as informações necessárias para a análise.

**Conclusão:** A V4.6 apresentou o comportamento esperado na classificação de prioridade e urgência. Não será alterada neste momento. Os ajustes de linguagem serão acumulados para uma próxima versão do prompt.
