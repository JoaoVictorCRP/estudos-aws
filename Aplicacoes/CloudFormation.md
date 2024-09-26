# CloudFormation
Esse é o serviço que permite provisionar e gerenciar recursos da AWS de forma "semi-automática" e segura, <span style="background-color: #e0a800; color: black;font-weight:bold">usando modelos de **infraestrutura como código(IaC)**</span>. Possibilita a criação e configuração de ambientes complexos por meio de templates que descrevem os recursos necessários (como instâncias EC2, VPCs, banco de dados, etc.) e suas configurações.


## Como funciona:
- **Templates**: Você define um template em JSON ou YAML, que especifica todos os recursos AWS que a aplicação precisará.

- **Stacks**: É o conjunto de recursos que o CF cria com base no template. Quando o template for executado, o CF irá criar todos os recursos descritos. Se houver uma falha em algum recurso, o stack pode ser revertido automaticamente.

- **Automação de Deploy**: Ao usar o CF, você pode automatizar a criação, atualização e exclusão de pilhas de recursos. Isso é especialmente útil para garantir consistência entre ambientes (de homologação, teste e produção).

- **Controle de Versão**: Como os templates são definidos como código, você pode armazená-los em sistemas de controle de versão, como o Git, permitindo uma melhor auditoria das configurações.