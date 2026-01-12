# AWS SAM

- O SAM (Serverless Application Model) é um framework open-source para construção de aplicações serverless na AWS.

- Ele simplifica o processo de desenvolvimento, teste e implantação de funções Lambda, APIs, bancos de dados e outros recursos serverless, permitindo inclusive que você rode a aplicação localmente para testes.

- Dá suporte para a construção de recursos serverless utilizando uma sintaxe simplificada baseada em YAML, que posteriormente é transformada em um template do CloudFormation.
  - Para que o template funcione corretamente, é necessário que a seguinte linha esteja presente no início do arquivo YAML:
    ```yaml
    Transform: 'AWS::Serverless-2016-10-31'
    ```
  - Caso ela não esteja presente, o CloudFormation não reconhecerá os recursos do SAM (Troubleshooting comum).

## Recursos suportados pelo SAM
- Funções Lambda
  - Definidos como `AWS::Serverless::Function` no YAML.

- APIs do API Gateway
  - Definidos como `AWS::Serverless::Api` no YAML.
  
- Tabelas do DynamoDB
  - Definidos como `AWS::Serverless::SimpleTable` no YAML.

## Empacotando e implantando com SAM CLI

- O SAM CLI é uma ferramenta de linha de comando que facilita o desenvolvimento, empacotamento e implantação de aplicações serverless.

- Com o SAM CLI, você pode:
  - Criar uma nova aplicação serverless a partir de templates pré-definidos (`sam init`).

  - Construir sua aplicação localmente, instalando dependências e preparando o código para implantação (`sam build`).

  - Empacotar sua aplicação, fazendo upload do código para um bucket S3 (`sam package`).

  - Implantar a aplicação na AWS, criando ou atualizando stacks do CloudFormation (`sam deploy`).

  - Sincronizar mudanças no código com a aplicação implantada (`sam sync`).
    - O Sam Sync atualiza automaticamente a aplicação na AWS, **sem a necessidade de implantar a stack via CloudFormation**.

  - Testar funções Lambda localmente (`sam local invoke`).

  - Depurar funções Lambda localmente (`sam local start-lambda`).

## Policy Templates do SAM
- O SAM oferece Policy Templates pré-definidos que facilitam a atribuição de permissões para funções Lambda, eliminando o overhead de criar políticas do IAM manualmente.

- Esses templates são definidos na seção `Policies` da definição da função Lambda no template do SAM.

- Alguns exemplos de Policy Templates disponíveis no SAM:
  - `AmazonDynamoDBReadOnlyAccess`: Concede permissões de leitura para tabelas do DynamoDB.
  - `AmazonS3ReadOnlyAccess`: Concede permissões de leitura para buckets do S3.
  - `DynamoDBCrudPolicy`: Concede permissões completas (CRUD) para uma tabela específica do DynamoDB.


## Deploy com SAM
- O SAM permite uso nativo do CodeDeploy para realizar deploys de aplicações serverless, garantindo implantações seguras e com rollback automático em caso de falhas. Para utilizar o CodeDeploy com SAM, é necessário definir uma seção `DeploymentPreference` na definição da função Lambda no template do SAM.
  
  - Sendo assim, é possível configurar estratégias de deploy como Canary ou Linear diretamente no template do SAM.

  - Também é possível configurar os Hooks do CodeDeploy para executar validações antes ou depois do deploy da aplicação serverless.
    - Os Hooks do SAM são nomeados `PreTraffic` e `PostTraffic`.

  - Rollback facilitado com apoio de alarmes do CloudWatch.