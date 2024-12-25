- Uma **Session Policy** é uma ==política temporária que você pode passar como parâmetro quando usa a API **`AssumeRole`**== (ou outra API que gera credenciais temporárias, como **`AssumeRoleWithSAML`** ou **`AssumeRoleWithWebIdentity`**).

- ==Essa política é usada para **limitar ainda mais** as permissões que a Role assumida já concede==, funcionado como uma "camada extra de segurança".

- **O Óbvio:** A Session Policy não pode conceder permissões fora do que já está permitido pela política da Role. Ela apenas serve como restrição! Veja o diagrama abaixo:
	![[PermissaoEfetiva-session-rbp-id.png]]
	- A session policy deve ser condizente com a identity-based policy que pertence a role e também com resource-based policies, caso envolvidas.