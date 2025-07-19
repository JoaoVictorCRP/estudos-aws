
- Serviço gerenciado para ==transferência de arquivos para dentro e para fora do S3 ou do EFS utilizando o protocolo FTP==.

- Útil para quando o caso de uso exige a utilização do **FTP, FTPS ou SFTP**.

- Infraestrutura gerenciada, escalável e de alta disponibiildade (Multi-AZ).

- Pagamento é realizado por endpoint + transferência de dados em GB.

- Autenticação dos usuários é gerenciada dentro do próprio serviço.
	- É possível integrar a autenticação com outros sistemas, como AD, LDAP, Okta, Cognito, dentre outros.

## Tipos de Endpoint
- **Público**
	- Acessível para toda a internet.
	- IP público gerenciado pela AWS.
	- ==Não é possível definir um filtro para IPs de origem autorizados==.
	
- **VPC Endpoint com acesso interno**
	- Acessível apenas dentro da VPC.
	- Acesso é feito de maneira privada por recursos na mesma VPC ou por redes físicas conectadas via VPN ou Direct Connect.
	- IPs privados estáticos.
	- Controle de acesso pode ser feito via SGs e NACLs.
	
- **VPC Endpoint com acesso para a internet**
	- Maneira híbrida de gerenciar o acesso ao endpoint.
	- IPs privados estáticos para acesso interno.
	- Permite a utilização de um Elastic IP no seu endpoint (IP público estático).
	- Controle de acesso através de Security Groups.
![[TransferFamily-EndpointTypes.png]]