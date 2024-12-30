# Estudos AWS
Este é o meu repositório de estudos da plataforma AWS. Se quiser, você pode clonar este repositório para utilizar as minhas anotações também! :)


## Estudar
- [x] KMS envelope encryption: Caso o dado a ser criptografado é >4KB, use a API **GenerateDataKey**.

- [ ] **Data Key Caching**: Realiza o armazenamento em cache de chaves do KMS através do Encryption SDK. Garante uma melhor performance e redução de custos, pois evita chamadas de API desnecessárias.

- [x] **User groups nas user pools do Cognito**: Os user groups do Cognito permitem um gerenciamento de permissões mais eficiente, garantindo a possibiliade de filtrar permissões de acordo com o grupo que o usuários pertence.

- [ ] **Single e multi user rotation no Secrets Manager**
## Revisões e Detalhes

- **AWS Managed Keys**: Não é possível habilitar ou desabilitar a ==rotação automática== das chaves gerenciadas pela AWS, isso ==é feito automaticamente pela própria AWS no período de 1 ano.==

- **CMK**: É impossível rotacionar o conteúdo de uma Customer Managed Key. Podemos apenas criar uma nova com um outro conteúdo de criptografia.