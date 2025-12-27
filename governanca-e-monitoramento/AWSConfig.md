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

## Conformance Packs
- Conjuntos pré-definidos de regras do AWS Config que ajudam a avaliar a conformidade dos recursos seguindo as melhores práticas e padrões de segurança da indústria.

- Permitem a implementação rápida de políticas de conformidade em toda a organização, uma vez que os Packs são definidos em formato YAML (facilmente importáveis).

- Você pode criar seus próprios Conformance Packs personalizados para atender às necessidades específicas da sua organização.
- Abaixo, um pequeno exemplo de um Conformance Pack em YAML:

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Resouces:
  IamPasswordPolicy:
    Type: 'AWS::Config::ConfigRule'
    Properties:
      ConfigRuleName: 'iam-password-policy'
      Description: 'Verifica se a política de senha do IAM atende aos requisitos mínimos.'
      Source:
        Owner: 'AWS'
        SourceIdentifier: 'IAM_PASSWORD_POLICY'
      InputParameters:
        minimumPasswordLength: '14'
        requireSymbols: 'true'
        requireNumbers: 'true'
        requireUppercaseCharacters: 'true'
        requireLowercaseCharacters: 'true'
```

- Você pode definir uma regra personalizada dentro do Conformance Pack, utilizando AWS Lambda para avaliar a conformidade dos recursos com base em critérios específicos da sua organização.
  - Neste caso, a propriedade `Source` deve ser ajustada para referenciar a função Lambda personalizada (`CUSTOM_LAMBDA`).


## Organizational Rules
- Permite a criação de regras do AWS Config que são aplicadas automaticamente a todas as contas dentro de uma organização do AWS Organizations.

- Facilita a implementação de políticas de conformidade consistentes em todas as contas da organização.

- As regras organizacionais podem ser gerenciadas centralmente, simplificando a administração e garantindo que todas as contas sigam as mesmas diretrizes de conformidade.

### Organizational Rules vs Conformance Packs
- Ambas as funcionalidades ajudam a gerenciar a conformidade em múltiplas contas, mas com abordagens diferentes.

- Conformance Packs podem ou não ser aplicados em nível organizacional, enquanto Organizational Rules são especificamente projetadas para serem aplicadas em todas as contas de uma organização.

- Ademais, Conformance Packs são conjuntos de regras que podem ser reutilizadas, enquanto Organizational Rules são regras individuais aplicadas diretamente às contas da organização.

<image src="./images/organizational-rules-vs-conformance-packs.png" alt="Organizational Rules vs Conformance Packs" width="600"/>

## Anotações
- Possui escopo regional, portanto você precisará ativar um AWS Config individual para cada região.

- É possível definir custom checks 

- O Config possui uma feature bem legal chamada auto-remediation, que realiza uma ação automática para resolver algum detalhe que esteja fora da conformidade, tudo de maneira nativa, sem precisar de lambda.