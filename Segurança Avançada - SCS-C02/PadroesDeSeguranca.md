Neste arquivo alguns detalhes sobre padrões de segurança, que costumam cair no exame SCS-C02

## OAuth/OpenID Connect (OIDC)
- **==Usado em cenários de login social, como "Entrar com o Google" ou "Entrar com o Facebook==**".

- **Identity Provider (IdP):** Nesse caso, o **Google** ou o **Facebook** vão atua como **IdP**, que é a aplicação/serviço responsável por fornecer um token de acesso para o aplicativo que está requisitando, com este token de acesso o app pode ter acesso a informações básicas do usuário.

- **Fluxo:** O aplicativo redireciona o usuário para o IdP (Google/Facebook), onde o usuário faz login. O IdP então emite um token de acesso que o aplicativo usa para autenticar o usuário e, se necessário, acessar seus dados.

## SAML (Security Assertion Markup Language)
- ==**Utilizado em cenários de autenticação corporativa**== ou em sistemas onde você faz login uma vez e tem acesso a vários serviços <ins>(Single Sign-On, ou SSO)</ins> É bem comum em ambientes empresariais.

- **Identity Provider (IdP)**: No caso do SAML, um provedor de identidade (que geralmente é algum provedor de SSO corporativo, um AD, por exemplo.) emite um um SAML assertion (mensagem XML) que são metadados do serviço que permitem realizar a validação do usuário.

- **Fluxo**: O usuário tenta acessar um serviço, como por exemplo o console da AWS, e é redirecionado para o IdP, onde faz o login. O IdP emite um então emite o SAML assertion que o serviço usa para autenticar o usuário.

[Vídeo Sobre SAML](https://www.youtube.com/watch?v=Ru3KfLCeEGY)
[Vídeo sobre OAuth](https://www.youtube.com/watch?v=ZV5yTm4pT8g)

## Anotações 

- Pensou em login corporativo para funcionários de uma empresa? Pensou SAML.
- Pensou em "login com o google" para usuários da sua aplicação? Pensou OAuth/OIDC.