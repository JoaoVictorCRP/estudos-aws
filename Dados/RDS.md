# RDS
O Relational Database Service é o serviço de banco de dados da AWS, é um 
serviço bem eficiente que possui integração com diversos SGBD.
## Multi-AZ
#### **Focado na recuperação de desastres.**
- Com o multi-az ativo, você terá uma versão primária e uma secundária do seu banco, cada um em uma AZ diferente. 
suponhamos que a versão primária vá pro saco, daí o DNS (connection string) irá trocar o apontamento para versão secundária automaticamente.

## Read Replica
#### **Focado no desempenho**
- Neste modo, toda vez que você fazer uma ação de Write no seu banco principal, essa ação também será realizada no banco 
secundário, que fica em outra AZ.

- É possível direcionar requisições para read replica, tirando muito stress do banco principal (usado para escrita)

- Read replicas possuem replicação assíncrona, portanto <span style="background-color: #e0a800; color: black;font-weight:bold">possuem consistência eventual. </span>

- Cada read replicas possui um endpoint diferente.

- IAM Database Authentication

- RDS Custom?

- On demand Backups para AURORA.

- Aurora Cloning

- RDS Proxy para redução o tempo de failover

## Backups
Além do Multi-AZ e Read Replica, temos outras opções de backup também, são elas: 
### Automated Backups
Permite recuperar o banco de dados para qualquer momento em um 
“período de retençãoˮ. O período de retenção pode ser entre 1 e 35 dias. Os Automated Backups fazem um snapshot completo diariamente, e também irão armazenar logs transacionais ao longo do dia. Quando você realizar um recovery, a AWS irá restaurar o snapshot mais recente e também aplicar os logs de inserção daquele dia.
### Database Snapshots
São feitos manualmente e ficarão armazenados mesmo depois da deleção da instância de RDS, diferentemente da versão automatizada.

## RDS Proxy
- Opção que oferece um proxy totalmente gerenciado para um banco RDS.
- Permite que as conexões ao banco sejam agrupadas e compartilhadas entre as aplicações.
- Melhora a eficiência de recursos do banco (CPU e RAM) devido a minimização das conexões.
- Nenhuma mudança no código é necessária
- Permite utilizar o IAM para conexões com o banco de dados.

___
## Elasticache
- O Elasticache é o serviço que fornece a opção de armazenar em cache as queries mais comuns e mais requisitadas, dessa forma salvando o tempo de processamento para uma consulta real em um banco de dados em disco.
- Neste serviço temos duas opções de sistema: Redis e Memcached.

___
## Aurora
- Serviço de banco de dados relacional da AWS que combina a alta performance e disponibilidade de bancos de dados comerciais com a 
efetividade dos bancos de dados open-source. o Aurora é 
compatível com PostgreSQL e MySQL.

- Projetado para ser até 5x mais rápido que o MySQL e 
três vezes mais rápido que o PostgreSQL padrão, oferecendo baixa 
latência e alto throughput.

- Oferece criptografia em repouso e em trânsito, e integrações nativas com IAM para controle de acesso.

- Inclui backups automáticos, recuperação point-in-time, patching 
automático e outras funcionalidades gerenciadas, liberando da manutenção rotineira.

### Alta Disponibilidade e Escalabilidade
**O aurora é replicado automaticamente em múltiplas AZs, garantindo alta disponibilidade.** Pode escalar automaticamente tanto em termos de armazenamento (até 128TB por instância) quanto de capacidade de leitura com réplicas de leitura.

### Tipos de Réplica
O Aurora oferece 3 tipos de réplicas: Aurora Replica, MySQL Read Replica, PostgreSQL Read Replica:

- **Aurora Replicas**: São réplicas de leitura criadas dentro do cluster de banco de dados Aurora. 
	- Failover automático: Em caso de falha na instância primária, uma das Aurora Replicas pode ser promovida automaticamente para ser a nova instância principal, garantindo alta disponibilidade.

	- <span style="background-color: #e0a800; color: black;font-weight:bold">Permite até 15 réplicas dentro de uma região</span>, com forte consistência de dados (pois as réplicas compartilham o mesmo armazenamento subjacente com o BD principal - São clusters).

    - Sincronização Rápida: Devido ao armazenamento compartilhado, as réplicas estão sempre atualizadas com a instância principal, minimizando a latência de replicação.

- **MySQL/PostgreSQL Read Replicas**:Você também pode criar até 5 Read Replicas MySQL ou PostgreSQL. Essas réplicas podem ser criadas tanto dentro do mesmo cluster quanto em outra região (cross-region), usando replicação assíncrona.

## Aurora Serverless
Essa é a configuração que permite que o Aurora escale automaticamente sua capacidade com base na demanda da aplicação, sem a necessidade de gerenciamento manual de instâncias de banco de dados. É eficiente para workloads imprevisíveis.

___
## Limitações
- **READ REPLICAS**: O número de read replicas que você pode criar de uma instância RDS depende do tipo de engine você usa, mas no geral, pode se ter <span style="background-color: #e0a800; color: black;font-weight:bold">
até 15 RRs, sendo 5 delas cross-region.
</span>
___
## Anotações
- O RDS roda em uma EC2, no entanto você não consegue entrar no SO delas, somente no serviço de BD.

- RDS não é serveless, a menos que o SGBD seja um AURORA SERVERLESS

- É necessário habilitar o Automatic Backups para dar deploy em uma Read Replica.

- Read Replicas podem ter Multi-AZ habilitado, além de também poderem ser promovidas a banco de dados principal

- Se você estiver utilizando uma RDS single-AZ e precisar fazer um backup ou snapshot, as operações de I/O serão suspendidas, cuidado!!!