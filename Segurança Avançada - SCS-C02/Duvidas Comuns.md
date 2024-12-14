
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