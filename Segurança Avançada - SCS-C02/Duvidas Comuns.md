
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