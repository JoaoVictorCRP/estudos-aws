# CodePipeline

- O CodePipeline é o serviço de orquestração (visual) de CI/CD na AWS.

- Nele podemos definir as fases envolvidas na integração e entrega contínua do código:
  - Source
  - Build
  - Test
  - Deploy 
  - Invoke

- Os estágio podem ser sequenciais ou paralelos.

## Artefatos
- Cada estágio da pipeline gera artefatos de saída, que são armazendos em um bucket S3 dedicado à pipeline.

  - Os artefatos de saída de um estágio são usados como artefatos de entrada pelo seu sucessor.

## Disparando uma Pipeline
Para além do disparo manual, a execução de uma pipeline pode acontecer de três maneiras:

- **Events**: Através de um evento lançado por um serviço da AWS, que é registrado no EventBridge. (Ex: Commit em repositório do Codecommit; Commit em repositório do GitHub conectado com Codetar Connection).

- **Webhooks**: Nesta opção podemos usar o endpoint HTTP fornecido pelo codepipeline para executar um script que envia uma requisição e dispara e inicia a execução da pipeline.

- **Pooling**: Nessa modalidade, o CodePipeline fará checks regulares no repositório para verificar se houveram mudanças.

