# CloudFormation
Esse é o serviço que permite provisionar e gerenciar recursos da AWS de forma "semiautomática" e segura, ==usando modelos de **infraestrutura como código(IaC)**==. Possibilita a criação e configuração de ambientes complexos por meio de templates que descrevem os recursos necessários (como instâncias EC2, VPCs, banco de dados, etc.) e suas configurações.

## Como funciona
- **Templates**: Você define um template em JSON ou YAML, que especifica todos os recursos AWS que a aplicação precisará.

- **Stacks**: É o conjunto de recursos que o CF cria com base no template. Quando o template for executado, o CF irá criar todos os recursos descritos. Se houver uma falha em algum recurso, o stack pode ser revertido automaticamente.

- **Automação de Deploy**: Ao usar o CF, você pode automatizar a criação, atualização e exclusão de pilhas de recursos. Isso é especialmente útil para garantir consistência entre ambientes (de homologação, teste e produção).

- **Controle de Versão**: Como os templates são definidos como código, você pode armazená-los em sistemas de controle de versão, como o Git, permitindo uma melhor auditoria das configurações.
---
## Conceitos Importantes
- **Outputs**: ==Seção opcional de um template do CF que declara valores a serem exportados, os quais poderão ser importados em outras stacks.== _**Caso de uso exemplar**: Ao definir uma stack de rede, você poderia exportar o ID da VPC como ouput e então importá-lo no stack da aplicação._

---
## Funções Intrínsecas
O CloudFormation possui algumas funções built-in bem úteis a criação de stacks. Vejamos algumas:

- **Ref ⮕** Usada para referenciar um parâmetro ou recurso AWS (ID do recurso). 
	- Em `YAML`: **`!Ref logicalName`**
	- **Obs:** O `!Ref` retorna somente o ID do recurso, se precisar de detalhes adicionais do recurso, use o `!GetAtt`.

- **Fn::GetAtt  ⮕** Retorna o valor de um atributo específico de um recurso AWS. 
	- Em `YAML`:  `!GetAtt logicalNameOfResource.attributeName`
	- **Caso de uso exemplar**: Obter a AZ que uma EC2 foi lançada, seu IP ou DNS público.
	
- **Fn::FindInMap ⮕** Retorna o valor baseado na chave enviada como parâmetro (Busca dentro de um `map` (Estrutura de dados com chave valor em `YAML`). 
	- Em `YAML`:  `!FindInMap [MapName, TopLevelkey, SecondLevelKey`
	- Veja um exemplo abaixo:
	 ![[ExemploMapping.png]]

- **Fn::ImportValue ⮕** Importa valores exportados em outras stacks.
	- Em `YAML`:  `!ImportValue exportedValueName`

- **Condition Functions (Fn::If, Fn::Not, Fn::Equals, etc...) ⮕** Realizar verificações e validações no momento de criação da stack.
	- Em `YAML`:  `!Equals [ value1, value2]

- **Fn::Base64 ⮕** Converte String para `Base64`.
	- Em `YAML`:  `!Base64 "ValueToEncode"
	- Muito utilizado para codificar dados a serem usados como `UserData` em uma instância EC2:
	- ![[Base64Example.png]]
---
## Infrastructure Composer
- O CloudFormation é integrado a um serviço bem legal, **o Infrastrucutre composer, que nos permite visualizar, construir e dar deploy em aplicações de maneira visual**, dá pra provisionar recursos num estilo **==Drag N' Drop==**! Muito legal. [GIF demonstativo](https://docs.aws.amazon.com/images/infrastructure-composer/latest/dg/images/aac_00.gif)
---
## CloudFormation StackSets
- Essa é uma feature que nos permite aplicar stacks do CF em múltiplas contas de uma só vez, a partir de uma conta de gerenciamento centralizada, tudo em uma única operação

- Este serviço é integrado ao **Organizations.**

---
## Deletion Policy
- Dentro do CloudFormation é possível definir uma política de deleção personalizada para quando a stack for excluída (ou caso o próprio recurso seja excluído). Veja os tipos de policies:

- **`Delete`**: Comportamento padrão, recurso é deletado (não funciona em um bucket S3 que não estiver vazio)
- **`Snapshot`**: Criará um snapshot final do recurso quando a stack for excluída.
- **`Retain`**: Recurso permanecerá mesmo se a stack for deletada.

---
## Rollbacks
- **Falha na ==CRIAÇÃO== de uma Stack:**
	- **==Por padrão**: Todos os recurso sofrem rollback (serão apagados)==, os logs fornecerão detalhes.
	- Há também a opção de desabilitar o rollback e solucionar o problema verificando diretamente o recurso.

- **Falha na ==ATUALIZAÇÃO ==de uma Stack:**
	- A Stack fará um ==rollback automático para o estado funcional mais recente==.

- ==**Falha no rollback*==:
	- Nesse caso ==será necessário consertar os recursos manualmente e então chamar a **API ContinueUpdateRollback**== diretamente do console ou CLI, isso fará com que o rollback tente ser feito novamente.