# RDS
O Relational Database Service é o serviço de banco de dados da AWS, é um serviço gerenciado extremamente eficiente e escalável, que possui integração com diversos SGBD.
## Multi-AZ
#### **Focado na recuperação de desastres**
- Com o Multi-AZ ativo, você terá uma versão primária e uma secundária do seu banco, cada um em uma AZ diferente. 

- Suponhamos que a versão primária vá pro saco, daí o DNS (connection string) irá trocar o apontamento para versão secundária automaticamente.

- Uma coisa legal é que ==os backups automatizados são realizados a partir dos dados da instância em standby do Multi-AZ.== O que fará com que a aplicação não fique indisponível, pois a instância primária ainda estará trabalhando tranquilamente.

## **Read Replica**
#### **Focado no desempenho**
- Neste modo, toda vez que você fazer uma ação de Write no seu banco principal, essa ação também será realizada no banco secundário, que fica em outra AZ. A read replica também pode estar em outra região (cross-region read replica, mas isso depende da engine - só da pra fazer isso com [**Postgres, MySQL, MariaDB e SQL Server**](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.RDS_Fea_Regions_DB-eng.Feature.CrossRegionReadReplicas.html))

- É possível direcionar requisições para read replica, aliviando carga do banco principal.

- Read replicas ==possuem **replicação assíncrona**, portanto, possuem consistência eventual==.

- Cada read replicas possui um endpoint diferente.

- ==Para a replicação funcionar corretamente é necessário que cada uma das instâncias RR tenham as mesmas capacidades de armazenamento e computação da instância primária.==
---
## Backups
Além do Multi-AZ e Read Replica, temos outras opções de backup também, são elas: 
### Automated Backups
- Permite recuperar o banco de dados para qualquer momento dentro do “período de retençãoˮ. 
- ==O período de retenção pode ser entre 1 e 35 dias.== 
- Os Automated Backups fazem um snapshot completo diariamente, e também irão armazenar logs transacionais ao longo do dia. 
- Quando você realizar um recovery, a AWS irá restaurar o snapshot mais recente e também aplicar os logs de inserção daquele dia.
### Database Snapshots
- São feitos manualmente e ficarão armazenados mesmo depois da deleção da instância RDS, diferentemente da versão automatizada.

---
## RDS Proxy
- Opção que oferece um proxy totalmente gerenciado para um banco RDS.
- Permite que as conexões ao banco sejam agrupadas e compartilhadas entre as aplicações.
- Melhora a eficiência de recursos do banco (CPU e RAM) devido a minimização das conexões.
- Nenhuma mudança no código é necessária.
- Permite utilizar o IAM para conexões com o banco de dados.

___
## Parameter Groups
- Com eles, é possível configurar a engine do banco de dados.

- Parâmetros dinâmicos se aplicam imediatamente, parâmetros estáticos são aplicados apenas após a reinicialização da instância.

- Você pode modificar o parameter group associado a um DB, mas precisa reiniciá-lo para que isso seja aplicado.

- **==IMPORTANTE==**: Para forçar conexões SSL no banco de dados, você precisa de um parâmetro específico habilitado:
	- **`rds.force_sll=1`** para PostgreSQL e SQL Server.
	- **`require_secure_transport=1`** para MySQL e MariaDB
---
## Engine Patches
- Se você precisar fazer algum upgrade na engine do banco de dados, isto é, no SGBD. ==A atualização será aplicada na instância primária e, automaticamente, nas standbys.==

- Isso ==causará um downtime até que o upgrade esteja completo!==

___
## IAM Database Authentication
- É possível integrar o IAM com a sua instância RDS, permitindo uma conexão segura e bem eficiente que não precisa de senha, pois utiliza um authentication token da AWS. 

- É compatível com: ==MariaDB, MySQL e PostgreSQL (E versões AURORA de ambos).==
## Limitações
- **READ REPLICAS**: O número de read replicas que você pode criar de uma instância RDS depende do tipo de engine você usa, mas no geral, pode se ter ==até 15 RRs, sendo 5 delas cross-region.==
___

## Monitoramento
Existem duas opções para monitorar uma instância RDS de maneira mais granular e detalhada São elas:
- **Enhanced Monitoring**: ==Coleta métricas a nível de SO==, como: **Memória ativa**, **memória livre**, **processos em execução**, **utilização de SWAP**.

- **Performance Insights**: ==Coleta métricas a nível de Engine de BD==, como: **Queries mais executadas**, **delay de queries**, **consumo de CPU por query**, **latência de E/S**, e muito mais. 

---
## Anotações
- O RDS roda em uma EC2, no entanto você não consegue entrar no SO delas, somente no serviço de BD.

- RDS não é serverless, a menos que o SGBD seja um AURORA SERVERLESS

- É necessário habilitar o Automatic Backups para dar deploy em uma Read Replica.

- **Read Replicas podem ter Multi-AZ habilitado**, caso, esta feature esteja habilitada, as read replicas poderão assumir o papel de nó primário em momentos de failover. 

- ==Se você estiver utilizando uma RDS single-AZ e precisar fazer um backup ou snapshot, as operações de I/O serão suspendidas, cuidado!!!==