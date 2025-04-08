Anotações avançadas sobre o funcionamento do IAM para a certificação Security Specialty.
## Principals
- "Principal" é o usuário/entidade/aplicação que faz uma requisição para um recurso da AWS
- A requisição pode realizar uma **action** ou uma **operation** em cima de um recurso da AWS.

## Policies
- Temos dois tipos de policies:
	- **Identity-based**: Podem ser aplicadas a usuários, grupos e roles.
	- **Resource-based**: São aplicados dentro de recursos da AWS, como buckets do S3, Filas do SQS, chaves do KMS, etc.
- Todas as permissões são negadas implicitamente por padrão.
## Roles
- Uma role é uma identidade do IAM que possui permissões específicas.
- Elas podem ser assumidas por usuários, aplicações e recursos AWS.
___
## MFA
- O Multi-factor authentication é um processo extra de autenticação, no qual é gerado um TOTP (Time-based one-time password).
- O MFA Virtual da AWS pode ser configurado em qualquer software de autenticação, como o Google Authenticator, que é o que eu uso.
- O **MFA Físico** já é um pouco mais complicado, baseia-se no uso de um dispositivo de geração de tokens físico, que é fornecido por terceiros, e não pela própria AWS, por conta disso ele ==sai mais caro==. Porém é mais seguro, visto que ele pode ser escondido fisicamente.
___
## STS (Security Token Service)
- **Utilizado para definir chaves de acessos temporárias para uma entidade.**
- Utiliza session tokens para controlar as credenciais temporárias.
- São utilizadas com:
	- **Identity Federation** (AD, por exemplo);
	- **Delegação**;
	- **Acessos cross-account;
	- **Roles IAM.**

## Password Policy
- Em Account Settings, no IAM, é possível definir uma política de senha própria para os usuários da conta, podemos estabelecer:
	- Mínimo de caracteres
	- Pelo menos 1 maiúsculos e minúsculos
	- Pelo menos 1 número
	- Pelo menos 1 caractere especial
	- Expiração de senha (E se isso requer um reset do administrador)
	- ==Proibição dos usuários mudarem a própria senha==
	- ==Proibição da reutilização de senha.==

___
## IAM Access Analyzer
- Este é um serviço muito útil para controlar recursos que são compartilhados externamente, como buckets, Roles, Chaves do KMS etc.

- Através dele, ==é possível definir uma **ZoneofTrust**, que especifica contas AWS de confiança,== que podem acessar o recurso.
	- ==Após o estabelecimento da ZoneofTrust, todos os acessos vindos de entidades que não estão listados nela serão reportados como findings.==

![[IAMAccessAnalyzer.png]]
___
# OBSERVAÇÕES
- É possível criar até 5000 usuários em uma conta AWS.
- Quando criado, um usuário não tem permissão de fazer nada, você deve atribuir permissões a ele.