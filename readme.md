# Estudos AWS
Este é o meu repositório de estudos da plataforma AWS. Se quiser, você pode clonar este repositório para utilizar as minhas anotações também! :)

## Estudar
- [ ] Serviços de IOT

- [ ] Serviços de ML

- [ ] Detalhes do AWS DLCM (*Data Lifecycle Manager*)

- [ ] [Autoscaling do DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/AutoScaling.html)

## Detalhes para memorizar


- **AWS Managed Keys**: Não é possível habilitar ou desabilitar a ==rotação automática== das chaves gerenciadas pela AWS, isso ==é feito automaticamente pela própria AWS no período de 1 ano.==

- **Customer-Managed CMK**: É impossível rotacionar o conteúdo de uma Customer Managed CMK importada. Podemos apenas criar uma nova com um outro conteúdo de criptografia.

- **==As SCPs são aplicadas até mesmo ao usuário root da conta.**==

- **`DisableApiTermination` vs. Instance Protection**: DisableApiTermination impede ações de usuários, mas não do ASG. O Instance Protection faz o contário.

- **Capacity Reservations**: As reservas de capacidade não garantem desconto nenhum, diferente das RIs e SPs. As CRs servem apenas para reservar hardware para você de maneira que evite que falte hardware para você em momentos de pico.

- **Endereço MAC**: Se o enunciado de alguma questão pede por um endereço MAC fixo para uma instância EC2, sempre pense nas **ENI**s. ==Se um endereço MAC estático estiver atribuído a uma ENI, ele não mudará==.

## 📚 Notas por Categoria

### 🧠 Básico
- [Cloudfront](basico/CloudFront.md)
- [Serviços Menores](basico/servicosMenores.md)
- [Support Plans](basico/supportPlans.md)

### 🖥️ Computação
- [AMI](computacao/AMI.md)
- [Appstream 2.0](computacao/AppStream%202.0.md)
- [Autoscalling](computacao/AutoScalling.md)
- [Containerização](computacao/Containerizacao.md)
- [Elastic Load Balancer](computacao/ELB.md)
- [Lambda](computacao/Lambda.md)
- [Workspaces](computacao/Workspaces.md)
- [EC2](computacao/ec2/EC2.md)
	- [EC2 - Avançado](computacao/ec2/EC2-Avancado.md)
	- [EC2 - Spot Fleets](computacao/ec2/EC2-SpotFleets.md)  

### 🗄️ Armazenamento
- [EBS](armazenamento/EBS.md)
- [EFS](armazenamento/EFS.md)
- [S3](armazenamento/S3.md)
- [S3 Glacier](armazenamento/S3%20-%20Glacier.md)
- [Snow Family](armazenamento/SnowFamily.md)

### 🔐 Segurança
- [AWS Signer](seguranca/AWS%20Signer.md)
- [CloudHSM](seguranca/CloudHSM.md)
- [Cloudtrail](seguranca/CloudTrail.md)
- [Cognito](seguranca/Cognito.md)
- [Detective](seguranca/Detective.md)
- [GuardDuty](seguranca/GuardDuty.md)
- [IAM Identity Center](seguranca/IAM%20Identity%20Center.md)
- [IAM](seguranca/IAM.md)
- [Inspector](seguranca/Inspector.md)
- [Parameter Store](seguranca/ParameterStore.md)
- [Secrets Manager](seguranca/SecretsManager.md)
- [Security Hub](seguranca/SecurityHub.md)
- [STS](seguranca/STS.md)
- [WAF](seguranca/WAF.md)
- [AWS ACM](seguranca/ACM/AWS%20ACM.md)
- [AWS Private CA](seguranca/ACM/AWS%20Private%20CA.md)
- [Anotações sobre Bloqueio de IPs](seguranca/anotacoes/BloqueioIPs.md)
- [Criptografia](seguranca/anotacoes/Criptografia.md)
- [KMS Avançado](seguranca/KMS/KMS%20Avancado.md)
- [KMS](seguranca/KMS/KMS.md)
- [Padroes de Segurança](certificacoes/security-specialty/PadroesDeSeguranca.md)

