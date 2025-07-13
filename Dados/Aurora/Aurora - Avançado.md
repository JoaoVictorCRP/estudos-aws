Este arquivo inclui notas avançadas sobre o funcionamento do Amazon Aurora e suas features.

- ==É possível associar uma grau de prioridade (0-15) para cada Read Replica do Aurora==.
	- Isso é importante no momento de failover, pois o RDS vai promover a RR com maior grau de prioridade para instância principal.
		- Se duas réplicas tiverem a mesma prioridade, o RDS vai promover a que tiver maior tamanho.
		- Caso as réplicas tiverem o mesmo nível de prioridade e tamanho, a decisão será arbitrária (escolha aleatória).

- **Você pode migrar um snapshot de um RDS MySQL normal para Aurora MySQL**.

- Há uma métrica do CloudWatch chamada `AuroraReplicaLag`, ela monitora o lag ao replicar atualizações da instância primária para as RR.