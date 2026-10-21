# AWS Lake Formation

- O Lake Formation é um serviço da AWS que facilita a configuração de um data lake seguro. Ele permite que você centralize e gerencie dados de diferentes fontes, aplique políticas de segurança e controle de acesso, e simplifique a análise de dados em grande escala.

- Ele se integra com o S3, Glue, Athena e outros serviços da AWS, permitindo que você gerencie e analise dados de forma eficiente e segura.

## Principais Funcionalidades

- Centralização e gerenciamento de dados de diferentes fontes.

- Aplicação de políticas de segurança e controle de acesso.
  - O controle de acesso pode ser feito em nível de tabela, coluna ou linha, garantindo que apenas usuários autorizados possam acessar os dados sensíveis.

- Ele é muito utilizado em conjunto com o S3 e o Athena para gerenciamento seguro de Data Lake.

- Integração com os serviços:
  - S3
  - Glue
  - Athena
  - Redshift Spectrum
  - EMR
  - QuickSight
  - SageMaker

## Etapas para Configuração

- Primeiramente, você deve registrar o recurso desejado como um Data Location no Lake Formation.
- Em seguida, você deve criar um catálogo de dados no Glue e registrar as tabelas que deseja gerenciar.
- Após isso, configure as permissões de acesso para os usuários e grupos (que podem ser usuários individuais ou grupos do IAM) no Lake Formation.