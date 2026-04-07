# Amazon Bedrock

- O Bedrock é um seviço de IA generativa totalmente gerenciado, ele fornece uma interface de aceesso a diversos ([modelos de fundação](../certificacoes/ai-practitioner/foundation-models.md)), como Claude, Llama, Stable Diffusion, Titan e muito mais.

- O modelo de custo é pay-per-use, portanto você só é cobrado pelas requisições e quantidade de tokens processados.

## Modelos de Fundação

- Como dito anteriormente, diversos modelos de fundação estão disponíveis no Bedrock.

- É importante esclarecermos que os modelos usados na sua conta AWS pertencem a você, e nenhum dado ou informação processados por eles serão usados para treinamento do modelo de fundação.

  - Isso torna as aplicações construídas com o Amazon Bedrock extremamente seguras para o uso corporativo, já que nenhuma regra ou segredo de negócio será usada para retreinar o modelo, **como ocorre em IAs públicas.**

## Fine Tuning de Modelos

- Em poucas palavras, o Fine Tuning é a prática de modificar o comportamento de um modelo de fundação usando dados produzidos por você.

- O Fine Tuning fará a mudança de pesos do modelo de fundação, o que **pode ser um processo demorado e custoso, dependendo do modelo e da quantidade de dados usados**.
  - **Observação**: pesos são os parâmetros que o modelo de fundação usa para processar e reconhecer as informações que recebe, são eles que definem o resultado (output) que o modelo irá gerar.

- Os dados de treinamento precisam:
  - Seguir um formato específico, que varia de acordo com o modelo de fundação escolhido.
    - Ex: arquivo JSON onde cada linha é um exemplo de treinamento, contendo um prompt e uma resposta esperada.

  - Estar armazenados em um bucket S3.

- Detalhe, nem todos os modelos de fundação disponíveis no Bedrock suportam o fine tuning, é importante verificar a documentação do modelo escolhido para saber se ele suporta ou não essa funcionalidade.

### Tipos de Fine Tuning

#### Supervised Fine Tuning
- Melhora a performance do modelo em uma tarefa específica.

- Utiliza exemplos rotulados (*labeled examples*) com pares de entrada-saída (Ex: prompt + resposta esperada).

#### Reinforcement Fine Tuning
- Melhora o modelo usando **aprendizado baseado em feedback**.

- Você provê APENAS os dados de entrada/treinamento (O prompt).

- Você define uma **reward function (função de recompensa)** que valida as repostas e julga se elas foram boas ou não.
  - A definição dessas funções depende do tipo de tarefa e como ela deve ser avaliada.

  - Se for uma tarefa objetiva, com uma resposta certa clara, você pode usar uma função lambda para a avaliação da resposta.

  - Já se a tarefa for subjetiva, pode-se usar um outro modelo (modelo juiz) para julgar as respostas com base em instruções de validação.

![Reward Function Diagram](./images/reward-function-fine-tunning.png)

- Com isso, o modelo aprenderá de maneira iterativa com base na pontuação de suas respostas, entregues pela função.

- Veja abaixo um exemplo de Fine Tuning usando um modelo juiz:

![Reinforcement Fine Tuning Example](./images/reinforcement-fine-tuning-example.png)

#### Distillation Fine Tuning

- O processo de distillation é uma técnica de **compressão de modelos**, onde um modelo menor (modelo estudante) é treinado para imitar o comportamento de um modelo maior (modelo professor).

- O principal objetivo é criar um modelo mais leve, eficiente e de baixo custo.

- O modelo estudante é treinado usando as saídas do modelo professor como rótulos, em vez de usar dados rotulados tradicionais.

## Model Evaluation

- O Bedrock oferece suporte para validação de Modelos, permitindo que você possa testar se um modelo se adequa ao seu caso de uso, ou finalidade desejada.

- Existem duas formas de efetuar essa validação:

### Automática
- Utiliza um modelo de avaliação pré-treinado (juiz) para avaliar a qualidade das respostas geradas pelo modelo de fundação.

- Permite atribuir tarefas pré-definidas ou não, como:
  - Resumos de textos
  - Perguntas e Respostas sobre determinado tópico
  - Geração de texto com resposta-alvo
  - Fornecer um dataset de prompts personalizados, para que o modelo responda

- Todas as respostas geradas serão comparadas com uma base de respostas de referências (que deve ser fornecida por você), e o modelo de avaliação irá atribuir uma pontuação para cada resposta gerada, com base na sua qualidade e aderência à resposta de referência.

- A pontuação é calculada automaticamente por meio de métricas pré-definidas, como:
  - Precisão
  - Utilidade
  - Coerência
  - Tonalidade
  - E métricas de responsabilidade, como:
    - Viés
    - Toxicidade
    - Segurança

- As métricas listadas acima são coletadas por meio da avaliação com base em métricas mais complexas, como:
  - **ROUGE**: mede a sobreposição de n-gramas entre a resposta gerada e a resposta de referência, avaliando a qualidade do texto gerado.
    - Falando de maneira não técnica, compara a resposta gerada com a resposta de referência, e atribui uma pontuação com base na quantidade de palavras ou frases que coincidem entre as duas respostas.
 
  - **BLUE**: Avalia a qualidade do texto gerado, considerando a precisão e a fluência da respota, penalizando respostas com erros gramaticais ou incoerentes. 
    - Especialmente útil para tarefas de tradução, onde a precisão e equivalência semântica é fundamental.

  - **BERTScore**: Compara a similaridade semântica entre a resposta gerada e a resposta de referência, utilizando embeddings de palavras para avaliar a qualidade do texto gerado.
    - Em outras palavras, transforma o texto em vetor numérico e compara a similaridade entre o vetor da resposta gerada e o vetor da resposta de referência.
    
    - Excelente para capturar nuances entre os dois textos.

### Manual
- Permite que você mesmo avalie as respostas geradas pelo modelo de fundação, atribuindo uma pontuação manualmente.

- A avaliação pode ser feita por você mesmo ou por avaliadores da própria AWS, que irão avaliar as respostas com base em critérios pré-definidos.

- O feedback da resposta pode ser fornecido em formato de joinhas (like/dislike) ou na escala likert (1 a 5 estrelas).