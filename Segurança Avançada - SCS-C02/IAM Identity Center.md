O IAM Identity Center é um serviço de gerenciamento de acessos que é muito recomendado pela AWS para utilizar em cenários onde se lida com múltiplas contas em uma organização. Sabe por quê? Porque ele é um serviço **SSO (Single-Sign On)**, diferentemente do IAM convencional.

Anteriormente, este serviço era chamado de AWS SSO, inclusive.

## Features
- Gerenciamento centralizado de múltiplas contas e aplicações.

- **Integração direta com outros serviços em nuvem, login corporativo e IDPs**, como AD, Google Workspace, Zoho, etc., usando protocolos como **SAML 2.0** e **OIDC**.

- Painel de login único para acessar as diversas contas de uma organização.

- Complexidade reduzida em relação ao IAM tradicional, se você precisa lidar com o acesso de pessoas reais à sua conta AWS, é totalmente recomendável usar o Identity Center.

## Controlando Permissões
- Para controlar permissões no Identity Center, nós utilizamos os **Permission Sets**.

- ==Um **Permission Set** é uma coleção de uma ou mais policies do IAM que podem ser atreladas a usuários ou grupos para a definição de acesso.== Eles podem incluir políticas gerenciadas pela AWS, gerenciadas pelo cliente, ou ambas.

- Um **Permission Set** está atrelado a uma conta e um usuário, descrevendo quais permissões este usuário tem naquela conta.


## ANOTAÇÕES
- ==O Identity Center deve ser ativado na conta root da organização==.

- ==O Identity Center só pode ser ativado em uma única região. (Não é um serviço global)==.