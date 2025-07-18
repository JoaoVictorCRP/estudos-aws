# Estudos AWS
Este é o meu repositório de estudos da plataforma AWS. Se quiser, você pode clonar este repositório para utilizar as minhas anotações também! :)

## Estudar
- [ ] Recursos e serviços que podem ser compartilhados através do RAM.

- [ ] Deployment policies do Elastic BeanStalk.

- [ ] Slow Start Mode em um Target Group.

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
- [Estratégias de Migração para a Nuvem](basico/migrationStrategies.md)
- [Servicos Menores](basico/servicosMenores.md)
- [Support Plans](basico/supportPlans.md)

### 🖥️ Computação
- [AMI](computacao/AMI.md)
- [Appstream 2.0](computacao/AppStream%202.0.md)
- [Autoscalling](computacao/AutoScalling.md)
- [Containerização](computacao/Containerizacao.md)
- [CWAgent](computacao/CWAgent.md)
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
- [Aws signer](seguranca/AWS%20Signer.md)
- [Cloudhsm](seguranca/CloudHSM.md)
- [Cloudtrail](seguranca/CloudTrail.md)
- [Cognito](seguranca/Cognito.md)
- [Detective](seguranca/Detective.md)
- [Guardduty](seguranca/GuardDuty.md)
- [Iam identity center](seguranca/IAM%20Identity%20Center.md)
- [Iam](seguranca/IAM.md)
- [Inspector](seguranca/Inspector.md)
- [Parameterstore](seguranca/ParameterStore.md)
- [Secretsmanager](seguranca/SecretsManager.md)
- [Securityhub](seguranca/SecurityHub.md)
- [Sts](seguranca/STS.md)
- [Waf](seguranca/WAF.md)
- [Aws acm](seguranca/ACM/AWS%20ACM.md)
- [Aws private ca](seguranca/ACM/AWS%20Private%20CA.md)
- [Bloqueioips](seguranca/anotacoes/BloqueioIPs.md)
- [Criptografia](seguranca/anotacoes/Criptografia.md)
- [Kms avancado](seguranca/KMS/KMS%20Avancado.md)
- [Kms](seguranca/KMS/KMS.md)
- [Padroesdeseguranca](certificacoes/security-specialty/PadroesDeSeguranca.md)

### 🌐 Rede
- [Redes](certificacoes/security-specialty/Redes.md)
- [Route53](rede/Route53.md)
- [Vpc endpoints](rede/VPC-EndPoints.md)
- [Vpc](rede/VPC.md)

### 🗃️ Banco de Dados
- [Dynamodb](dados/DynamoDB.md)
- [Elasticache](dados/Elasticache.md)
- [Emr](dados/EMR.md)
- [Kinesis](dados/Kinesis.md)
- [Rds](dados/RDS.md)
- [Redshift](dados/Redshift.md)
- [Aurora](dados/Aurora/Aurora.md)
- [Aurora - Avançado](dados/Aurora/Aurora%20-%20Avan%C3%A7ado.md)

### 🛠️ Automação e Aplicações
- [API Gateway](automacao-e-aplicacoes/ApiGateway.md)
- [Cloudformation](automacao-e-aplicacoes/CloudFormation.md)
- [Elasticbeanstalk](automacao-e-aplicacoes/ElasticBeanStalk.md)
- [Elastictranscoder](automacao-e-aplicacoes/ElasticTranscoder.md)
- [Systems manager](automacao-e-aplicacoes/Systems%20Manager.md)

### 🧳 Migração e Transferência
- [Aws migration tools](migracao-e-transferencia/AWS%20Migration%20Tools.md)
- [Dms](migracao-e-transferencia/DMS.md)

### 🧪 Revisões e Erros de Simulado
- [Disasterrecovery](revisoes-e-erros/DisasterRecovery.md)
- [Duvidascomuns](revisoes-e-erros/DuvidasComuns.md)
- [Cost optimized architecture](revisoes-e-erros/Erros%20no%20simulado/Cost-Optimized%20Architecture.md)
- [High performancing architecture](revisoes-e-erros/Erros%20no%20simulado/High-Performancing%20Architecture.md)
- [Resilient architecture](revisoes-e-erros/Erros%20no%20simulado/Resilient%20Architecture.md)
- [Secure architectures](revisoes-e-erros/Erros%20no%20simulado/Secure%20Architectures.md)

### 📁 Outros
- [Readme](readme.md)
- [Cloudfront security](certificacoes/security-specialty/CloudFront-Security.md)
- [Directory services](certificacoes/security-specialty/Directory%20Services.md)
- [Duvidas comuns](certificacoes/security-specialty/Duvidas%20Comuns.md)
- [Logging](certificacoes/security-specialty/Logging.md)
- [Iam identity center](certificacoes/security-specialty/Acessos%20e%20Policies/IAM%20Identity%20Center.md)
- [Iam](certificacoes/security-specialty/Acessos%20e%20Policies/IAM.md)
- [Iampolicys indepth](certificacoes/security-specialty/Acessos%20e%20Policies/IAMPolicys-InDepth.md)
- [Rbps](certificacoes/security-specialty/Acessos%20e%20Policies/RBPs.md)
- [Session policies](certificacoes/security-specialty/Acessos%20e%20Policies/Session%20Policies.md)
- [Awsconfig](governanca-e-monitoramento/AWSConfig.md)
- [Control tower](governanca-e-monitoramento/Control%20Tower.md)
- [X ray](governanca-e-monitoramento/X-Ray.md)
- [Firewall manager](governanca-e-monitoramento/Organizations/Firewall%20Manager.md)
- [Organizations](governanca-e-monitoramento/Organizations/Organizations.md)
- [Sns](mensageria/SNS.md)
- [Sqs](mensageria/SQS.md)
- [Swf](mensageria/SWF.md)
