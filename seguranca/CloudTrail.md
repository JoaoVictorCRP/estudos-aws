O **CloudTrail** é uma ferramenta essencial para auditoria das contas AWS. Esse serviço registra todas as chamadas de API dentro da conta ou da organização. Indicando qual foi o usuário, qual serviço ele utilizou e em qual horário.

### Trails
- Trilhas (Trails) são configurações no CloudTrail que determinam como e onde os logs **serão armazenados**.

- ==Por padrão, o **Cloudtrail registra eventos por 90**, mas somente no console da AWS, sem persistência.==

- Para armazenar logs de longo prazo, é necessário configurar uma trilha persistente que salva os eventos em um **bucket S3, CloudWatch Logs ou SNS**.

### Tipos de Evento
O CT captura dois tipos principais de eventos, são eles:

1. **Eventos de Gerenciamento (Management Events)**
	- Registra ações relacionadas à configuração da conta e gerenciamento de recursos.
	- Exemplo: **Criação de um usuário IAM, modificação de permissões, rotação de chaves do KMS.**
	- ✅**Ativado por padrão.** (retem logs no console por 90 dias).

2. **Eventos de Dados (Data Events)**
	- Registra chamadas diretas a dados em serviços como **S3, DynamoDB, Lambda.**
	- Exemplo: **Download de arquivos no S3**, leitura de uma tabela DynamoDB, execução de uma função Lambda.
	- ==⚠==**NÃO É ATIVADO POR PADRÃO** (Precisa se habilitado manualmente).


### Tipos de Trails
1. Single-Region Trail
	- Registra eventos apenas na região em que foi criada.
	- Boa para auditoria em cenários menores e ambientes menos distribuídos.

2. Multi-Region Trail (Trilha global)
	- Registra eventos em todas as regiões da AWS automaticamente.
	- Ideal para **contas corporativas** e **ambientes multi-region**.
	- Captura **ações globais**, como mudanças no IAM ou no CloudFront.