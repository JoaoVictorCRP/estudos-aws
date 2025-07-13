Serviço que oferece uma dashboard integrada para gerenciamento de segurança em uma ou várias contas AWS, permite também ativar checks de segurança.

- Integra os findings de diversos serviços de segurança da AWS, incluindo:
	- **Config**
	- **GuardDuty**
	- **Inspector**
	- **Macie**
	- **IAM Access Analyzer**
	- **AWS Systems Manager**
	- **AWS Firewall Manager**
	- **AWS Health**

- ==Para ativá-lo, é necessário primeiro habilitar o AWS Config.==


## Insights
- Os insights do Security Hub são coleções de findings correlacionadas que requerem atenção ou intervenção.
- Exemplo: Insight de uma instâncias EC2 com segurança deficitária. (Porta SSH aberta para internet, Envio anormal de requisições para IPs desconhecidos.)

## Principais Features

### Cross-Region Aggregation
- ==É possível unificar os findings, insights e o security score== de múltiplas regiões ==em uma única região== de sua preferência, que agregará estes pontos. ==Bem centralizado!==

### Integração com o Organizations
- Permite o gerenciamento de todas as contas no Organizations.
- Security Hub detecta automaticamente novas contas da organização, nada manual!
- POR PADRÃO, a conta administradora da organização é a gerenciadora do Security Hub, porém é possível delegar essa função para outra conta.

### Security Standards
- É possível incluir padrões de segurança que o security hub irá seguir, eles funcionam como guidelines para as automações de segurança.
![[SecurityStandards.png]]


## Integração com Terceiros
- É possível integrar o Security Hub com serviços de segurança de terceiros, tanto para receber findings deles quanto para enviar findings para eles.

- Exemplo: Receber alertas de segurança vindo do 3CoreSEC; Enviar alertas de segurança para o Atlassian (Jira).

