# Questões Sobre Arquitetura Segura
Neste arquivo estão questões que eu errei sobre o design de arquiteturas seguras.

___
## <span style="background-color:#fff; color:blue"> Criptografia SSL/TLS em RDS
</span>

_**"A company uses an Amazon RDS MySQL database instance to store customer order data. The security team have requested that SSL/TLS encryption in transit must be used for encrypting connections to the database from application servers. The data in the database is currently encrypted at rest using an AWS KMS key."**_

- [ ] <span style="background-color:green; color:#fff"> A. Download the AWS-provided root certificates. Use the certificates when connecting to the RDS DB instance.
</span>

- [x] <span style="background-color:red;color:#fff">B. Take a snapshot of the RDS instance. Restore the snapshot to a new instance with en cryption in transit enabled.</span> 

- [ ] C. Add a self-signed certificate to the RDS DB instance. Use the certificates in all connections to the RDS DB instance.

- [ ] D. Enable encryption in transit using the RDS Management console and obtain a key using AWS KMS.

### **Explicação**
Não há necessidade de criar uma snapshot da instâncias RDS e recriá-la, já que um certificado para criptografia é criado quando as instâncias de BD são bootadas no RDS.

_Read The Docs:_ [Using SSL/TLS to encrypt a connection to a DB instance](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/UsingWithRDS.SSL.html).

___
## <span style="color:blue; background-color:#fff">Permissão de Acesso do Container</span>


_**An application running on an Amazon ECS container instance using the EC2 launch type needs permissions to write data to Amazon DynamoDB. How can you assign these permissions only to the specific ECS task that is running the application?**_

- [ ] Modify the AmazonECSTaskExecutionRolePolicy policy to add permissions for DynamoDB

- [ ] <span style="background-color:green; color:#fff"> Create an IAM policy with permissions to DynamoDB and assign It to a task using the taskRoleArn parameter
</span>

- [ ] Use a security group to allow outbound connections to DynamoDB and assign it to the container instance


- [X] <span style="background-color:red; color:#fff"> Create an IAM policy with permissions to DynamoDB and attach it to the container instance</span>

### Explicação
Para especificar permissões para uma task específica no ECS você pode utilzar o _IAM Roles for Tasks_. A política de permissão pode ser aplicada a determinadas tasks quando estiver realizando a definição delas. o `taskRoleArn` é utilizado para específicar a política.<br>

- **O meu erro**: Não se deve aplicar uma permissão para toda a instância do container, pois dessa forma todas as tasks ficarão com permissão de acessar os serviços.

_**Read the docs**_: [Task IAM Roles](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/task-iam-roles.html)

___
## <span style="color:blue; background-color:#fff">Criptografia de Read Replica</span>

_**An Amazon RDS Read Replica is being deployed in a separate region. The master database is not encrypted but all data in the new region must be encrypted. <br>How can this be achieved?**_

- [ ] <span style="background-color:green; color:#fff">Encrypt a snapshot from the master DB instance, create a new encrypted master DB instance, and then create an encrypted cross-region Read Replica</span> 

- [ ] Enable encryption using Key Management Service (KMS) when creating the cross-region Read Replica

- [ ] Enabled encryption on the master DB instance, then create an encrypted cross-region Read Replica

- [X] <span style="background-color:red; color:#fff"> Encrypt a snapshot from the master DB instance, create an encrypted cross-region Read Replica from the snapshot</span>

### Explicação
Não é possível criar uma read replica criptografada de um DB master. Também não é possível habilitar a criptografia depois que o master DB já foi inicializado. <br>
Por conta disso, é preciso criar um novo master DB a partir de um snapshot do DB existente, daí é só criptografar e criar um CR Read Replica desse (novo) master DB.

**Meu erro**: A opção que eu assinalei está quase certa, Faltou só um detalhe: É preciso que o master DB  também seja criptografado e não só a CR Read Replica.

___

## <span style="color:blue; background-color:#fff">Variáveis de Ambiente na Lambda</span>

**_You are a solutions architect working for a social media company that provides a place for civil discussion of political and news-related events. Due to the constantly changing regulatory requirements and restrictions, you need to build your app in a way that allows you to modify configurations instantly without changing the Lambda function code. You have chosen to build the REST API endpoints used by your social media app user interface code using Lambda. How can you securely configure your Lambda functions without updating code? (Select TWO)_**


- [X] Pass environment variables to your Lambda function via the request header sent to your API Gateway methods.
- [ ] <span style="background-color:green; color:#fff"> Configure your Lambda functions to use key configuration.</span>
- [ ] <span style="background-color:green; color:#fff"> Use encryption helpers.
</span>
- [ ] Use Lambda layers.
- [ ] Use Lambda aliases.


### **Explicação**
- Passar variáveis de ambiente no header da requisição iria expor as variáveis como plain text, isso é uma falha de segurança gravíssima. 

- A melhor opção é utilizar uma key criada no KMS para criptografia da função (opção B) e então realizar a criptografia das variáveis de ambiente com a opção _encryption helpers_.

- Um detalhe interessante é que, com o encryption helpe/rs, as variáveis são criptografadas antes mesmo de chegarem a Lambda. (Quase um client-side encryption)

___
## <span style="color:blue; background-color:#fff">SCPs no Organizations</span>
An AWS Organization has the below hierarchy of OUs:

Root -> Project_OU -> Dev_OU

The root is attached to the default SCP.

Project_OU is attached to an SCP that prevents users from deleting VPC Flow Logs.

Dev_OU has an SCP that allows the action of "ec2:DeleteFlowLogs"

Are the IAM Users/Roles in Dev_OU allowed to delete VPC Flow Logs?

- [x] It is permitted because the SCP in Dev_OU allows it.
- [ ] It is allowed because the Root has the default SCP that allows all actions
- [ ] <span style="background-color:green; color:#fff">It is not allowed as the SCP in Project_OU restrics the action.</span>
- [ ] It is not allowed as the default SCP in Root denies the action.

### **Explicação**
As SCPs seguem uma estrutura hierárquica dentro da organização. Isso significa que as políticas que você aplica em uma **OU superior (Parent OU)** se aplicam **automaticamente** às **OUs subordinadas (Child OUs)**.
- Em suma, ==Deny sempre tem prioridade sobre Allow==;