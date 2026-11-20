# Algoritmos de Machine Learning

Existem diversos algoritmos de Machine Learning, cada um adequado para diferentes tipos de problemas e dados. Para a certificação Machine Learning Associate, é importante ter uma compreensão dos principais algoritmos e suas aplicações. Vejamos alguns:

## Word2Vec
- Um algoritmo de aprendizado de representação de palavras, usado principalmente em processamento de linguagem natural (NLP) para transformar palavras em vetores densos que capturam semântica e contexto.

- Com a vetorização de palavras, a máquina pode entender relações semânticas entre palavras, como similaridade e analogias, facilitando tarefas de NLP como tradução automática, análise de sentimentos e busca semântica.

  - A AWS fez melhorias no Word2Vec e criou o algoritmo **BlazingText**, que é otimizado para treinamento rápido e eficiente de modelos de representação de palavras em larga escala, disponível como algoritmo gerenciado no Amazon SageMaker.

## SVM (Support Vector Machine)
- Um algoritmo de aprendizado supervisionado usado para classificação e regressão. O SVM busca encontrar o hiperplano que melhor separa as classes no espaço de características, maximizando a margem entre os pontos de diferentes classes.
  
  - Em outras palavras, ele separa as classes de dados traçando uma linha (ou hiperplano em dimensões mais altas) que maximiza a distância entre os pontos de diferentes classes. Isso ajuda a melhorar a generalização do modelo e a reduzir erros de classificação.

- O SVM é muito usado em cenários onde há uma clara separação entre as classes e os dados são de alta dimensionalidade, como em reconhecimento de imagens, detecção de fraudes e recomendação de produtos.
  - A Netflix, por exemplo, utiliza SVMs para sistemas de recomendação, ajudando a prever se um filme é "Recomendado" ou "Não recomendado" para um usuário específico.

## Random Forest
- Um algoritmo de aprendizado supervisionado usado para classificação e regressão. Ele constrói múltiplas árvores de decisão durante o treinamento e combina suas previsões para melhorar a precisão e reduzir o overfitting.

  - **Cada árvore de decisão é treinada em uma amostra aleatória dos dados** e considera apenas um subconjunto aleatório das características em cada divisão, o que aumenta a diversidade entre as árvores e melhora a robustez do modelo.

- O Random Forest é amplamente utilizado em problemas de classificação e regressão em diversas áreas, como detecção de fraudes, diagnóstico médico e previsão de demanda.
  - Empresas como a Amazon utilizam Random Forests para sistemas de recomendação e detecção de anomalias em transações, aproveitando a capacidade do algoritmo de lidar com grandes volumes de dados e características complexas.

- A Amazon desenvolveu uma variante desse algoritmo chamado **Random Cut Forest (RCF)**, que é otimizado para detecção de anomalias em grandes volumes de dados de séries temporais, sendo capaz de identificar padrões incomuns de forma eficiente e escalável, sem precisar de rótulos ou supervisão explícita.

## Transformers
- Um algoritmo de aprendizado profundo usado principalmente em processamento de linguagem natural (NLP) e tarefas de sequência a sequência. 

- Os Transformers utilizam mecanismos de atenção para capturar dependências de longo alcance nos dados, permitindo que o modelo foque em partes relevantes da entrada ao fazer previsões.

  - Diferente de redes neurais recorrentes (RNNs), os Transformers processam toda a sequência de entrada simultaneamente, o que melhora a eficiência do treinamento e a capacidade de capturar contextos complexos.

- Os Transformers são amplamente utilizados em tarefas de NLP, como tradução automática, resumo de texto, geração de linguagem natural e análise de sentimentos.

  - Um **exemplo muito popular de transformer é a linha GPT (da OpenAI)**, pioneiros na geração de texto natural e criação de assistentes de IA.

## K-Means
- Este é um algoritmo de **clusterização não supervisionado que busca agrupar dados em `k` clusters distintos** com base em suas características.

- O K-Means funciona iterativamente, atribuindo cada ponto de dados ao cluster mais próximo com base na média dos pontos do cluster e atualizando os centróides até que a convergência seja alcançada.

- É amplamente utilizado em análise de clientes, segmentação de mercado, compressão de imagens e detecção de anomalias.

## DeepAR
- DeepAR é um algoritmo de aprendizado profundo desenvolvido pela Amazon para **previsão de séries temporais**. Ele é especialmente eficaz em cenários com múltiplas séries temporais relacionadas e dados esparsos.

- O DeepAR utiliza redes neurais recorrentes (RNNs) para modelar a dinâmica temporal das séries, aprendendo padrões complexos e dependências de longo prazo.

- É amplamente utilizado em previsão de demanda, previsão de vendas, monitoramento de infraestrutura e outros cenários onde a previsão precisa de séries temporais é crucial.

## Linear Learner
- Linear Learner é um algoritmo de aprendizado supervisionado que pode ser usado para tarefas de classificação e regressão. 

- Ele é projetado para lidar com grandes volumes de dados e é eficiente em termos de tempo de treinamento.

- O Linear Learner é **particularmente útil quando se trabalha com grandes conjuntos de dados e quando a interpretabilidade do modelo é importante**, pois os coeficientes lineares podem ser facilmente analisados para entender a influência de cada característica na previsão.

- Muito utilizado para classicação binária (exemplo: detecção de fraude, classificação de e-mails como spam ou não spam).