## Resource-Based Policies vs Roles

- Ao lidar com acessos cross-account a recursos que oferecem opção de RBP, prefira utilizar os RBPs do que roles, pois elas são mais fáceis de gerenciar e limitam o escopo da permissão.

### Lista de Serviços que Suportam Resource-Based Policies

- **S3**: Permitir acesso a buckets ou objetos específicos.

- **Lambda**: Permitir que outras contas ou serviços invoquem uma função Lambda.

- **SQS**: Permitir que contas externas enviem mensagens para uma fila, ou leiam mensagens delas.

- **SNS**: Permitir que outras contas ou serviços PUBLIQUEM mensagens em um tópico.

- **KMS**: Permitir que uma chave KMS seja usada para criptografar dados em uma conta diferente.

- **ECR**: Permitir que contas externas acessem repositórios para **push** ou **pull** de imagens Docker.

- **Secrets Manager**: Permitir que outras contas ou serviços acessem segredos específicos (ex: Credencial de banco de dados).

### Quando Roles Podem Ser Mais Adequadas?

- Cenários de acesso a múltiplos recursos/serviços.
- Cenários de acesso temporário.
- Cenários onde a troca de contexto total da conta é exigido.