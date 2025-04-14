# AWS Config
O Config é uma ferramenta para ajustes e configurações dos seus recursos na AWS.
Vejamos aqui algumas funções deste serviço.

## <span style="background-color: #5946B2">Vigilância e Caguetagem</span>
Dentre as muitas funções do Config, uma delas é o monitoramento dos recursos ativados, modificados ou desativados por cada um dos usuários da conta AWS. **Basicamente, atuando como uma versão simplificada e menos técnica do Cloudtrail.**


## <span style="background-color: #ffd966; color: black">Administração Centralizada</span>
### Avaliação de recursos
Através do Config é possível criar verificações de seus recursos baseando-se em regras, como por exemplo: "Sempre que detectar um volume EBS não criptografado, me informe". Como você pode imaginar, ele também pode se integrar com o SNS.

### Auditoria
Com o config é possível auditar a data da criação de um recurso, por quem ele foi criado e qual foi a configuração inicial do recurso. Muito interessante.

### Conformidade com diretrizes
Também é possível checar uma linha do tempo de eventos associados a um recursos inspecionado, isto é, mostrando em uma estaca de tempo toda a vida de uma instância, por exemplo, quando ela teve um ENI removida, quando ela teve um novo security group adicionado e quando ela foi desligada, deixando claro qual usuário fez isso e quando.


## <span style="background-color: #6a329f;">Histórico de tudo</span>
Pelo fato desse serviço ser integrado ao CloudTrail, ele guarda o histórico de tudo o que ocorre na região onde ele foi lançado.


## Anotações
- Possui escopo regional, portanto você precisará ativar um AWS Config individual para cada região.

- É possível definir custom checks 

- O Config possui uma feature bem legal chamada auto-remediation, que realiza uma ação automática para resolver algum detalhe que esteja fora da conformidade, tudo de maneira nativa, sem precisar de lambda.