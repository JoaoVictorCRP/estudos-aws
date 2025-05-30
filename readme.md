# Estudos AWS
Este é o meu repositório de estudos da plataforma AWS. Se quiser, você pode clonar este repositório para utilizar as minhas anotações também! :)


## Estudar
- [x] **Capacity Reservations**: As reservas de capacidade não garantem desconto nenhum, diferente das RIs e SPs. As CRs servem apenas para reservar hardware para você de maneira que evite que falte hardware para você em momentos de pico.

- [ ] **AWS Discovery Agent**

- [ ] **[RAID](https://docs.aws.amazon.com/pt_br/ebs/latest/userguide/raid-config.html) em Volumes EBS**

- [x] Deployment policies do Elastic BeanStalk

- [ ] Listeners em ALBs

- [ ] Slow Start Mode em um Target Group.

## Revisar
- **Replicas do Amazon Aurora**

## Detalhes para memorizar


- **AWS Managed Keys**: Não é possível habilitar ou desabilitar a ==rotação automática== das chaves gerenciadas pela AWS, isso ==é feito automaticamente pela própria AWS no período de 1 ano.==

- **Customer-Managed CMK**: É impossível rotacionar o conteúdo de uma Customer Managed CMK importada. Podemos apenas criar uma nova com um outro conteúdo de criptografia.

- **==As SCPs são aplicadas até mesmo ao usuário root da conta.**==

- **`DisableApiTermination` vs. Instance Protection**: DisableApiTermination impede ações de usuários, mas não do ASG. O Instance Protection faz o contário.