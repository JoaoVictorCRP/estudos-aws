O AWS Outposts é uma **extensão da AWS para ambientes on-premises**, permitindo rodar serviços da AWS fisicamente dentro do seu datacenter ou instalação local, com **baixa latência e consistências total com a nuvem**.

### Como funciona?
- A AWS entrega **hardware gerenciado** ao cliente (racks físicos).
- Você pode executar **serviços AWS nativos** (como EC2, EBS, RDS, ECS, EKS) **localmente**.
- Gerenciamento, APIs, SDKs e console são **iguais aos da nuvem**.
- **Requer conexão com a AWS** (exceto na versão “Outposts Servers” com modos desconectados).

##### Serviços suportados
- **EC2**, **EBS**, **VPC**
- **ECS** e **EKS** (em modo local)
- **RDS** (PostgreSQL, MySQL)
- **S3 Outposts** (armazenamento de objetos local)
- **EMR** (para Big Data no edge)
---
### Casos de uso
- **Baixa latência** 🕓: Sistemas que precisam de resposta em tempo real.

- **Requisitos regulatórios ou de residência de dado**s 🔒: Países ou setores que exigem que dados fiquem localmente (ex: setor bancário, governo).

- **Ambientes desconectados ou intermitentes** 🏝️: Plataformas de petróleo, fábricas remotas, navios, etc.


## Anotações
- Toda comunicação é criptografada.
- Gerenciamento do acesso é feito vai IAM
- Todos os objetos em um S3 que roda em outpost possuem uma única classe, chamada **S3 Outposts**.
- Para que uma instância EC2 na AWS acesse um bucket do Outpost, é preciso provisionar um Access Point ligado ao bucket.