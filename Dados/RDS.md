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

## Engine Patches
- Se você precisar fazer algum upgrade na engine do banco de dados, isto é, no SGBD. ==A atualização será aplicada na instância primária e, automaticamente, nas standbys.==

- Isso ==causará um downtime até que o upgrade esteja completo!== Deixa pro plantonista fazer fora do horário...
## Elasticache
- O Elasticache é o serviço que fornece a opção de armazenar em cache as queries mais comuns e mais requisitadas, dessa forma salvando o tempo de processamento para uma consulta real em um banco de dados em disco.
- Neste serviço temos duas opções de sistema: Redis e Memcached.

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