O IAM Identity Center é um serviço de gerenciamento de acessos que é muito recomendado pela AWS para utilizar em cenários onde se lida com múltiplas contas em uma organização. Sabe por quê? Porque ele é um serviço **SSO (Single-Sign On)**, diferentemente do IAM convencional.

Anteriormente, este serviço era chamado de AWS SSO, inclusive.

## Features
- Gerenciamento centralizado de múltiplas contas e aplicações.

- Integração com outros serviços em nuvem e login corporativo (Salesforce, Zoho, AD etc.)

- Painel de login único para acessar as diversas contas de uma organização.

- Complexidade reduzida em relação ao IAM tradicional, se você precisa lidar com o acesso de pessoas reais à sua conta AWS, é totalmente recomendável usar o Identity Center.

## Controlando Permissões
- Para controlar permissões no Identity Center, nós utilizamos os **Permission Sets**.

- ==Um **Permission Set** é uma coleção de uma ou mais policies do IAM que podem ser atreladas a usuários ou grupos para a definição de acesso.==

- Um **Permission Set** está atrelado a uma conta e um usuário, descrevendo quais permissões este usuário tem naquela conta.


