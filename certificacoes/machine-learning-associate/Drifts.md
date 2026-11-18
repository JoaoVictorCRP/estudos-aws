# Data Drift e Model Drift
- Em Machine Learning, é comum que o desempenho de um modelo comece a degradar ao longo do tempo devido a mudanças nos dados de entrada ou no ambiente em que o modelo opera. Esse fenômeno é conhecido como **drift**.

- Temos duas categorias principais de drift, são elas:

- **Data Drift**: Que ocorre quando a distribuição dos dados de entrada muda ao longo do tempo, afetando a capacidade do modelo de fazer previsões precisas.

  - **Exemplo**: Usuários começam a interagir de maneira diferente com um aplicativo, alterando o padrão de uso que o modelo foi treinado para prever, resultando em respostas menos precisas do modelo.

- **Model Drift**: Ocorre quando o desempenho do modelo se deteriora ao longo do tempo, mesmo que a distribuição dos dados de entrada permaneça a mesma, indicando que o modelo não está mais capturando corretamente os padrões subjacentes nos dados.

  - **Exemplo**: Um modelo de previsão de vendas que foi treinado com dados históricos pode começar a apresentar erros maiores se houver mudanças significativas no mercado ou no comportamento do consumidor, mesmo que os dados de entrada sigam a mesma distribuição.

## No SageMaker
- Usando o SageMaker, é possível monitorar tanto o Data Drift quanto o Model Drift através do **Model Monitor**. Assim, você pode detectar mudanças na distribuição dos dados de entrada ou no desempenho do modelo ao longo do tempo, antes que as reclamações de usuários ou problemas de negócio se tornem evidentes.