Para cumprir com requisitos de conformidade, a AWS possui diversos serviços para geração e armazenamento de logs para auditoria.

## Principais Serviços de Log

- **CloudTrail Trails**: As trilhas do CT permitem traçar todas as chamadas de API da conta.

- **Config Rules**: O Config permite captura de registro de modificação de um recurso ao longo do tempo.

- **CloudWatch Logs**: Para retenção total de dados de registro.

- **VPC Flow Logs**: Feito para rastrear todo o tráfego dentro da sua VPC.

- **ELB Access Logs**: Metadados de requisições feitas ao Load Balancer

- **CloudFront Logs**: Logs de acesso de uma distribuição web.

- **WAF Logs**: Gera logs de todas requisições analisadas pelo WAF.


## Anotações
- ==Os logs podem ser analisados rapidamente utilizando o Amazon Athena==, caso eles estejam armazenados em um bucket S3.

- Para arquivar os logs, use o S3 Glacier, e se quiser proteger estes logs, dá pra usar um Vault Lock para cumprir ainda mais com requisitos de conformidade.

- Para garantir a integridade dos logs entregues pelo CloudTrail, habilite a opção _"**Cloudtrail log file integrity validation**"_. 

- Por padrão, os logs do CloudTrail são criptografados utilizando uma chave S3-SSE. É possível também definir uma lifecycle rule para arquivar ou deletar os logs automaticamente.

- Os ==logs do **CloudTrail** de serviços globais==, como o IAM, CloudFront e STS ==são registrados somente na região *us-east-1*.==

- É possível estabelecer uma trilha do CloudTrail em uma organização inteira direto da conta administradora/gerenciadora. Como foi referido na nota do [[Organizations#Detalhes]].