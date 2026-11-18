# Catastrophic Forgetting
- O **Catastrophic Forgetting** (ou esquecimento catastrófico) é um problema em aprendizado contínuo, onde um modelo de machine learning esquece informações previamente aprendidas ao ser treinado com novos dados. Isso ocorre principalmente em redes neurais, que tendem a sobrescrever os pesos ajustados anteriormente ao aprender novas tarefas.

- Esse é um dos grandes perigos do Fine Tunning, pois ao ajustar os pesos de um modelo pré-treinado para uma nova tarefa, ele pode esquecer informações importantes aprendidas anteriormente, prejudicando seu desempenho em tarefas anteriores.

- Para mitigar o Catastrophic Forgetting, técnicas como **replay de memória**, **regularização** e **aprendizado incremental** são frequentemente utilizadas. Essas abordagens ajudam o modelo a reter conhecimento antigo enquanto aprende novas tarefas, equilibrando a adaptação e a preservação do conhecimento prévio.

- Para ajudar com a resolução deste problema, a AWS oferece o **Nova Forge Data Mixing** no painel do SageMaker.
  
  - Essa funcionalidade permite misturar os novos dados de treinamento que você está utilizando com dados antigos (vindos de datasets previamente coletados e curados pela própria AWS), ajudando a preservar o conhecimento previamente adquirido pelo modelo e reduzir o risco de esquecimento de tarefas do modelo de fundação anterior.