# Estudos AWS
Este é o meu repositório de estudos da plataforma AWS. Se quiser, você pode clonar este repositório para utilizar as minhas anotações também! :)


## Estudar
- [x] KMS envelope encryption: Caso o dado a ser criptografado é >4KB, use a API **GenerateDataKey**.
- [ ] **Data Key Caching**
- [ ] **User groups nas user pools do Cognito**
- [ ] **Single e multi user rotation no Secrets Manager**
## Revisões e Detalhes

- **AWS Managed Keys**: Não é possível habilitar ou desabilitar a ==rotação automática== das chaves gerenciadas pela AWS, isso ==é feito automaticamente pela própria AWS no período de 1 ano.==

- **CMK**: É impossível rotacionar o conteúdo de uma Customer Managed Key. Podemos apenas criar uma nova com um outro conteúdo de criptografia.