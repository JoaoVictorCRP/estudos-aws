# Auto Scaling
Esse é o <span style="background-color: #e0a800; color: black;font-weight:bold">serviço que ajusta automaticamente a capacidade dos seus recursos de computação com base nas demandas da aplicação</span>. Ele garante que você tenha o número correto de instância disponíveis para lidar com o tráfego, aumentando ou diminuindo o número de instâncias em resposta à carga de trabalho.

## Compontentes do AS

- **Groups (ASG)**
    - Componentes lógicos. Grupos de webservers, aplicações ou banco de dados.

- **Launch Templates**
    - <span style="background-color: #e0a800; color: black;font-weight:bold">Definem as configurações de inicialização usadas pelo ASG para lançar instâncias EC2</span>. Esses templates permitem ajustar diversos detalhes da EC2, como:
        - AMI
        - Tipo de instância
        - Key Pairs
        - Security Groups
        - Rede e Subrede

- **Scaling Options**
    - Fornece diferentes estratégias para ajustar a capacidade dos ASGs. Isso pode ser feito com base em condições dinâmicas (Dynamic Scaling) ou através de agendamento.

## Tipos de Escalonamento
### Nível Fixo
- Mantém um número específico de instâncias rodando continuamente.

- Realiza verificações periódicas de saúde (**Health Checks**) nas instâncias.

- Se uma instância for detectada como **Unhealthy**, ela será substituída automaticamente por uma nova.

### Escalonamento Manual
- Permite ajustar manualmente o número mínimo, máximo ou desejado de instâncias no ASG

- <span style="background-color: #e0a800; color: black;font-weight:bold">Embora o escalonamento seja feito manualmente, o Auto Scaling gerencia a criação ou remoção das instâncias automaticamente com base nos parâmetros fornecidos.</span>

## Políticas de Escalonamento Automático
### Scheduled Scalling
- Ocorre com base em horários e datas predefinidos.

- <span style="background-color: #e0a800; color: black;font-weight:bold">Ideal para situações onde você sabe com antecedência quando haverá picos ou quedas de demanda.</span>
___
###  Dynamic Scaling
#### Target Tracking
- Define um alvo para o uso de recursos do ASG
- Simples de configurar
- Exemplo: "Uso médio da CPU deve ficar abaixo de 50%"

#### Simple / Step Scaling (==Integração com CW==)
- Quando um alarme do CW disparar (Exemplo: CPU > 70%), adicione mais 2 EC2s.
___
### Predictive Scaling
- Neste método, o ASG analisa dados históricos de carga para escalonar automaticamente baseado em horários e datas.

## Integração com Alarmes do CloudWatch
- É possível escalonar um ASG baseado nos alarmes do CloudWatch
![ASG e CloudWatch](ASGeCloudWatch.png)

- O Alarme é baseado em uma métrica, por exemplo: "Consumo médio da CPU do ASG está muito alto", daí aumentar número de instâncias.

- Dá pra integrar com outros serviços da AWS, tipo o SQS, utilizando a métrica "número máximo de mensagens na fila", por exemplo.

- Baseado no alarme, é possível aumentar (scale-out) ou diminuir(scale-in) o número de instâncias.

___
### Launch Template VS. Launch Configuration
É bem possível que no exame SAA-C03 caia perguntas que tracem comparações entre LT e LC. Vejamos as diferenças:

#### Launch Configuration 🗿
- ==Versão mais antiga e básica de se configurar um grupo de auto-scaling.==
- **Configuração é fixa**: Uma vez criada, não pode mais ser modificada. Da idade da pedra mesmo.
- **Opções limitadas**: Inclui configurações básicas, como tipo de instância, AMI, par de chaves e opções de rede.

#### Launch Template 🚀
- ==Mais moderno e flexível. Feito para ser uma versão atualizada do launch configuration.==
- **Versionamento e alterações**: Com launch templates, você pode criar múltiplas versões para ajustes sem precisar recriar tudo, como era no LC.
- **Opções Avançadas**: É possível selecionar diversas opções mais específicas, como:
	- Modelo de pagamento da instância;
	- Configuração avançada de rede (múltiplas interfaces, IPs adicionais);
	- Tags de instância (que são passadas para os recursos criados)
	- Criptografia do volume EBS.

---
## Tipos de Health Checks
Os Auto-Scalling groups podem checar a saúde das instâncias de dois tipos:

- ==**EC2**: O check via EC2 monitora a saúde do servidor apenas a nível de instância==, isto é, só vai verificar se o estado é **"`running`"**, deixando detalhes adicionais como estado da aplicação ou serviços internos de lado.

- **ELB**: ==O check via **ELB** permite monitorar o estado da própria aplicação hospedada na instância, isso através do envio de uma requisição para um endpoint específico, que é enviada para as instâncias do target group em um intervalo de tempo definido por você.== Isso permite um monitoramento mais detalhado e interessante. 

**Qual se deve usar?**
R: Depende, se quiser verificar a disponibilidade real da aplicação ou serviços na instância, use o **Health Check ELB**, caso uma verificação simples bastar, use **Health Check EC2**.
___
## ANOTAÇÕES
- <span style="color:red; font-weight: bold"> NÃO CONFUNDA AUTO-SCALLING GROUPS COM PLACEMENT GROUPS </span>
- Para corrigir algum erros em instâncias de um ASG, basta colocá-la em modo stand-by temporáriamente.
- Quando ocorre um balanceamento, o Auto Scalling cria novas instâncias antes de terminar as antigas, para que a aplicação não tenha sua performance ou disponibilidade comprometida.