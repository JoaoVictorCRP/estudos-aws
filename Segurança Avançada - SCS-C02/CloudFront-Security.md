Nesta anotação falaremos um pouco sobre o serviço de IaC da AWS, o CloudFront. Que, como sabemos, nos permite provisionar infraestrutura de maneira declarativa, evitando a falha humana que muitas vezes ocorre na criação manual.

---
## Service Role
- As service roles do CloudFormation permite que possamos atribuir uma role à uma stack específica.

- A atribuição de uma role ==**serve para restringir as permissões do CF==**, de modo que se use apenas as necessárias para gerenciar os recursos especificados.

- Garante conformidade, pois o CF só irá operar dentro dos limites de segurança da organização.
---
## Stack Policies
**Por padrão**, durante o processo de atualização de uma Stack, todas as ações de atualização estão permitidas em **TODOS OS RECURSOS**. *(Ou seja: imagine, por exemplo, que você tem uma instância RDS nessa stack, e após uma pequena atualização no código CF, o banco vai pro saco... Poxa!)*

Por isso é que existem as **Stack Policies,** que **==são documentos JSON que definem as ações de update que são permitidas durante a atualização de uma Stack==**!

- **Resumindo**: Stack policies nos protegem de atualizações não intencionais.
---
## Referenciação Dinâmica
- É possível referenciar valores sensíveis, como parâmetros armazenados no **Parameter Store** ou no **Secrets Manager**, diretamente no código do CloudFormation, utilizando **referenciação dinâmica**.

- Exemplos:
    - Para acessar um segredo no **Parameter Store**:  
        `!Sub "{{resolve:ssm-secure:NomeParametro}}"`.
    - Para acessar um segredo no **Secrets Manager**:  
        `!Sub "{{resolve:secretsmanager:NomeDoSegredo}}"`.

- **Dica adicional:** Destaque que o uso da referenciação dinâmica elimina a necessidade de expor valores sensíveis diretamente no código do template CloudFormation.
---
### Drift Detection
Quando o Drift Detection é executado, ele **compara o estado atual dos recursos da stack com o estado esperado definido no template**. **Caso haja discrepâncias, um alerta será gerado.**

- Exemplo: 
	- Se o **Security Group** de uma instância for alterado manualmente (fora do CloudFormation), o Drift Detection detectará essa alteração e exibirá um alerta no console do CloudFormation.

---
## CloudFormation Guard (cfn-guard)
O **cfn-guard** é uma **==ferramenta open-source da AWS que ajuda a validar os templates do CF em relação a políticas de conformidade e boas práticas antes de aplicar as stack**s==.

##### Como Funciona?
- **Definição de Regras (`Rules`)**:
	- Você define um conjunto de **regras** de maneira declarativa.
	- As regras especificam critérios que os recursos de um template devem cumprir, como:
		- Tipos de instâncias permitidos.
		- Restrições de tamanho de volumes EBS.
		- Criptografia obrigatória em buckets S3.

- **Validação (`Validate`):**
	- O cfn-guard analisa o template do CloudFormation e o valida contra as regras definidas.
	- Ele retorna um relatório com os **erros encontrados** e as **violação das regras**.