# <span style="color: orange; font-weight:bold"> Elastic Container Service </span>
O ECS é um serviço gerenciado que facilita a execução e gerenciamento de contêiners Docker em um infraestrutura da Amazon, sem a necessidade de provisionar ou gerenciar servidores. Ideal para executar aplicações containerizadas em larga escala.

## Pontos Chave
- **Clusters (A.K.A. Ambiente de execução)**: Os clusters são coleções de recursos (instâncias EC2 ou Fargate) que provisionam os recursos de computação para os containers. Eles funcionam como o ambiente onde as tasks e services são executados.
  
- **Services (A.K.A. DockerCompose)**: O Service gerencia a quantidade de containers que devem estar em funcionamento, escalonando-os horizontalmente de acordo com a demanda. Se uma task falhar, o Service é responsável por reiniciá-la automaticamente para garantir a disponibilidade.

- **Tasks (A.K.A. Docker run)**: Uma Task é uma instância de containers Docker em execução, criada com base nas configurações definidas na **Task Definition**. A Task Definition define qual imagem Docker o container usará, os recursos necessários e outras configurações, semelhante ao comando `docker run`.

### E as imagens?
- As imagens são criadas em um ambiente local e então se realiza o upload no ECR, a partir da imagem depositada no ECR você faz uma task definition.

## Funcionalidades
### Gerenciamento de Containers
- O ECS permite que você defina clusters de containers que podem ser gerenciados de forma centralizada. Você define tarefas que especificam quais containers executar, quais imagens Docker usar e como os containers devem interagir entre si.

### Agendador de Tarefas
- O ECS possui um **task scheduler** que gerencia a execução das tarefas, garantindo que os containers sejam iniciados e mantidos conforme o necessário. Oferece flexibilidade na definição de regras de execução para tarefas e serviços, como a quantidade máxima e mínima de instâncias que devem ser mantidas.

### Suporte ao EC2 e Fargate
- O ECS suporta duas modalidades de execução:
    - **ECS com EC2**: Você gerencia a infraestrutura subjacente (A instância EC2) em que os containers serão executados.

    - **EC2 com Fargate**: Com o Fargate, não há necessidade de provisionar ou gerenciar servidores, já que a AWS gerencia a infraestrutura. Você apenas define as tarefas e containers, o Fargate cuida do resto.

### Integração com Outros Serviços AWS
- O ECS se integra com vários serviços AWS, como o **ELB** para balanceamento de carga, o **IAM** para gerenciar permissões, o **CloudWatch** para monitoramento, e o **ECR (Elastic Conteiner Registry)** para armazenamento de imagens Docker.

### Escalabilidade Automática
- O ECS pode escalar automaticamente o número de instâncias EC2, ou tarefas, baseadas na demanda, integrando-se com o **Auto Scaling**. Isso permite que o ECS se ajusta às flutuações na carga de trabalho sem intervenção manual.

# <span style="color: orange; font-weight:bold"> Fargate</span>
Serviço **serverless** de execução de containers, não há necessidade de gerenciar a infraestrutura subjacente, como servidores ou clusters. <span style="background-color: #e0a800; color: black;font-weight:bold"> Com Fargate, você apenas define e executa containers, o serviço cuida automaticamente de provisionar e escalar a infraestrutura.
</span>

## Gerenciamento Automático de Infraestrutura
<span style="background-color: #e0a800; color: black;font-weight:bold">Com Fargate, você não precisa provisionar, configurar, escalar instâncias EC2 ou gerenciar clusters. Você apenas define as especificações do container (CPU, memória, imagem, etc.) e o Fargate cuida do resto.</span>

## Integração com ECS e EKS
O Fargate pode ser usado tanto com o **Amazon Elastic Container Service (ECS)** quanto com o **Amazon Elastic Kubernetes Service (EKS)**. Isso significa que você pode optar por usar Fargate em arquiteturas baseadas em Kubernetes ou Docker de maneira transparente.

## Escalabilidade Automática
O Fargate escala automaticamente os containers com base na demanda, adicionando ou removendo capacidade conforme necessário. Isso simplifica a operação de ambientes que sofrem variações de carga.

# <span style="color: orange; font-weight:bold"> Elastic Kubernetes Service</span>

## Gerenciamento Automático de Kubernetes
O EKS gerencia automaticamente a instalação, operação e manutenção dos nós de controle do Kubernetes, que são responsáveis por tarefas como escalonamento de pods, monitoramento de nodes e gerenciamento de atualizações de estado.

## Suporte para Ambientes Multinuvem e On-premises
Além de rodar clusters Kubernetes na AWS, <span style="background-color: #e0a800; color: black;font-weight:bold">o EKS também pode ser usado para gerenciar Kubernetes on-premises</span> usando o **EKS Anywhere**, que também possibilita gerenciar um ambiente de múltiplas nuvens.

## Clusters Gerenciados
O EKS simplifica a criação de clusters Kubernetes, gerenciando tanto os nós de controle quanto os nós de trabalho. O serviço automaticamente mantém os componentes do Kubernetes atualizados.

## Segurança
A integração com o **IAM** permite que você gerencie permissões e autenticações de forma segura. Além disso, ele utiliza **VPCs** para isolar seus clusters, aumentando a segurança de suas aplicações.

## Networking e Load Balancing
O EKS oferece integração direta com **Elastic Load Balancers (ELB)** e serviços de redes da AWS, o que facilita o roteamento de tráfego entre seus containers de forma eficiente e escalável.


# Anotações
- Containers são agrupados em **PODS**.