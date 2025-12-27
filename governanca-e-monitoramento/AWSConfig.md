# AWS Config
O Config é uma ferramenta para ajustes e configurações dos seus recursos na AWS.
Vejamos aqui algumas funções deste serviço.

## Vigilância e Caguetagem
Dentre as muitas funções do Config, uma delas é o monitoramento dos recursos ativados, modificados ou desativados por cada um dos usuários da conta AWS. Atuando basicamente como uma versão simplificada e menos técnica do Cloudrail.


## Administração Centralizada
### Avaliação de recursos
Através do Config, é possível criar verificações de seus recursos baseando-se em regras, como por exemplo: "Sempre que detectar um volume EBS não criptografado, me informe". Como você pode imaginar, ele também pode se integrar com o SNS.

### Auditoria
Com o Config é possível auditar a data da criação de um recurso, por quem ele foi criado e qual foi a configuração inicial do recurso. Muito interessante.

### Conformidade com diretrizes
Também é possível checar uma linha do tempo de eventos associados a um recursos inspecionado, isto é, mostrando em uma estaca de tempo toda a vida de uma instância, por exemplo, quando ela teve um ENI removida, quando ela teve um novo security group adicionado e quando ela foi desligada, deixando claro qual usuário fez isso e quando.


### Histórico de ações
Pelo fato desse serviço ser integrado ao CloudTrail, ele guarda o histórico de tudo o que ocorre na região onde ele foi lançado.


## Configuration Recorder
- Grava as configurações dos recursos da AWS em sua conta.
- Pode ser configurado para gravar todas as mudanças ou apenas mudanças específicas, permitindo uma auditoria detalhada das alterações feitas nos recursos.

## Aggregator
- Permite agregar dados de configuração de várias contas e regiões da AWS em um único local.
- Facilita a visualização e análise das configurações em um ambiente multi-conta e multi-região.
- **As regras devem ser criadas em cada conta/região de origem**.


## Anotações
- Possui escopo regional, portanto você precisará ativar um AWS Config individual para cada região.

- É possível definir custom checks 

- O Config possui uma feature bem legal chamada auto-remediation, que realiza uma ação automática para resolver algum detalhe que esteja fora da conformidade, tudo de maneira nativa, sem precisar de lambda.