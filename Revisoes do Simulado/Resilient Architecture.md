# Questões Sobre Arquitetura Resiliente
Neste arquivo estão questões que eu errei sobre o design de arquiteturas resilientes.

___
## <span style="color:blue; background-color:#fff">Modo Standby</span>

**_A critical web application is deployed on multiple EC2 Instances which are part of an Autoscalling Group. One of the instances in the group needs a software upgrade. The Operations Team is looking for suggestions to advise for this ugrade without impacting another instance in the group. Post upgrade, the same instance should be part of the Auto Scaling group.
What Steps can be initated to complete this upgrade?_**

- [x] <span style="background-color:red; color:#fff"> Use cooldown timers to perform upgrades on the instance. Post cooldown timers' instances would be part of the same auto-scaling group.
</span>

- [ ] Hibernate the instance and perform upgrade in offline mode. Post upgrade, start the instance which will be part of the same auto-scaling group.

- [ ] <span style="background-color:green; color:#fff">Put the instance in Standby mode. Post upgrade, move instance back to InService mode. It will be part of the same auto-scaling group.
</span>

- [ ] Use lifecycle hooks to perform upgrades on the instance. Once these timers expire, the instance would be part of the same auto-scalling group.

### **Explicação**
**Instâncias em um grupo de auto-scaling podem ser colocadas em modo standby enquanto ficam no modo InService. No modo standby, é possível realizar upgrades de software e solucionar problemas técnicos.** Após o upgrade a instância pode ser colocada novamente em serviço no mesmo grupo que estava. O modo standby não é considerado uma falha para os health checks.

___

## <span style="color:blue; background-color:#fff">Falhas no Lambda</span>
***Sua organização precisa realizar análises de Big Data para transformar dados e armazenar os resultados em um bucket do AWS S3. Eles implementaram a solução usando AWS Lambda devido à natureza sem administração e ao custo efetivo do serviço. No entanto, em raros casos, a execução é interrompida abruptamente após 15 minutos. Eles gostariam de receber uma notificação nesses cenários. O que você faria?***

**Opções:**

- **A.** Configurar um timer no código e enviar uma notificação quando o temporizador atingir 900 segundos.

- **B.** Configurar SES para falhas na opção de Configuração dentro da função Lambda.

- **C.** <span style="background-color:red; color:#fff">Configurar a variável de ambiente ERROR_NOTIFY com um endereço de e-mail. A função Lambda tem um recurso interno para enviar um e-mail durante terminações causadas por tempo limite ou uso máximo de memória usando essa variável de ambiente.</span>

- **D.** <span style="background-color:green; color:#fff">Configurar uma Dead-letter Queue e enviar uma notificação para o tópico SNS.</span>

### **Explicação**

- Não existe nenhum recurso interno da lambda que faça envio de e-mail utilizando essa variável de ambiente `ERROR_NOTIFY`, é uma opção armadilha.

- A resposta corre é a D, pois é possível encaminhar cargas de trabalho que não foram processadas a tempo para uma fila "Dead Letter Queue", que funciona como se fosse um "banco de reservas" de mensagens.

___

## <span style="color:blue; background-color:#fff">Containers e Outposts</span>
**_A start-up firm is planning to deploy container-based applications using Amazon ECS. The firm is looking for the least latency from on-premises networks to the workloads in the containers. The proposed solution should be scalable and should support consistent high CPU and memory requirements._**

What deployment can be implemented for this purpose?

- [X] **A.** Create a Fargate launch type with Amazon ECS and deploy it in the AWS Outpost.
- [ ] **B.** Create a Fargate launch type with Amazon ECS and deploy it in the AWS Local Zone.
- [ ] **C.** Create an EC2 launch type with Amazon ECS and deploy it in the AWS Local Zone.
- [ ] **D.** <span style="background-color:green; color:#fff">Create an EC2 launch type with Amazon ECS and deploy it in the AWS Outpost.
</span>

### **Explicação**
- É possível fazer um deploy de Amazon ECS com o AWS Outposts, mas o _launch type_ só pode ser EC2, e não Fargate.

- Não é possível fazer um deploy IMEDIATO de ECS com o Local Zone, já que primeiro precisaria configurar uma infraestrutura completa com FSx e ALBs. ([ECS em Local Zones](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/cluster-regions-zones.html))
