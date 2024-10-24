# Serviços Menores
Arquivo de anotações de serviços menores que costumam cair no CLF-02 (Cloud Practitioner).

# Aplicações 📱
## AppSync
- Serviço para conectar aplicativos a fontes de dados seguras através de APIs.

## Amazon Connect
- **Serviço** omnichannel **de atendimento ao cliente** baseada em IA. Basicamente um software de SAC automatizado.

## Step Functions
- Serviço para desenvolver um fluxo para aplicações de maneira **Drag N' Drop**, integra com o Lambda.

# Desenvolvimento 🖥️

## Amplify
- Framework de desenvolvimento para construção de aplicações multiplataforma.

## CodeArtifact
- Serviço de repósitorio de artefatos para gerenciamento de pacotes de software e bibliotecas utilizados no processo de desenvolvimento.

## CodeCommit
- Repositório remoto git.

## CodeBuild
- Utilizado para automação, compilação e testes nas mudanças no código de um ambiente de CI.

## CodeDeploy
- Serviço de automação de deploys para alvos computacionais (EC2, Lambda, ECS, etc).

## CodePipeline
- Usado para orquestração e automtização da entrega de software. Pode incluir o CodeBuild como um step, mas é focado no processo completo de CI/CD, não só a construção do software.

## CodeStar
- Oferece uma interface unificada para desenvolvimento, construção e deploy de aplicações rapidamente, basicamente o LightSail da programação.

## LightSail
- <span style="background-color: #e0a800; color: black;font-weight:bold">Serviço para aplicações web simples para realização de um deploy rápido e de baixo custo.</span>Oferece instâncias de VPS fáceis de usar, containers e IaaS no geral.


# Dados 📈
## Glue
- Utilizado no processo de extração, transformação e carregamento de dados; Serverless; Torna a preparação de dados mais simples, rápida e barata.



# Organizacional 🏨
## Workspaces Web
- Serviço de desktop virtual que permite às organizações criar ambientes de trabalho na nuvem, oferecendo <span style="background-color: #e0a800; color: black;font-weight:bold">acesso remoto seguro a desktops direto pelo naveagador.</span>

## AppFlow
- <span style="background-color: #e0a800; color: black;font-weight:bold">Solução gerenciada que facilita a transferência segura de dados entre aplicativos SaaS e serviços da AWS.</span> Oferece integração com plataformas como Salesforce, Zendesk, Slack e ServiceNow.


# Pagamentos & Suporte 💰
## Health Dashboard
- Exibe o status gerais dos serviços da AWS, nele você pode conferir comunicados personalizados da AWS sobre a sua conta ou organização, além de comunicar sobre futuras manutenções nos serviços em uma região.


# Segurança 🔑
## CloudHSM
- Serviço de criptografia para criação e gerenciamento de chaves e criptografia. **diferentemente do KMS, esse serviço NÃO é gerenciado pela AWS.**

## Certificate Manager
- Permite a <span style="background-color: #e0a800; color: black;font-weight:bold">criação e gerenciamento de certificados digitais que são utilizados para criptografar os dados entre os usuários e os servidores.</span>

## Security Hub
- Oferece uma interface facilmente utilizável dos alertas de segurança e outros detalhes relacionados ao acesso a serviços e outras aplicações de terceiros.

## Inspector
- Verifica instâncias, containers e funções lambda em busca de vulnerabilidades e **exposição não intencional de dados da rede.**

## Shield
- Oferece proteção contra ataques DDOS

## GuardDuty
- Serviço de detecção de ameaças e comportamentos suspeitos por parte de usuários da conta AWS e chamadas de API.

## Parameter Store
- Utilizado para armazenar parâmetros e variáveis de ambiente para os desenvolvimento de aplicações (Exemplo: Connections Strings, senhas e endpoints).

# Miscelânea 👀
## AWS IQ
- <span style="background-color: #e0a800; color: black;font-weight:bold">Permite que os clientes encontrem, contratem e paguem especialistas terceirizados</span> certificados pela AWS para trabalhos sob demanda em um projeto.

## Rekognition
- Serviço de visão computacional capaz de analisar o conteúdo de vídeos e fotos, utiliza Deep Learning para fazer isso, a API é bem fácil de usar e não requer nenhum conhecimento em Machine Learning para usar. Além disso, ele também possui integração com o S3, para fazer análise dos arquivos que aparecerem por lá. Bem interessante!

## MediaStore
- Serviço de armazenamento otimizado para **fluxos de mídia** e **transmissões ao vivo**, oferece baixa latência e alto desempenho para entregar vídeos em tempo real. Ele armazena segmentos de vídeo de forma eficiente para transmissões contínuas. 
- Não realiza transcodificação de vídeo, mas pode ser integrado com outros serviços, como **AWS Elemental MediaLive** para gerenciar **transmissões ao vivo**.
- Ideal em cenários de streaming ao vivo.

## Device Farm
- Este é um serviço utilizado para testes em diferentes plataformas. Permite a emulação de celulares, computadores e tablets para análise e QA.
- Através da emulação de múltiplos dispositivos é possível testar a responsividade e o comportamento da lógica da aplicação em diferentes cenários.