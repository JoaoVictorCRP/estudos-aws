# Aurora
- Serviço de banco de dados relacional da AWS que combina a alta performance e disponibilidade de bancos de dados comerciais com a efetividade dos bancos de dados open-source. o Aurora é compatível com PostgreSQL e MySQL.

- Projetado para ser ==até 5x mais rápido que o MySQL e três vezes mais rápido que o PostgreSQL padrão==, oferecendo baixa latência e alto throughput.

- Oferece criptografia em repouso e em trânsito.

- Integração nativa com IAM para controle de acesso.

- ==Inclui backups automáticos, recuperação point-in-time, patching automático e outras funcionalidades gerenciadas==, liberando da manutenção rotineira. Você pode definir o período de retenção de backup entre 1 e 35 dias.

## Alta Disponibilidade e Escalabilidade
**==O aurora é replicado automaticamente em múltiplas AZs==, garantindo alta disponibilidade.** Pode escalar automaticamente tanto em termos de armazenamento (até 128TB por instância) quanto de capacidade de leitura com réplicas de leitura.

## Tipos de Réplica
O Aurora oferece 3 tipos de réplicas: Aurora Replica, MySQL Read Replica, PostgreSQL Read Replica:

- **Aurora Replicas**: São réplicas de leitura criadas dentro do cluster de banco de dados Aurora. 
	- **Failover automático**: Em caso de falha na instância primária, uma das Aurora Replicas pode ser promovida automaticamente para ser a nova instância principal, garantindo alta disponibilidade.

	- **==Permite até 15 réplicas dentro de uma região==,** com **forte consistência de dados**, pois as **réplicas compartilham o mesmo armazenamento subjacente com o BD principal** (Cluster).

    - **Sincronização Rápida**: Devido ao armazenamento compartilhado, as réplicas estão sempre atualizadas com a instância principal, minimizando a latência de replicação.

- **MySQL/PostgreSQL Read Replicas**: Você pode criar até 5 Read Replicas MySQL ou PostgreSQL. Essas réplicas podem ser criadas tanto dentro do mesmo cluster quanto em outra região (cross-region), **usando replicação assíncrona neste caso**.

## Aurora Serverless
Essa é a configuração que ==permite que o Aurora escale automaticamente sua capacidade com base na demanda da aplicação==, sem a necessidade de gerenciamento manual de instâncias de banco de dados. É eficiente para workloads imprevisíveis.

## Os Endpoints do AURORA
O Aurora possui tipos diferentes de endpoint, cada um servindo para um caso de uso específico, vamos analisar:

- **Cluster Endpoint**: Este é o endpoint principal, ele leva direto para instância primária do cluster.

- **Reader Endpoint**: Como o nome sugere, este é o endpoint para leitura de dados, ele faz um ==load balance entre as read replicas disponíveis==.

- **Custom Endpoint**: Endpoint personalizado, permite que você possa definir uma ou mais instâncias para responderem nesse endpoint.

- **Instance Endpoint**: Endpoint para uma única instância específica.

## Aurora Cloning
Essa é uma feature do Aurora que permite realizar uma clonagem completa de um cluster do Aurora, criando com isso um cluster independente. **O processo de cloning é bem mais simples e rápido que o de gerar um snapshot.**

- Muito útil para cenários onde se precisa preparar um ambiente de testes rapidamente.

- É possível criar mais de um clone de um cluster aurora, além disso também dá pra ter vários clones de um clone.

- Não dá pra criar um clone em uma região diferente da que está o cluster de origem.

- É possível compartilhar um clone com uma conta membro da organização.

## Aurora Backtracking
Essa feature permite voltar o estado cluster a um período anterior de até 72 horas.
- NÃO cria um novo cluster (restauração in-place)
- **Disponível apenas para Aurora MySQL**

## Limitações e detalhes
- **READ REPLICAS**: O número de read replicas que você pode criar depende do tipo de engine você usa, mas no geral, pode se ter ==até 15 RRs, sendo 5 delas cross-region.==

- **O Aurora é caro pra caramba**, claro que as vantagens compensam em casos onde o dono da aplicação quer alta performance e redundância para cargas de trabalho intensa, mas caso o alvo seja uma arquitetura cost-effective... VAZA!