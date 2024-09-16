# Revisões - ECS
Aqui estão algumas perguntas sobre ECS e containerização que eu errei no simulado.

- <span style="background-color:red; color:#fff"> Em vermelho, a resposta que eu assinalei.</span>

- <span style="background-color:green; color:#fff">Em verde, a reposta correta.
</span>

## Acessando Outros Serviços
_**An application running on an Amazon ECS container instance using the EC2 launch type needs permissions to write data to Amazon DynamoDB.
<br>
How can you assign these permissions only to the specific ECS task that is running the application?**_

- [ ] Modify the AmazonECSTaskExecutionRolePolicy policy to add permissions for DynamoDB

- [ ] <span style="background-color:green; color:#fff"> Create an IAM policy with permissions to DynamoDB and assign It to a task using the taskRoleArn parameter
</span>

- [ ] Use a security group to allow outbound connections to DynamoDB and assign it to the container instance


- [X] <span style="background-color:red; color:#fff"> Create an IAM policy with permissions to DynamoDB and attach it to the container instance</span>

### Explicação
Para especificar permissões para uma task específica no ECS você pode utilzar o _IAM Roles for Tasks_. A política de permissão pode ser aplicada a determinadas tasks quando estiver realizando a definição delas. o `taskRoleArn` é utilizado para específicar a política.<br>

- **O meu erro**: Não se deve aplicar uma permissão para toda a instância do container, pois dessa forma todas as tasks ficarão com permissão de acessar os serviços.

_**Read the docs**_: [Task IAM Roles](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/task-iam-roles.html)