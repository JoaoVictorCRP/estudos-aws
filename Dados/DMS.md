## Database Migration Service (DMS)
Este serviço oferece uma migração entre SGBDs de maneira altamente controlada e consisitente, <span style="background-color: #e0a800; color: black;font-weight:bold">toda a migração pode ser feita enquanto o banco de origem continua operacional</span>, o que faz com que os seus negócios não sejam afetados!

### Sobre a migração
Há dois tipos de migração:
- **Homogênea**, isto é, quando o schema do banco de origem é igual ao destino.
- **Heterogênea**: Quando o schema do banco de origem é diferente do destino. Nesse caso, é necessário utilizar o **AWS Schema Conversion Tool**.

### Origem e Destino
- A **origem** pode ser um banco On Premise, hospeado em EC2 ou no RDS.
- O **destino** pode ser o RDS ou uma EC2.

### Outras funcionalidades
- **Migração para DB de testes**: Útil para copiar uma base de dados de produção para o ambiente de testes, com o objetivo de realizar homologações.

- **Consolidação de DB:** Quando se possui várias base de dados e precisa unificar todas elas em uma única base de dados central.

- **Replicação contínua**: Utilizado para replicação automática da base de dados, visando recuperação de desastres ou separação geográfica.
### Segurança
- Criptografado usando KMS (Encryption at rest)
- Permite utilização de VPN site-to-site
- Suporta policies e roles do IAM
- Opção de acesso granulado (permitir somente determinadas funções para cada usuário)
- Monitorável com CloudWatch e CloudTrail