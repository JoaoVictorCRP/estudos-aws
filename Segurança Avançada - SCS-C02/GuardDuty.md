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


## Supression Rules
As ==**Suppression Rules** permitem que você crie regras para **filtrar e descartar detecções**== que, por algum motivo, não são relevantes para o seu caso de uso. Por exemplo, você pode querer ignorar certos tipos de detecções que já foram investigadas e não representam uma ameaça real, ou simplesmente filtrar alarmes de atividades que você sabe que são legítimas (como uma atividade que ocorre rotineiramente em sua rede).

## Estratégia Multi contas
- ==É possível gerenciar múltiplas contas através do GuardDuty==.

- Para gerenciar uma outra conta com o GuardDuty, você precisa estar associando ela a conta administradora. Duas opções para isso:
	- Usando o AWS Organizations.
	- Enviando um convite por meio do próprio GuardDuty.

- As contas administradoras podem:
	- Adicionar e remover contas membro
	- Gerenciar o GuardDuty das contas membros.
	- Gerenciar findings, supression rules, white lists e threat lists .

- Com o AWS Organizations, você pode especificar uma conta membro para ser a administradora do GuardDuty (Ou seja, não precisa necessariamente ser a conta root)

## Automatizando Respostas aos Findings
- É possível automatizar respostas aos findings do GuardDuty através de uma integração com o EventBridge.
![[GuardDuty_Automation.png]]

- É possível mandar o finding para o SNS, Lambda ou SQS. 