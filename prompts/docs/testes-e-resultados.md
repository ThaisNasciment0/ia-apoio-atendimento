# Testes e resultados — IA de Apoio ao Atendimento ao Cliente

## Objetivo

Registrar os testes realizados com diferentes versões do prompt, avaliar a qualidade das classificações e documentar os ajustes necessários para melhorar a triagem de reclamações.

Os testes foram realizados com cinco mensagens fictícias, mantendo os mesmos textos para permitir a comparação entre as versões.

---

## 1. Cenários utilizados nos testes

**Teste 1 — Consulta sobre estoque**

> Gostaria de saber se vocês possuem uma previsão para disponibilizar novamente o produto que está esgotado no site.

**Teste 2 — Atraso no pedido**

> Realizei minha compra há cinco dias e o pedido ainda não foi enviado. No site, consta que o prazo de postagem era de dois dias.

**Teste 3 — Cobrança duplicada**

> Já entrei em contato quatro vezes sobre uma cobrança duplicada. Vocês continuam descontando o valor da minha conta e ninguém resolve. Quero meu dinheiro de volta.

**Teste 4 — Problema de acesso à conta**

> Não consigo entrar na minha conta de jeito nenhum. Coloco meu e-mail e senha e dá "credenciais inválidas". Já cliquei em "esqueci minha senha" duas vezes e o link de redefinição nunca chega na minha caixa de entrada, nem no spam. Preciso acessar meu painel agora.

**Teste 5 — Descumprimento de serviço contratado**

> Estou muito decepcionado. Contratei o serviço, paguei antecipadamente e a empresa não cumpriu o que prometeu. Se ninguém resolver hoje, vou registrar uma reclamação no Procon.

---

## 2. Resultados da versão V1

A primeira versão foi utilizada para verificar se a IA conseguia identificar o problema, classificar a prioridade e sugerir um encaminhamento inicial.

| Teste | Prioridade esperada | Resultado V1 | Avaliação |
|---|---|---|---|
| 1. Estoque | Baixa | Baixa | Correto |
| 2. Atraso | Média | Média | Correto |
| 3. Cobrança duplicada | Alta | Alta | Correto |
| 4. Acesso à conta | Média | Alta | Parcialmente correto |
| 5. Descumprimento de serviço | Alta | Alta | Correto |

**Resultado:** 4 de 5 classificações corresponderam à expectativa inicial.

**Principal ponto de melhoria:** o problema de acesso à conta foi classificado com prioridade alta sem evidências suficientes de impacto significativo. Era necessário diferenciar a dificuldade de acesso de situações em que a indisponibilidade impede uma atividade essencial.

---

## 3. Resultados da versão V3

A versão V3 incorporou critérios mais detalhados para classificação de prioridade, urgência e necessidade de avaliação humana.

| Teste | Prioridade | Urgência | Avaliação |
|---|---|---|---|
| 1. Estoque | Baixa | Baixa | Correto |
| 2. Atraso | Média | Normal | Adequado |
| 3. Cobrança duplicada | Alta | Alta | Correto |
| 4. Acesso à conta | Alta | Alta | Classificação excessiva |
| 5. Descumprimento de serviço | Alta | Alta | Parcialmente correto |

### Principais observações

**Teste 1 — Estoque:** classificação adequada. Solicitação informativa, sem impacto imediato.

**Teste 2 — Atraso:** classificação adequada. O problema foi identificado e encaminhado à logística. A necessidade de avaliação humana poderia ser melhor calibrada.

**Teste 3 — Cobrança duplicada:** classificação adequada. A IA identificou o impacto financeiro, as tentativas anteriores de contato e a necessidade de avaliação humana.

**Teste 4 — Acesso à conta:** prioridade e urgência foram superestimadas. A mensagem não apresentava evidências suficientes de que o acesso era essencial para uma
