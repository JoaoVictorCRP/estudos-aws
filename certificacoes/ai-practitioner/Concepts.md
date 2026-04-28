# Conceitos de GenAI

## Tokenization
- A tokenização é o processo de converter texto puro em uma sequência de tokens, que são as unidades básicas de texto que os modelos de linguagem processam.
  - Os tokens podem ser palavras, subpalavras ou caracteres, dependendo do modelo e da técnica de tokenização utilizada.
  
- A tokenização é fundamental para o funcionamento dos modelos de linguagem, pois permite que eles compreendam e processem o texto de maneira eficiente.

- Você pode obter a quantidade de tokens de um texto usando a API de tokenização do modelo (**Tokenizer**), o que é útil para entender o custo e a eficiência do processamento.
  - O Bedrock também possui a funcionalidade de Tokenização para os modelos de fundação que ele oferece.

## Context Window
- A janela de contexto (context window) é o número máximo de tokens que um modelo pode processar de uma vez ao gerar uma resposta.
  - Quanto maior a janela de contexto, mais informações o modelo pode considerar ao gerar a resposta, portanto maior será a coerência.

## Embedding
- O embedding é uma técnica de representação de texto em um espaço vetorial, onde palavras, frases ou documentos são convertidos em vetores numéricos que capturam o significado semântico do texto.
  - Os modelos de embeddings são treinados para criar essas representações vetoriais, permitindo que o modelo compreenda as relações semânticas entre diferentes palavras ou frases.

- Para além de transformar texto em vetores númericos, os embeddings são úteis para capturar outras informações, como o sentido semântico, a sintaxe e o sentimento expresso no texto, o que os torna uma ferramenta poderosa para tarefas de processamento de linguagem natural (NLP).

- Uma outra vantagem de vetorizar textos é o fato de que ele facilita a busca e a recuperação de informações, permitindo que o modelo correlacione palavras ou frases semelhantes, mesmo que não sejam idênticas.