### 🌐 Rede
- [Redes](certificacoes/security-specialty/Redes.md)
- [Route 53](rede/Route53.md)
- [VPC Endpoints](rede/VPC-EndPoints.md)
- [VPC](rede/VPC.md)

### 🗃️ Banco de Dados
- [DynamoDB](dados/DynamoDB.md)
- [Elasticache](dados/Elasticache.md)
- [EMR](dados/EMR.md)
- [Kinesis](dados/Kinesis.md)
- [RDS](dados/RDS.md)
- [Redshift](dados/Redshift.md)
- [Aurora](dados/Aurora/Aurora.md)
- [Aurora - Avançado](dados/Aurora/Aurora%20-%20Avan%C3%A7ado.md)

### 🛠️ Automação e Aplicações
- [API Gateway](automacao-e-aplicacoes/ApiGateway.md)
- [Cloudformation](automacao-e-aplicacoes/CloudFormation.md)
- [ElasticBeanstalk](automacao-e-aplicacoes/ElasticBeanStalk.md)
- [Elastic Transcoder](automacao-e-aplicacoes/ElasticTranscoder.md)
- [Systems Manager](automacao-e-aplicacoes/Systems%20Manager.md)
- [IOT](IoTServices)

### 🧳 Migração e Transferência
- [AWSMigrationTools](AWSMigrationTools.md)
- [DMS](migracao-e-transferencia/DMS.md)
- [Estratégias de Migração para a Nuvem](migrationStrategies.md)
- [Transfer Family](migracao-e-transferencia/TransferFamily)

### 🧪 Revisões e Erros de Simulado
- [Disaster Recovery](revisoes-e-erros/DisasterRecovery.md)
- [Dúvidas Comuns](revisoes-e-erros/DuvidasComuns.md)
- [Cost Optimized Architecture](revisoes-e-erros/Erros%20no%20simulado/Cost-Optimized%20Architecture.md)
- [High Performancing Architecture](revisoes-e-erros/Erros%20no%20simulado/High-Performancing%20Architecture.md)
- [Resilient Architecture](revisoes-e-erros/Erros%20no%20simulado/Resilient%20Architecture.md)
- [Secure Architectures](revisoes-e-erros/Erros%20no%20simulado/Secure%20Architectures.md)

### ✉️ Mensageria
- [SNS](mensageria/SNS.md)
- [SQS](mensageria/SQS.md)
- [SWF](mensageria/SWF.md)
- [Step Functions](mensageria/StepFunctions.md)

### 🏛️ Governança e Monitoramento
- [AWS Config](governanca-e-monitoramento/AWSConfig.md)
- [Control Tower](governanca-e-monitoramento/Control%20Tower.md)
- [X-Ray](governanca-e-monitoramento/X-Ray.md)
- [Firewall Manager](governanca-e-monitoramento/Organizations/Firewall%20Manager.md)
- [Organizations](governanca-e-monitoramento/Organizations/Organizations.md)
- - [CloudwatchAgent](CloudwatchAgent.md)

### 👮🏻 Security Specialty
- Anotações específicas sobre detalhes que caem na certificação Security Specialty
- [Segurança no Cloudformation](certificacoes/security-specialty/Cloudformation-Security.md)
- [Directory Services](certificacoes/security-specialty/Directory%20Services.md)
- [Dúvidas Comuns](certificacoes/security-specialty/Duvidas%20Comuns.md)
- [Logging](certificacoes/security-specialty/Logging.md)
- [IAM - Avançado](certificacoes/security-specialty/Acessos%20e%20Policies/IAM.md)
- [IAM Identity Center](certificacoes/security-specialty/Acessos%20e%20Policies/IAM%20Identity%20Center.md)
- [Validação de Políticas do IAM](certificacoes/security-specialty/Acessos%20e%20Policies/IAMPolicys-InDepth.md)
- [Resource-Based Policies](certificacoes/security-specialty/Acessos%20e%20Policies/RBPs.md)
- [Session Policies](certificacoes/security-specialty/Acessos%20e%20Policies/Session%20Policies.md)

