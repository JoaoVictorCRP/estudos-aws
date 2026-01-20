A AWS conta com vários serviços úteis para migração de aplicações e componentes que rodam on-premises para a nuvem. Vejamos aqui algumas delas.

**AWS Application Discovery Service**: Útil para ==coleta de dados sobre servidores que rodam on-premises==.
- Coleta dados como *hostname*, endereços IP, endereço MAC, uso de CPU, rede, memória e disco.
- Funciona em formato agent-based (servidores Linux/Windows) e Agentless (arquivo OVA para VMware). Ver mais informações abaixo:
	<img src="./images/Discovery-agentlessconector-vs-agent.png" alt="Discovery Agent vs Agentless Connector"/>

**AWS Application Migration Service**: Após a coleta de dados pelo serviço acima, ==podemos então migrar nossos servidores para EC2 através do AMS==.

**AWS Database Migration Service**: O DMS é muito útil quando precisamos migrar uma database on-premises para o RDS.
- Um detalhe legal é que os dados são criptografados em repouso na instância de replicação, a chave utilizada por padrão é a ==**`aws/dms`**==.

- ==Para criptografia em trânsito, é necessário que os endpoints do banco de destino e do banco de origem utilizem SSL/TLS.==


**AWS DataSync**: Esse serviço é utilizado para largarmos de mão o armazenamento on-premises e migrarmos para um bucket S3, EFS ou FSx.

**AWS Migration Hub**: Serviço feito para monitorar o processo de migração para a AWS.