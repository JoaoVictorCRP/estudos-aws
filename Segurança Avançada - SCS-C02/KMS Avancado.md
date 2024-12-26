Neste documento veremos alguns detalhes mais avançados do KMS.

## Chaves Importadas
Quando lidamos com uma chave que possui conteúdo importado externamente (**CMK**), precisamos entender alguns detalhes:

- Você é 100% responsável pela segurança, disponibilidade e durabilidade da chave fora da AWS.

- A rotação deve ser feita manualmente. (Automatic Key Rotation não funciona aqui).

- Tanto chaves **Simétricas** (chave única) quanto **Assimétricas** (par de chaves) são suportadas.

## Envelope Encryption
O Envelope Encryption deve ser utilizado para criptografar um dado maior que 4KB (4.096 bytes) utilizando o KMS. Pois a API principal tem este limite de tamanho.

- **Para fazer uso do Envelope Encryption, você deve chamar a API ==GenerateDataKey==**

**DICA DE OURO:** Se no exame cair que você precisa criptografar um dado maior que 4KB , dá-lhe **GenerateDataKey.**


## KMS Grants
- Permite garantir acesso a chaves específicas do KMS para outras contas AWS, também pode ser usado com usuários e roles dentro da própria conta.

- ==**Podemos conceder acesso temporário**. ==(É justamente isso que destaca esse recurso perante a uma key policy ou permissão direta do IAM)

- ==1 Grant pode ser usado apenas em uma chave do KMS, porém, pode ser aplicado a mais de uma entidade==. (IAM Principal)

- Grants não são deletados automaticamente, é preciso deletá-los manualmente.

- **Garante acesso sem precisar alterar key policy ou permissões dos usuário**.

- Os grants **são muito utilizados pela própria AWS para garantir acesso de recursos a uma chave KMS específica**. 

	- Veja um diagrama abaixo de como funciona "por debaixo dos panos" com uma EC2 com volume criptografado com chave do KMS:
		![[KMS-Grant.png]]