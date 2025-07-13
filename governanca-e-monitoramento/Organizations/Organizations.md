# AWS Organizations
O **AWS Organizations** permite gerenciar várias contas da AWS de forma centralizada, a partir de uma **conta gerenciadora**. Ele facilita o controle de políticas, o gerenciamento de acesso e a otimização de custos em ambientes com múltiplas contas, como quando departamentos, projetos ou ambientes (produção, desenvolvimento, testes) usam contas separadas.

![Organizations](Organizations.png)
- Como mostrado na imagem acima, o **AWS Resource Access Manager (RAM)** pode ser utilizado para **compartilhar recursos entre contas**, como VPCs, subnets e licenças, unificando a infraestrutura entre elas.

- Para adicionar membros na organização, temos duas opções:
	1. **Convidar uma conta existente** para se juntar à organização. A conta deve aceitar o convite.
	
	2. **Criar uma nova conta** diretamente pelo console do AWS Organizations.
---
## Painel IAM - Organization Activity
No console do **IAM**, é possível acessar o painel "Organization Activity", que exibe os serviços utilizados (ou não utilizados) por cada conta da organização. Isso facilita a aplicação do princípio do **privilégio mínimo**.

---
## SCP
As **SCPs** são políticas organizacionais que permitem **restringir as permissões máximas** que uma conta, usuário ou role pode ter. Elas **não concedem permissões**, apenas impõem **limites máximos** ao que é permitido pelas políticas do IAM.

- ==Elas **não concedem permissões diretamente**, mas **limitam** as permissões que uma conta pode ter.== Em outras palavras, elas funcionam como uma camada extra de controle para **restringir permissões** que foram atribuídas por políticas do IAM.

- ==As SCPs **não se aplicam à conta gerenciadora**, esta sempre terá acesso irrestrito== (`AdministratorAccess`).

![[scp-hierarchy.png]]

- No exemplo acima:
	- A **OU** possui um _deny_ explícito para **S3**, bloqueando esse serviço para todas as contas dentro dela.
	- A **Conta A**, além do deny herdado da OU, possui um _deny_ próprio para **EC2**, bloqueando também esse serviço.

## Características
- **Conta gerenciadora**: Conta responsável pelo gerenciamento dos acessos, infraestrutura e pagamento de todas as outras que são partes da organização.

- **Conta membro**: Contas que pertencem à organização. São gerenciadas pela conta master.

- **Organizational Units (OU)**: Hierarquia para organizar contas em grupos lógicos, separando por departamento, projeto ou ambiente. facilitando a aplicação de políticas específicas para grupos de contas.

- **Service Control Policies (SCP)**: Políticas que definem o limite máximo de permissões para contas e OUs.

- **Feature Sets**: O AWS Organizations possui dois tipos de feature sets:
	- **Consolidated Billing features**: Com este aqui podemos consolidar todos os custos das diferentes contas em uma única fatura, facilitando o rastreamento de despesas.

	- **All features**: Este feature set é o mais recomendado e a maneira padrão de trabalhar com o Organzations, nele podemos definir integrações de serviços AWS que suportam centralização de dados da organização, além de também podermos aplicar SCPs. ==Este feature set é habilitado por padrão.==

- **Resource Access Manager (RAM)**: Permite que você compartilhe recursos AWS, como sub-redes VPC, gateways e licenças entre as contas da organização.

## Detalhes
- O AWS Organizations é um **serviço global**.

- As contas membro só podem fazer parte de uma organização por vez.

- O **Consolidated Billing** soma o uso de recursos entre contas, o que pode gerar **descontos por volume**.

- SCPs não se aplicam a conta gerenciadora (ela sempre terá `AdministratorAccess`)

- Você pode aninhar OUs (Colocar OU dentro de OU)

- ==SCPs se aplicam inclusive ao usuário root das contas membros.==

- ==A conta gerenciadora pode configurar uma **trilha do AWS CloudTrail em nível organizacional**==, coletando logs de todas as contas e regiões da organização.