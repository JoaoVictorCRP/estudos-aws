Os serviços de diretório é um tema bem comum no exame Security Specialty, especialmente o **Microsoft Active Directory** e sua integração com a AWS. Vejamos alguns detalhes:

## Microsoft AD
- É encontrado em qualquer Windows Server com serviços de domínio AD.

- ==Fornece uma maneira centralizada de gerir objetos de um ecossistema empresarial==, são considerados "objetos":
	- Usuários e contas;
	- Computadores;
	- Impressoras;
	- Arquivos Compartilhados, etc.

- Objetos do AD são organizados em árvores. Um grupo de árvores é chamado floresta.

## ADFS
- O ==AD Federation Services permite SSO em várias aplicações.==
- **Integração SAML com** terceiros como: **o console AWS**, DropBox, Office 365, etc...

## Serviços de Diretório Na AWS

### AWS Managed Microsoft AD
- Permite criar ==seu próprio AD na AWS==, gerenciando usuários localmente;
- Suporta MFA;
- ==É possível estabelecer uma conexão com um AD on-premise.==

### AD Connector
- ==Atua como um proxy== para redirecionar para um AD on-premise;
- suporta MFA;
- Os usuários são gerenciados no AD on-premise

### Simple AD
- Serviço de diretório gerenciado **compatível** com o da Microsoft.
- ==Não pode ser integrado com um AD on-prem==.
- Mais simples e mais barato.
- Compatível com o Samba.

# **ANOTAÇÕES**
- Para estabelecer uma conexão entre um AD na nuvem e um AD on-premise, é necessário **estabelecer um Direct Connect ou uma conexão VPN**.