Neste documento veremos alguns detalhes mais avançados do KMS.

## Chaves Importadas
Quando lidamos com uma chave que possui conteúdo importado externamente (**CMK**), precisamos entender alguns detalhes:

- Você é 100% responsável pela segurança, disponibilidade e durabilidade da chave fora da AWS.

- A rotação deve ser feita manualmente. (Automatic Key Rotation não funciona aqui).

- Tanto chaves **Simétricas** (chave única) quanto **Assimétricas** (par de chaves) são suportadas.

## Envelope Encryption
O Envelope Encryption deve ser utilizado para criptografar um dado maior que 4KB (4.096 bytes) utilizando o KMS. Pois a API principal (`kms:encrypt`) tem este limite de tamanho.

- **Para fazer uso do Envelope Encryption, você deve chamar a API ==GenerateDataKey==**

**Dica:** Se no exame cair que você precisa criptografar um dado maior que 4KB, dá-lhe **GenerateDataKey.**


## KMS Grants
- **Permite garantir acesso a chaves específicas do KMS para outras contas AWS**, também pode ser usado com usuários e roles dentro da própria conta.

- **Podemos conceder acesso temporário**, e é justamente isso que destaca esse recurso perante a uma key policy ou permissão direta do IAM.

- ==1 Grant pode ser usado apenas em uma chave do KMS, porém, pode ser aplicado a mais de uma entidade== (IAM Principal).

- Grants não são deletados automaticamente ao excluir a chave do KMS, mas eles se tornam inativos e não concedem mais acesso.

- **Garante acesso sem precisar alterar key policy ou permissões dos usuário**.

- Os grants **são muito utilizados pela própria AWS para garantir acesso de recursos a uma chave KMS específica**. 

	- Veja um diagrama abaixo de como funciona "por debaixo dos panos" com uma EC2 com volume criptografado com chave do KMS:
		![[../images/KMS-Grant.png]](../images/KMS-Grant.png)

## Alias 
Um **Alias** no KMS funciona como um ==apelido para referenciar uma chave de criptografia==. Ele é usado para facilitar o gerenciamento e a referência às chaves sem precisar lidar diretamente com o **ARN** ou **ID da chave**.

- Cada Alias é associado a **uma** key.
- Uma key pode ter mais de um Alias apontando para ela.
- Todo Alias deve começar com o prefixo `alias/`

#### Casos de uso
- **Rotacionamento de Chaves**: Em vez de atualizar cada recurso ou aplicação para usar uma nova key, você cria uma nova key e aponta o Alias existente para ela.
	- Exemplo:
		- Antes: `alias/my-key` -> Key antiga
		- Depois: `alias/my-key` -> Key nova
- **Segurança e boa prática**: Usar aliases em vez de IDs de chave diretamento no código reduz o risco de erros humanos e facilita auditorias.