# AWS Organizations
O Organizations tem como papel o gerenciamento de várias contas AWS a partir de uma única conta master, facilita muito o controle de políticas, gerenciamento de acessos e otimização de custos em larga escala. É especialmente útil para empresas que utilizam várias contas para diferentes departamentos, projetos ou ambientes (produção, desenvolvimento, etc.).

![Organizations](./images/Organizations.png)

- Como mostrado na imagem acima, através do VPC peering é possível ter uma única rede unificando os recursos de cada uma das contas.

## Características
- **Conta master**: Conta responsável pelo gerenciamento dos acessos, infraestrutura e pagamento de todas as outras que são partes da organização.

- **Conta membro**: Contas que pertencem à organização. São gerenciadas pela conta master.

- **Organizational Units (OU)**: Um tipo de hierarquia para organizar contas em grupos lógicos, separando por departamento, projeto ou ambiente. Isso facilita a aplicação de políticas específicas para grupos de contas.

- **Service Control Policies (SCP)**: Permitem definir políticas de permissões que são aplicadas em nível organizacional ou nas OUs. Com SCPs você pode restringir ou permitir acessos para contas vinculadas a uma estrutura da organização.

- **Consolidated Billing**: Com o Organizations, podemos consolidar todos os custos das diferentes contas em uma única fatura, facilitando o rastreamento de despesas.

- **Resource Access Manager (RAM)**: Permite que você compartilhe recursos AWS, como sub-redes VPC, gateways e licenças entre as contas da organização.