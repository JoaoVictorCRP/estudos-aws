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

  - ==É mandatório que o bucket S3 tenha versionamento habilitado==.

- Cenário Cross-Account (Deploy em outra conta):

  - **S3 Bucket Policy**: O bucket (na conta do Pipeline) deve ter uma policy permitindo s3:Get* e s3:Put* para a Role da conta de destino.

  - **KMS CMK (Mandatório):** Deve-se usar uma chave gerenciada pelo cliente (CMK). A chave padrão da AWS não funciona cross-account.

  - **Key Policy**: A policy da chave KMS deve conceder permissões para a Role da conta de destino.

  - **IAM Role (Conta Alvo)**: A role que fará o deploy na conta de destino deve ter permissão para descriptografar os dados usando a chave KMS que reside na conta do pipeline.

## Ações

- As fases da pipeline são compostos por ações, que são as tarefas executadas em cada estágio.

- Cada ação é associada a um provedor de serviço (CodeCommit, CodeBuild, CodeDeploy, etc), que define o que a ação faz.

- As ações podem executar em paralelo ou em sequência, dependendo da definição do valor do parâmetro **[`RunOrder`](https://docs.aws.amazon.com/codepipeline/latest/userguide/action-requirements.html#action.runOrder)**, ações com o mesmo valor de RunOrder executam em paralelo, ações com valores diferentes executam em sequência.
  - Ações sobre um mesmo runOrder são chamadas **Actions Groups**, e é desta maneira que este tópico é referido em exames de certificação.

## Disparando uma Pipeline
Para além do disparo manual, a execução de uma pipeline pode acontecer de três maneiras:

- **Events**: Através de um evento lançado por um serviço da AWS, que é registrado no EventBridge. (Ex: Commit em repositório do Codecommit; Commit em repositório do GitHub conectado com Codetar Connection).

- **Webhooks**: Nesta opção podemos usar o endpoint HTTP fornecido pelo codepipeline para executar um script que envia uma requisição e dispara e inicia a execução da pipeline.

- **Pooling**: Nessa modalidade, o CodePipeline fará checks regulares no repositório para verificar se houveram mudanças. Este é um método depreciado e não recomendado, pois gera custos adicionais e é menos eficiente que os outros dois.