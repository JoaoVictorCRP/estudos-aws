# Ensemble Learning
Ensemble Learning é uma técnica de aprendizado de máquina onde múltiplos modelos são combinados para melhorar a performance da inferência. Esta é uma técnica que comprovadamente trás benefícios em termos de acurácia e robustez do modelo.

Existem diferentes categorias de ensemble learning, sendo as principais:

- **Boosting**: Técnica onde modelos mais fracos são treinados sequencialmente, e cada modelo subsequente tenta corrigir os erros do modelo anterior através da modificação dos pesos das amostras de treinamento.
  - Exemplos: AdaBoost, Gradient Boosting, XGBoost.

- **Bagging**: Utiliza múltiplos modelos para reduzir a variância de um modelo principal, treinando cada modelo em subconjuntos diferentes do conjunto de treinamento.
  - Exemplos: Random Forest, Extra Trees. 

- **Stacking**: Combina **modelos de tipos diferentes** para melhorar a performance geral, a inferência de cada um é "empilhada" e utilizada como entrada para um modelo final que faz a predição.
  - Exemplos: Stacked Generalization, Super Learner.