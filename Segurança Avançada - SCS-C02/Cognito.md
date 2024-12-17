Você já sabe que o Cognito é um ==serviço que implementa de maneira facilitada o gerenciamento de registro e login de usuários em uma aplicação.== Mas vamos ver alguns detalhes avançados sobre este serviço:

## User Pools
- O **Cognito User Pools (CUP)** ==permite que você possa manter uma base de dados serverless dos usuários da sua aplicação== web ou mobile.

- Permite atribuir MFA aos usuários

- Verificação de email ou telefone.

- Identidade Federada: Usuários podem logar com suas conta do Facebook, Google, ou serviço com SAML.

### Integrações do CUP
- É possível integrar o CUP com o **API Gateway** e também com o **Application Load Balancer**
___
## Identity Pools (Federated Identities)
- Atribui credenciais temporárias da AWS para usuários da aplicação.

- Em uma Identity Pool podemos incluir:
	- Provedores públicos (Login com Facebook, Google, Apple, etc.)
	- Usuários que já estão em um User Pool.
	- Provedores de identidade SAML ou OpenID Connect.
	- Sistema de autenticação customizada (A qual está inclusa na aplicação do desenvolvedor que usará o Cognito).

- Através do Identity Pool, podemos permitir o acesso temporário de guests/anônimos.

- Após pegar uma credencial temporário pelo Identity Pool, os usuários poderão acessar os serviços AWS diretamente, ou então através do API Gateway.
	- ==As policies aplicadas aos usuários são definidas no próprio cognito.==

![[IdentityPoolsDiagram.png]]