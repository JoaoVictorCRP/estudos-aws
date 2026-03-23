# Amazon Bedrock

- O Bedrock é um seviço de IA generativa totalmente gerenciado, ele fornece uma interface de aceesso a diversos ([modelos de fundação](../certificacoes/ai-practitioner/foundation-models.md)), como Claude, Llama, Stable Diffusion, Titan e muito mais.

- O modelo de custo é pay-per-use, portanto você só é cobrado pelas requisições e quantidade de tokens processados.

## Modelos de Fundação

- Como dito anteriormente, diversos modelos de fundação estão disponíveis no Bedrock.

- É importante esclarecermos que os modelos usados na sua conta AWS pertencem a você, e nenhum dado ou informação processados por eles serão usados para treinamento do modelo de fundação.

  - Isso torna as aplicações construídas com o Amazon Bedrock extremamente seguras para o uso corporativo, já que nenhuma regra ou segredo de negócio será usada para retreinar o modelo, **como ocorre em IAs públicas.**