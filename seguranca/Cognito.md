Você já sabe que o Cognito é um ==serviço que implementa de maneira facilitada o gerenciamento de registro e login de usuários em uma aplicação.== Mas, vejamos neste arquivo alguns detalhes avançados sobre este serviço.
___
## O que é Identity Federation?
- O Identity Federation nos permite utilizar outros sistemas de autenticação, chamados IDPs - Identity Providers, para dar acesso temporário à conta AWS para colaboradores ou clientes de nossa aplicação, sem precisar criar um usuário IAM para cada pessoa.
### Como Funciona?
1. O usuário faz login no **sistema externo** (ex: Google, Facebook, AD, etc.)
2. Esse sistema, chamado de IdP, Identity Provider, confirma que o usuários está autenticado.
3. A AWS confia nesse sistema e emite **credenciais temporárias** através do [**STS**](STS.md), dando acesso aos recursos definidos na conta AWS.

___
## User Pools
- O **Cognito User Pools (CUP)** ==permite que você possa manter uma base de dados serverless dos usuários da sua aplicação== web ou mobile.

- Permite atribuir MFA aos usuários

- Verificação de email ou telefone.

- Identidade Federada: Usuários podem logar com suas conta do Facebook, Google, ou serviço com SAML.

- Gera um JSON Web Token (JWT) ao autenticar o usuário com os tokens:
	- **ID Token**: Informações sobre o usuário autenticado.
	- **Access Token**: Permissões para acessar APIs protegidas.
	- **Refresh Token**: Utilizado para obter novos tokens de acesso.

- **User Groups**: ==Os User Groups nas User Pools permitem organizar usuários de forma lógica e associar permissões específicas baseadas em seus grupos.== Isso simplifica o gerenciamento de acesso e autorizações, especialmente em cenários onde diferentes níveis de permissões são necessários para grupos distintos de usuários.

### Integrações
- É possível integrar o CUP com o **API Gateway** e também com o **Application Load Balancer**

___
## Identity Pools (Federated Identities)
- Atribui credenciais temporárias da AWS para usuários da aplicação.

- Em uma Identity Pool podemos incluir:
	- **Provedores públicos** (Login com Facebook, Google, Apple, etc.)
	- Usuários que já estão em um **User Pool**.
	- Provedores de identidade **SAML ou OpenID Connect**.
	- Sistema de autenticação customizada (A qual está inclusa na aplicação do desenvolvedor que usará o Cognito).

- ==Através do Identity Pool, podemos permitir o acesso temporário de guests/anônimos==.

- Após pegar uma credencial temporário pelo Identity Pool, os usuários poderão acessar os serviços AWS diretamente, ou então através do API Gateway.
	- ==As policies aplicadas aos usuários são definidas no próprio Cognito.==

![[IdentityPoolsDiagram.png]]

## Anotações
- Você pode utilizar um domínio próprio para autenticar usuários no Cognito (ao invés do domínio padrão `amazoncognito.com`). [¹](https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-user-pools-add-custom-domain.html#cognito-user-pools-add-custom-domain-console-step-1)
	- Para isto, é um requisito que você já tenha um certificado configurado no ACM na região `us-east-1` (pois ocorrerá a criação automática de uma distribuição do Cloudfront.
	- Após isso, acesse o console do, vá até a aba "**Domain**" no console do Cognito e selecione "**Create custom domain**".