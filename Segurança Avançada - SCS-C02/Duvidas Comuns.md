
## IAM Roles vs Resource-Based Policies
Ambos podem ser utilizados para fornecer acesso de um usuário, de uma conta X, a um recurso em uma conta Y. Porém, há algumas diferenças:

- **Roles**: A entidade que assume a role renuncia temporariamente de suas permissões para aderir somente às permissões que a Role garante.

- **Resource-Based Policies**: Permite que o usuário possa manter suas permissões enquanto acessa o recurso, dado o fato de que a permissão está atrelada ao recurso, e não ao usuário.

**Exemplo**: "O usuário 'Joãozinho' da _conta A_ deseja fazer uma consulta em uma tabela do DynamoDB e enviar um dump dela para um bucket na _conta B_.  Como devemos permitir o acesso do Joãozinho?"

Nesse caso, a melhor opção é liberar o acesso através de uma bucket policy que dá o acesso para o Joãozinho. 

```json
{ 
	"Effect": "Allow", 
	"Principal": { 
		"AWS": "arn:aws:iam::<idContaA>:user/joaozinho" 
	},
	"Action": "s3:PutObject",
	"Resource": "arn:aws:s3:::bucket-da-conta-b/*" 
}
```


## ABAC vs RBAC

- **Role-Based Access Control (RBAC)**
	- Estratégia baseada em controlar acessos pelas funções que os usuários de cada departamento tem acesso.
	- Permite implementar permissões granulares, que concedem acesso somente a recursos específicos de um serviço.
	- Exemplo: Administrativo, DBA, Desenvolvedor
	- **DESVANTAGEM:** Precisará atualizar a policy quando criar um recurso.

- **Attribute-Based Access Control (ABAC)**
	- Estratégia baseada em controlar acessos baseados nas tags (atributos) do usuário ou do recurso.
	- Permissões garantidas automaticamente, pois tudo é baseado no atributo.
	- Requer a criação de menos policies.
	- ==É possível obter os atributos dos usuários que estiverem acessando através de um diretório corporativo (SAML 2.0, IdP).==



## IMDSv1 vs. IMDSv2
IMDS, Instance Metadata Service, é a forma como AWS denomina a obtenção de metadados de uma instância enquanto dentro dela. Temos duas versões do IMDS. Sendo eles: 

- **IMDSv1**: Método baseado em solicitação/resposta. Nesta versão é que ocorre ==o clássico acesso direto com `curl http://169.254.169.254/latest/meta-data`.==

- **IMDSv2**: Método orientado a sessões utilizando tokens, garante maior segurança. Ele é feito em dois passos. Primeiro você obtém o token:
```bash 
$ TOKEN=curl -X PUT "http://169.254.169.254/latest/api/token" -H "X-aws-ec2-metadata-token-ttl-seconds: 21600" \ && curl -H "X-aws-ec2-metadata-token: $TOKEN" http://169.254.169.254/
```
	- Depois, você faz a requisição, passando o token como um Header:
```bash 
$ curl http://169.254.169.254/latest/meta-data/reservation-id -H "X-aws-ec2-metadata-token: $TOKEN" 
```

- **Para forçar forçar a obtenção de metadados apenas via IMDSv2, é possível definir utilizar um Automation Document do SSM**, a partir dele, selecione a opção `EnforceIMDSv2` como `required`. 

	- Também é possível forçar o IMDSv2 através da CLI, basta utilizar o comando de modificação de metadata, veja um exemplo: `aws ec2 modify-instance-metadata-options --instance-id i-abc123456789 --http-tokens required --http-endpoint enabled` **(Repare como http-tokens é definido como required).**

## Cognito User Pools x Cognito Identity Pools

- O **Cognito User Pools** funciona como uma **"base de dados serverless"** para armazenar dados de autenticação dos usuários finais da aplicação, tudo de maneira totalmente gerenciada. ==**Pensou em CUP? Pensou em AUTENTICAÇÃO.**==


- O **Cognito Identity Pools** é utilizado para forncer **autorização** e acesso temporário a recursos da AWS (ex: S3, DynamoDB, Lamb) utilizando **Roles.** ==**Pensou em CIP? Pensou em AUTORIZAÇÃO**==.
	- Os usuários podem vir do **CUP**, de **IDPs** ou mesmo ser um login anônimo.


## SCPs x RBPs
No AWS Organizations temos duas formas de exercer controle sob uma organização, podemos utilizar **Service Control Policies (SCPs)** ou **Resource-Based Policies (RBPs)**. Vejamos as diferenças

#### Service Control Policies (SCPs)
- São políticas ==aplicadas a nível da conta ou organização==.

- Servem como **limite de permissão**.

- São **aplicadas em OUs.**

- ==**Não concede permissões por si só**, mas **restringe** permissões concedidas== em políticas IAM ou outras políticas dentro da conta.

- **Restringem ações do IAM**.

#### Resource-Based Policies
- Tipo de política que permite controlar quais recursos podem ser criados ou utilizados em uma conta, com base em condições como **tags** e **atributos de recurso**.

- Enquanto as **SCPs** restringem **ações** de IAM, as **RCPs** restringem **recursos** que podem ser utilizados ou configurados, adicionando uma camada extra de controle.

- **Restringem configurações específicas de um recurso**.


## Root CA x Subordinate CA (AWS Private CA)

### Root CA
- A **Root CA** é autoridade certificadora principal, no topo da hierarquia de confiança.

- É **autossuficiente**, pois assina seu próprio certificado

- ==**Única entidade confiável** na hierarquia de CA==, pois todas as subordinate CAs e os certificados finais derivam dela.

- É ela quem ==emite certificados para as subordinate CAs.==

- **Não é recomendada para emissão direta de certificados,** para isso use uma subordinate.

## Subordinate CA 
- Opera sob a autoridade de uma **Root CA**.

- Seu certificado digital é assinado pela Root CA **ou** por outra Subordinate CA.

- É a responsável pela emissão de certificados para usuários, recursos e dispositivos.

##### 🌟É Possível Criar uma Subordinate CA Sem Ter uma Root CA?

- ==**Sim**==, é possível criar uma Subordinate CA sem ter uma Root CA na AWS Private CA, ==**mas você precisa de uma Root CA externa para assinar o certificado da Subordinate CA**.==
