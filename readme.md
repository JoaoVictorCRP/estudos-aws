# Estudos AWS
Este é o meu repositório de estudos da plataforma AWS. Se quiser, você pode clonar este repositório para utilizar as minhas anotações também! :)


## Estudar
- [ ] **Capacity Reservations**

- [ ] **AWS Discovery Agent**

- [ ] **[RAID](https://docs.aws.amazon.com/pt_br/ebs/latest/userguide/raid-config.html) em Volumes EBS**

## Revisões e Detalhes

- **WAF Rules**

- **Deployment Policies do Beanstalk**

- **AWS Managed Keys**: Não é possível habilitar ou desabilitar a ==rotação automática== das chaves gerenciadas pela AWS, isso ==é feito automaticamente pela própria AWS no período de 1 ano.==

- **Customer-Managed CMK**: É impossível rotacionar o conteúdo de uma Customer Managed CMK importada. Podemos apenas criar uma nova com um outro conteúdo de criptografia.

- **==As SCPs são aplicadas até mesmo ao usuário root da conta.**==