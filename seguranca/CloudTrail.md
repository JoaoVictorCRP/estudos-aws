# Cloudtrail
O **CloudTrail** é uma ferramenta essencial para auditoria das contas AWS. Esse serviço registra todas as chamadas de API dentro da conta ou da organização. Indicando qual foi o usuário, qual serviço ele utilizou e em qual horário.

## Trails
- Trilhas (Trails) são configurações no CloudTrail que determinam como e onde os logs **serão armazenados**.

- Por padrão, o Cloudtrail registra eventos de até 90 dias.

- Para armazenar logs de longo prazo, é necessário configurar uma trilha persistente que salva os eventos em um **bucket S3, CloudWatch Logs ou Eventbridge**.

## Tipos de Evento
O CT captura dois tipos principais de eventos, são eles:

1. **Eventos de Gerenciamento (Management Events)**
	- Registra ações relacionadas à configuração da conta e gerenciamento de recursos.
	- Exemplo: 
		- Criação de um usuário IAM
		- Modificação de permissões
		- Rotação de chaves do KMS.
	- ✅**Ativado por padrão.** (retém logs no console por 90 dias).

2. **Eventos de Dados (Data Events)**
	- Registra chamadas diretas a dados em serviços como S3, DynamoDB, Lambda.
	- Exemplo: 
		- Download de arquivos no S3,
		- Leitura de uma tabela DynamoDB, 
		- Execução de uma função Lambda.
	- ==⚠ **NÃO É ATIVADO POR PADRÃO**== (Precisa se habilitado manualmente).


## Tipos de Trails
1. Single-Region Trail
	- Registra eventos apenas na região em que foi criada.
	- Boa para auditoria em cenários menores e ambientes menos distribuídos.

2. Multi-Region Trail (Trilha global)
	- Registra eventos em todas as regiões da AWS automaticamente.
	- Ideal para **contas corporativas** e **ambientes multi-region**.
	- Captura **ações globais**, como mudanças no IAM ou no CloudFront.

3. Organization Trail
	- Registra eventos de todas as contas dentro de uma organização AWS (AWS Organizations).
	- Centraliza o monitoramento e auditoria em ambientes com múltiplas contas.
	- Requer permissões adequadas na conta master da organização.

## Log File Integrity Validation
- Recurso que garante que os arquivos de log do CloudTrail não foram alterados ou corrompidos após serem gravados em um **bucket S3**.

- Utiliza **hashes criptográficos** para verificar a integridade dos arquivos de log. Muito útil para auditorias de segurança e conformidade.