# Serviços Menores
Arquivo de anotações de serviços menores que costumam cair no CLF-02 (Cloud Practitioner).

## Segurança 🔑
### CloudHSM
- Serviço de criptografia para criação e gerenciamento de Hardware Security Modules (HSMs), diferentemente do KMS, esse serviço NÃO é gerenciado pela AWS.

### Certificate Manager
- Permite a <span style="background-color: #e0a800; color: black;font-weight:bold">criação e gerenciamento de certificados digitais que são utilizados para criptografar os dados entre os usuários e os servidores.</span>

### Security Hub
- Oferece uma interface facilmente utilizável dos alertas de segurança e outros detalhes relacionados ao acesso a serviços e outras aplicações de terceiros.

### Inspector
- Verifica instâncias, containers e funções lambda em busca de vulnerabilidades e exposição não intencional de dados da rede.

### Shield
- Oferece proteção contra ataques DDOS

### GuardDuty
- Serviço de detecção de ameaças e comportamentos suspeitos por parte de usuários da conta AWS.

## Organizacional 🏨
### Workspaces Web
- Serviço de desktop virtual que permite às organizações criar ambientes de trabalho na nuvem, oferecendo <span style="background-color: #e0a800; color: black;font-weight:bold">acesso remoto seguro a desktops direto pelo naveagador.</span>

### AppFlow
- <span style="background-color: #e0a800; color: black;font-weight:bold">Solução gerenciada que facilita a transferência segura de dados entre aplicativos SaaS e serviços da AWS.</span> Oferece integração com plataformas como Salesforce, Zendesk, Slack e ServiceNow.

## Desenvolvimento 🖥️
### CodeStar
- Oferece uma interface unificada para desenvolvimento, construção e deploy de aplicações rapidamente, basicamente o LightSail da programação.


### CodeCommit
- Repositório remoto git.

### CodeBuild
- Utilizado para automação, compilação e testes nas mudanças no código de um ambiente de CI.

### CodeDeploy
- Serviço de automação de deploys para alvos computacionais (EC2, Lambda, ECS, etc).

### CodePipeline
- Usado para orquestração e automtização da entrega de software. Pode incluir o CodeBuild como um step, mas é focado no processo completo de CI/CD, não só a contrução do software.


### Amplify
- Framework de desenvolvimento para construção de aplicações multiplataforma.


### LightSail
- <span style="background-color: #e0a800; color: black;font-weight:bold">Serviço para aplicações web simples para realização de um deploy rápido e de baixo custo.</span>Oferece instâncias de VPS fáceis de usar, containers e IaaS no geral.


### CodeArtifact
- Serviço de repósitorio de artefatos para gerenciamento de pacotes de software e bibliotecas utilizados no processo de desenvolvimento.

## Aplicações 📱
### AppSync
- Serviço para conectar aplicativos a fontes de dados seguras através de APIs.


## Miscelânea 👀

### AWS IQ
- <span style="background-color: #e0a800; color: black;font-weight:bold">permite que os clientes encontrem, contratem e paguem especialistas terceirizados</span> certificados pela AWS para trabalhos sob demanda em um projeto.