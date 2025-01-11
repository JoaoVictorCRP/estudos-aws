# Estudos AWS
Este é o meu repositório de estudos da plataforma AWS. Se quiser, você pode clonar este repositório para utilizar as minhas anotações também! :)


## Estudar
- [x] KMS envelope encryption: Caso o dado a ser criptografado é >4KB, use a API **GenerateDataKey**.

- [x] **Data Key Caching**: funcionalidade do AWS **Encryption SDK** que permite armazenar em cache **Data Keys** geradas pelo AWS KMS, evitando chamadas desnecessárias à API do KMS, **melhorando a performance e reduzindo os custos operacionais**.

- [x] **User groups nas user pools do Cognito**: Os user groups do Cognito permitem um gerenciamento de permissões mais eficiente, garantindo a possibiliade de filtrar permissões de acordo com o grupo que o usuários pertence.

- [x] **Single e multi user rotation no Secrets Manager**: Estratégias para rotação de segredos relacionados a uma instância RDS. O single user utiliza as credenciais armazenadas no próprio secret para fazer a rotação. O multi user cria um clone do usuário armazenado durante a rotação para auxliar na alteração da senha do usuário principal.

- [x] **Traffic Mirroring para sniffing**: Se quiser inspecionar pacotes de rede para solução de problemas na infraestrutura, você deve configurar uma ferramenta de monitoramento em uma instância, como o _Wireshark_, por exemplo. A partir disto, você deve habilitar o traffic mirroring na VPC para que você possa copiar dados de tráfego de uma *ENI (Elastic Network Interface)* e enviá-los para outra.

- [x] **SSE-C para criptografia de buckets S3**: É possível estabelecer criptografia *server-side* em objetos utilizando uma chave fornecida por você, cliente, estas são chamdas _customer-provided keys_. Desta forma, você não precisa realizar criptografia *client-side*(antes de realizar o upload) para usar a sua própria chave, basta configurar esta chave na AWS.

- [x] **AWS PCA (Private Certificate Authority)**: Serviço para emissão de certificados TLS/SSL privados (que são usados internamente), incluído no ACM.

- [ ] **Segurança no CloudFormation** 

- [ ] **Certificados nos Listeners do ELB**

## Revisões e Detalhes

- **AWS Managed Keys**: Não é possível habilitar ou desabilitar a ==rotação automática== das chaves gerenciadas pela AWS, isso ==é feito automaticamente pela própria AWS no período de 1 ano.==

- **Customer-Managed CMK**: É impossível rotacionar o conteúdo de uma Customer Managed CMK importada. Podemos apenas criar uma nova com um outro conteúdo de criptografia.
