O Security Token Service é o serviço que ==garante acesso a recursos **AWS POR TEMPO LIMITADO** a uma determinada entidade==.

- As ==credenciais temporárias do STS podem ser válidas de 15 minutos a 1 hora==, de acordo com as configurações.

- Para que a entidade possa ter acesso a role, ela deve ter a permissão de **AssumeRole**.

- Pode ser utilizado para acessos cross acount, em um modelo **RBAC** (Role Based Access Control)

- É possível dar acesso temporário para usuários logados via SAML com a API **AssumeRoleWithSAML**.
	
	- Além do SAML, também é possível fazer isso com Web IdP (Web Identity Providers) com a **AssumeRoleWithWebIdentity**. ==Isso no entanto, não é recomendado pela AWS, nesse caso, prefira usar o cognito.==