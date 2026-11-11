# SageMaker

- Serviço totalmente gerenciado utilizado para a construção de modelos de Machine Learning, feito para cientistas de dados e desenvolvedores especialistas em ML.

- Permite criar, treinar e implantar modelos de ML em grande escala, com suporte para diversos frameworks e algoritmos.

## Algoritmos pré-construídos

- O SageMaker oferece uma grande quantidade de algoritmos prontos para serem aplicados ao seu conjunto de dados. Alguns exemplos:

### Algoritmos Supervisionados (Supervised)
- Regressão Linear e classificação.

- KNN (Para classificação).

### Algoritmos não supervisionados (Unsupervised)
- **Principal Component Analysis (PCA)**: Simplifica datasets ao reduzir a dimensionalidade dos dados, mantendo a maior parte da informação possível.

- **K-Means**: Agrupa dados em clusters com base em características semelhantes.

- **Detecção de Anomalias**: Identifica padrões incomuns em dados, útil para detecção de fraudes ou falhas.

## Automatic Model Tuning (Hiperparâmetros)

- O SageMaker oferece a funcionalidade de ajuste automático de hiperparâmetros, que são parâmetros que controlam o processo de treinamento do modelo, como a taxa de aprendizado, o número de camadas em uma rede neural ou o número de árvores em um modelo de floresta aleatória.

- Isso é feito para modificar o comportamento do modelo e melhorar seu desempenho, como a taxa de aprendizado, o número de camadas em uma rede neural ou o número de árvores em um modelo de floresta aleatória.

## Deploy de Modelos

- Ao fazer o deploy de um modelo, será disponibilizado o endpoint de inferência, que é a URL que você pode usar para enviar dados e receber previsões do modelo.

- Há quatro opções para o deploy de modelos no SageMaker: 
  - **Real-time Inference**: Para casos de uso que exigem respostas rápidas, como chatbots ou detecção de fraudes em tempo real.
  - **Batch Transform**: Para processar grandes volumes de dados de uma só vez, como análise de imagens ou processamento de texto.
  - **Serverless Inference**: Para casos de uso com tráfego imprevisível, onde o modelo é carregado totalmente sob demanda, podendo ficar inativo quando não estiver em uso, economizando custos.
  - **Asynchronous Inference**: Para casos de uso que exigem processamento em segundo plano, como análise de grandes conjuntos de dados ou processamento de vídeo.

## SageMaker Studio
- O SageMaker Studio é uma IDE (que roda na web) que oferece uma visualização unificada de todo o ciclo de vida do Machine Learning.

- Por ele é possível fazer o tuning, depuração e deploy de modelos, além de monitorar métricas e logs de treinamento e inferência. Tudo de maneira colaborativa, permitindo que equipes de cientistas de dados e desenvolvedores trabalhem juntas em projetos de ML.

## Data Wrangler

- O SageMaker Data Wrangler é uma ferramenta que simplifica o processo de preparação de dados para Machine Learning.

- Por meio dele, é possível importar dados de diversas fontes, realizar a limpeza, transformá-los e visualizá-los, tudo em uma interface gráfica intuitiva.

- Ele permite que os cientistas de dados realizem transformações complexas nos dados sem precisar escrever código, além de gerar automaticamente scripts que podem ser reutilizados em pipelines de Machine Learning.

- Alguma das capacidades do Data Wrangler incluem:

  - **Criar amostras adicionais dos dados**, permitindo aumentar a diversidade do dataset de treinamento, o que pode melhorar a robustez e a capacidade de inferência dos modelos.
    - Isso é feito através de técnicas como **Oversampling** e **Inerpolação Sintética**, que consiste em replicar ou gerar novas amostras de classes minoritárias para equilibrar a distribuição dos dados no dataset de treinamento.

  - **Balancear a distribuição das classes nos dados**, garantindo que o modelo não seja tendencioso em relação a classes majoritárias.

  - **Detectar e tratar valores ausentes nos dados**, garantindo que o modelo receba informações completas e consistentes durante o treinamento.

  - **Detectar e tratar outliers nos dados**, garantindo que valores extremos não distorçam o treinamento do modelo e que o modelo aprenda padrões representativos do dataset.