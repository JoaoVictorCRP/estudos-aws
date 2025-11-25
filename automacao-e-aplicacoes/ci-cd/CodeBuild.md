# CodeBuild
- O CodeBuild é um serviço totalmente gerenciado de *build & test* (CI)

- Através dele podemos compilar aplicações a partir de um código fonte armazenado no CodeCommit, GitHub, Bitbucket, etc.
 
- As definições de build são feitas através do arquivo `buildspec.yml`, que deve ficar na raiz do repositório.

- O Codebuild possui um painel que exibe os relatórios de falhas e sucessos em testes unitários, chamado **Report Group**.

## Detalhes Avançados
### Build Environment: Compute Types & Privileged Mode

#### Compute Types e Performance
- CodeBuild oferece _compute types_ (SMALL, MEDIUM, LARGE, GPU), mas pouco se fala sobre:
    - **Burstable CPU**: builds podem sofrer throttling.
    - Builds paralelos funcionam melhor com **LARGE** por causa de I/O.
    - Builds envolvendo _machine learning_, _video processing_, _renderização_, se beneficiam da **compute type GPU**.

#### Privileged Mode
- Essencial para **builds Docker dentro do CodeBuild**.
- Quando ativado:
    - O contêiner do CodeBuild recebe acesso ao daemon Docker.
    - Permite:
        - build de imagens Docker,
        - push para ECR,
        - execução de contêineres dentro do build.


## Integração com VPC
Permite rodar o build **dentro de uma VPC privada**, o que desbloqueia:
- acesso a RDS,
- endpoints privados,
- serviços internos.
> ⚠️ **Porém, ativa um efeito colateral** 
   Se sua VPC não tiver **NAT Gateway** ou **VPC Endpoints**, o build **não tem acesso à internet**, quebrando:
- `npm install`
- `pip install`
- downloads via curl/wget
- pulls do DockerHub