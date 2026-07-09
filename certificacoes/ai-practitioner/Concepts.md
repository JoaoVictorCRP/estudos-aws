# Conceitos de GenAI e Machine Learning

## Tokenization
- A tokenização é o processo de converter texto puro em uma sequência de tokens, que são as unidades básicas de texto que os modelos de linguagem processam.
  - Os tokens podem ser palavras, subpalavras ou caracteres, dependendo do modelo e da técnica de tokenização utilizada.
  
- A tokenização é fundamental para o funcionamento dos modelos de linguagem, pois permite que eles compreendam e processem o texto de maneira eficiente.

- Você pode obter a quantidade de tokens de um texto usando a API de tokenização do modelo (**Tokenizer**), o que é útil para entender o custo e a eficiência do processamento.
  - O Bedrock também possui a funcionalidade de Tokenização para os modelos de fundação que ele oferece.

## Context Window
- A janela de contexto (context window) é o número máximo de tokens que um modelo pode processar de uma vez ao gerar uma resposta.
  - Quanto maior a janela de contexto, mais informações o modelo pode considerar ao gerar a resposta, portanto maior será a coerência.

## Tipos de aprendizado de máquina (Machine Learning)
- Existem 3 tipos principais de aprendizado de máquina: supervisionado (supervised), não-supervisionado (unsupervised), por reforço (reinforcement).

  - O aprendizado supervisionado é quando o modelo é treinado usando dados rotulados, ou seja, dados (input) que já incluem o output esperado.
    - A máquina aqui aprende com base na iteração da predição de resultados, tornando o output final cada vez mais preciso.
  
  - O aprendizado não-supervisionado é quando os dados usados no treinamento não possuem o output esperado. Fazendo com que a própria máquina identifique padrões e anomalias nos dados, sem qualquer intervenção humana.
    - Esse tipo de aprendizado é muito utilizado para análise de risco de crédito, detecção de fraudes e segmentação de clientes.

  - O aprendizado por reforço é quando o modelo aprende a tomar decisões com base em recompensas e punições, recebendo feedback sobre suas ações e ajustando seu comportamento para maximizar a recompensa ao longo do tempo.
    - Esse tipo de aprendizado é muito utilizado em jogos, robótica e sistemas de recomendação, onde o modelo precisa aprender a tomar decisões em um ambiente dinâmico e incerto.

- Adicionalmente, podemos citar também o aprendizado semi-supervisionado, que é uma combinação dos dois primeiros tipos, onde o modelo é treinado com uma pequena quantidade de dados rotulados e uma grande quantidade de dados não rotulados.
  - Esse tipo de aprendizado é útil quando a rotulagem de dados é cara ou demorada, permitindo que o modelo aprenda com menos supervisão humana.

## Embedding
- O embedding é uma técnica de representação de texto em um espaço vetorial, onde palavras, frases ou documentos são convertidos em vetores numéricos que capturam o significado semântico do texto.
  - Os modelos de embeddings são treinados para criar essas representações vetoriais, permitindo que o modelo compreenda as relações semânticas entre diferentes palavras ou frases.

- Para além de transformar texto em vetores númericos, os embeddings são úteis para capturar outras informações, como o sentido semântico, a sintaxe e o sentimento expresso no texto, o que os torna uma ferramenta poderosa para tarefas de processamento de linguagem natural (NLP).

- Uma outra vantagem de vetorizar textos é o fato de que ele facilita a busca e a recuperação de informações, permitindo que o modelo correlacione palavras ou frases semelhantes, mesmo que não sejam idênticas.

## Overfitting e Underfitting

- Ambos são termos usados para descrever problemas de desempenho em modelos de ML.

- Overfitting é quando um modelo aprende muito bem os dados de treinamento, mas não consegue generalizar para dados novos, resultando em baixa performance em dados não vistos.

- Underfitting é quando um modelo não aprende o suficiente dos dados de treinamento, resultando em baixa performance tanto nos dados de treinamento quanto nos dados novos.

## Bias e Variance

- O tradeoff entre bias (viés) e variance (variância) é um conceito fundamental em aprendizado de máquina, que descreve a relação entre a complexidade do modelo e sua capacidade de generalização. Ao fazer um modelo mais complexo, você reduz o erro sistêmico (bias), mas aumenta a variância, tornando o modelo sensível a pequenas variações em relação aos dados de treinamento.

  - Bias é a tendência de um modelo de ML de fazer previsões sistematicamente incorretas devido a suposições simplificadas feitas durante o treinamento, o "underfitting".

  - Variance é a tendência de um modelo de ML de ser sensível a pequenas variações nos dados de treinamento, resultando em previsões inconsistentes, o "overfitting".

- O desafio é encontrar o equilíbrio entre as duas, de modo que o modelo seja capaz de generalizar bem para novos dados, sem ser excessivamente complexo ou simplista.