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