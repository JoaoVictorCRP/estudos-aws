O GuardDuty é um serviço que utiliza machine learning para detectar anomalias e atividades suspeitas em sua conta AWS.

- Fácil de ativar, basta um clique no console AWS para iniciar uma demonstração de 30 dias.

- Pode extrair e analisar  dados das seguintes fontes:
	- **CLOUDTRAIL**: Eventos de criação de recursos de rede, interações com buckets no S3.
	 
	- **VPC Flow Logs**: Tráfego interno incomum, Endereços de IP suspeitos. 
	
	- **DNS Logs**: Instâncias EC2 enviando dados através de queries DNS.
	
	- Além disso, é possível habilitar algumas outras origens como:
		- **EKS Audit Logs** para Kubernetes.
		- **Login Activies do RDS**
		- **Registros do EBS**
		- **Lambda Network Activity

- Pode ser integrado com o EventBridge para notificar detecções com o SNS.

- ==É uma excelente opção para se proteger contra ataques relacionados a mineração de criptomoedas.==