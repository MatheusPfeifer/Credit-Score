# Credit-Score

## 1. Contexto
O problema de risco de crédito é um problema recorrente em instituições que oferecem este tipo de produto. A informação do score de crédito fornece para a empresa um valor, pode ser uma probabilidade por exemplo, de um cliente ser um provável bom pagador ou um provável mau pagador.

É importante a empresa ter essa estimativa, porque quando um cliente chegar para pedir algum tipo de crédito, será possível oferecer produtos personalizados para cada pessoa. Ou seja, pessoas com risco baixos poderão ter acesso a créditos maiores com taxas menores, em contrapartida clientes com baixos score, terão acessos a créditos menores com taxas maiores, por exemplo.

Uma das maneiras de estimar o score de crédito de um cliente é usando um algoritmo de Machine Learning em dados históricos, de forma que o algoritmo irá ser treinado para identificar padrões de clientes que foram bons pagadores ou maus pagadores no passado. Com o algoritmo treinado, este pode ser aplicado a novos clientes de maneira que vai retorna a probabilidade do cliente ser um bom cliente, dessa forma esta pessoa pode ser classificada dentro um grupo de risco baseado nesta probabilidade.

Um modelo de score de crédito é bastante eficiente para uma empresa que oferece crédito, pois pode mitigar riscos e evitar prejuízos desnecessários em oferecer crédito a prováveis maus pagadores.

Os dados para o problema são encontrado em: http://archive.ics.uci.edu/ml/machine-learning-databases/statlog/german/german.data

## 2. Plano de Solução
Como foi dito anteriormente, iremos utilizar Machine Learning para identificar o risco de crédito de clientes, baseado em dados históricos. O processo de análise foi divido em:
- Entendimento do problema de negócio
- Obtenção dos dados
- Análise exploratória dos dados
- Pré-processamento dos dados
- Criação do modelo
- Avaliação do modelo
- Entrega da solução

Para a entrega da solução, será fornecida uma tabela com os clientes que foram classificados de acordo com o risco de crédito, para a equipe de negócio poder avaliar qual a melhor solução de crédito pode ser entregada ao cliente.

## 3. Insights sobre os dados
Na pasta de script, será encontrado o arquivo com toda a análise dos dados e as principais conclusões tiradas. Aqui terá um resumo dos principais pontos sobre o perfil dos clientes que entraram em Churn:
- 30% dos clientes foram maus pagadores;
- Pessoas com conta negativas ou com pouco dinheiro em conta, tem maior porcentagem de maus pagadores;
- Clientes com pouco tempo de emprego e desempregados, são os que tem maior taxa de maus pagadores;
- Pessoas estrangeiras tem menor taxa de maus pagadores, do que os clientes que não são estrangeiros;
- Clientes que são maus pagadores, pedem em média quantias maiores que os bons pagadores;
- Pessoas classificadas como maus pagadoras, tem em média créditos com duração maior.

## 4. Modelo de Machine Learning
Para a construção do modelo, foi utilizada a biblioteca PyCaret que funciona de forma mais automatizada e fornece vários algoritmos de classificação, e dentre esses foram escolhidos alguns para testar. A biblioteca fornece diversas técnicas de Machine Learning que foram aplicadas ao modelo. Foram aplicadas a normalização para a variáveis numéricas, o tipo de normalização aplicada foi Z-Score. Para as variáveis categóricas, foi aplicado a dumificação de variáveis, que auxilia no treinamento do modelo de Machine Learning.

Para a avaliação do melhor modelo, foi levado em conta a métrica de f1-score, a escolha de otimizar esta métrica, é porque o f1-score retorna uma média harmônica entre a precisão e o recall. A precisão fornece o número de vezes que a classe foi predita corretamente, sobre o número de vezes que a classe foi predita. E o recall, o número de vezes que a classe foi predita corretamente, sobre a quantidade de observações no conjunto de dados.

Após testar todos os modelos, o modelo que apresentou melhor performance foi o de Regressão Logística. O modelo conseguiu prever 58/76 = 76,3% dos maus pagadores e 128/174 = 73,5% dos bons pagadores. Abaixo, será mostrado a matriz de confusão que fornece os acertos e erros do modelo para cada uma das classes.

O modelo de regressão logística, fornece como resultado uma probabilidade de o cliente pertencer a cada uma das classes, ou seja, o cliente é classificado na classe de bom pagador caso a probabilidade de ele pertencer a essa classe for maior do que a de pertencer a classe de mau pagador. Com essa informação, para classificar o risco de crédito de um cliente, foi utilizado um recurso de estatística.

Primeiramente, todos os clientes foram classificados de acordo com a probabilidade de serem bons pagadores. Ou seja, clientes que são maus pagadores tem uma probabilidade menor de serem bons pagadores, obviamente. Sendo assim, a probabilidade de ser bom pagador foi dividida em 4 grupos, levando em conta a distribuição dos clientes. Clientes em que a probabilidade está acima do 3º quartil (75%) foram classificados com risco baixo, clientes entre o 2º e o 3º quartil com risco médio; clientes entre o 1º e 2º quartil com risco alto; e cliente abaixo do 1º quartil (25%) com risco muito alto.

## 5. Resultado de negócio
Por último, será avaliado quanto que o modelo geraria de valor ao negócio. Quando o modelo foi testado em novos dados, que não foram usados para treinamento, o modelo acertou 1541  de 2037 casos de churn, ou seja, 75,7% dos casos. Dessa forma, a empresa poderia ter intervido nessa pessoas e ter evitado perder muitos clientes, oferecendo produtos ou benefícios para esses clientes.

Portanto, podemos considerar que o modelo construído consegue gerar valor para o negócio, mas que claro conforme for surgindo mais dados podemos aprimorar ainda mais o modelo.

## 6. Conclusão
Sendo assim, com o final deste projeto, foi possível observar que uma empresa que aplica modelos de Machine Learning para prever clientes que podem entrar em churn pode ser mais bem sucedida no mercado.
A respeito da solução temos diversos algoritmos de ML no mercado e passar por todos eles dentro de um projeto é praticamente impossível, para isso foi utilizado a biblioteca do Pycaret que aborda 18 algoritmos de classificação e foi obtido o melhor para a nossa análise. Também foi possível observar o quanto um conjunto de dados com classes desbalanceadas pode impactar negativamente o modelo. Porém, no final foi possível entregar uma boa solução ao cliente.
