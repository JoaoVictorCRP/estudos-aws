# Revisões - EC2
Aqui estão algumas perguntas sobre instâncias EC2 que eu errei no simulado.

- <span style="background-color:red; color:#fff"> Em vermelho, a resposta que eu assinalei.</span>

- <span style="background-color:green; color:#fff">Em verde, a reposta correta.
</span>

## Migração On-premise x AWS
>_**A persistent database must be migrated from an on-premises server to an Amazon EC2 instances. The database requires 64,000 IOPS and, if possible, should be stored on a single Amazon EBS volume. 
<br>
Which solution should a Solutions Architect recommend?**_


- [x] <span style="background-color:red; color:#fff">Use an instance from the I3 I/O optimized family and leverage instance store storage to achieve the IOPS requirement.
</span>

- [ ] <span style="background-color:green; color:#fff"> Create a Nitro-based Amazon EC2 instance with an Amazon EBS Provisioned IOPS SSD (io1) volume attached. Provision 64,000 IOPS for the volume.
</span>

- [ ] Create an Amazon EC2 instance with four Amazon EBS General Purpose SSD (gp2) volumes attached. Max out the IOPS on each volume and use a RAID 0 stripe set.

- [ ] Create an Amazon EC2 instance with two Amazon EBS Provisioned IOPS SSD (i01) volumes attached. Provision 32,000 IOPS per volume and create a logical volume using the OS that aggregates the capacity.

### Explicação
Instâncias EC2 Nitro-based oferecem vantagens na performance que irão ajudar otimizar o uso do volume EBS. Para este volume, podemos selecionar **um Provisioned IOPS (io1),** que **suporta até 64,000 IOPS**, então um único volume com capacidade suficiente poderia cumprir os requisitos.

_**Read the docs**_: [EBS Volume Types](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volume-types.html)

## Auto Scalling

### AS + Dynamo DB
> **_An eCommerce application consists of three tiers. The web tier includes EC2 instances behind an Application Load balancer, the middle tier uses EC2 instances and an Amazon SQS queue to process orders, and the database tier consists of an Auto Scaling DynamoDB table. During busy periods customers have complained about delays in the processing of orders. A Solutions Architect has been tasked with reducing processing times.<br>
Which action will be MOST effective in accomplishing this requirement?_**

- [x] <span style="background-color:red; color:#fff"> Use Amazon DynamoDB Accelerator (DAX) in front of the DynamoDB backend tier.
</span>

- [ ] Add an Amazon CloudFront distribution with a custom origin to cache the responses for the web tier.

- [ ] <span style="background-color:green; color:#fff"> Use Amazon EC2 Auto Scaling to scale out the middle tier instances based on the SQS queue depth.
</span>

- [ ] Replace the Amazon SQS queue with Amazon Kinesis Data Firehose.

#### Explicação
A causa mais provável da lentidão é a quantidade insuficiente de instâncias na camada média da aplicação, onde ocorrer o processamento dos pedidos. A soluçãoi mais efetiva para reduzir o tempo de processamento seria etnão escalonar baseado no número de mensagem na fila do SQS, pois isso reflete a quantidade de trabalho que precisa ser feito.

**Meu erro**: O DynamoDB é natualmente equipado com escalonagem automática, portanto o problema não está nele. Além do mais, o DynamoDB nem realiza processamento de dados.

### Modo Standby
>**_A critical web application is deployed on multiple EC2 Instances which are part of an Autoscalling Group. One of the instances in the group needs a software upgrade. The Operations Team is looking for suggestions to advise for this ugrade without impacting another instance in the group. Post upgrade, the same instance should be part of the Auto Scaling group. <br><br>
What Steps can be initated to complete this upgrade?_**

- [x] <span style="background-color:red; color:#fff"> Use cooldown timers to perform upgrades on the insance. Post cooldown timers' instances would be part of the same auto-scaling group.
</span>

- [ ] Hibernate the instance and perform upgrade in offline mode. Post upgrade, start the instance whic will be part of the same auto-scaling group.

- [ ] <span style="background-color:green; color:#fff"> Put the instance in Standby mode. Post upgrade, move instance back to InService mode. It will be part of the same auto-scaling group.
</span>

- [ ] Use lifecycle hooks to perform upgrades on the instance. Once these timers expire, the instance would be part of the same auto-scalling group.

#### Explicação
**Instâncias em um grupo de auto-scaling podem ser colocadas em modo standby enquanto ficam no modo InService. No modo standby, é possível realizar upgrades de software e solucionar problemas técnicos.** Após o upgrade a instância pode ser colocada novamente em serviço no mesmo grupo que estava. O modo standby não é considerado uma falha para os health checks.