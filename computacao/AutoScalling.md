# Auto Scaling
Esse é o ==serviço que ajusta automaticamente a capacidade dos seus servidores com base nas demandas da aplicação==. Ele garante que você tenha o número correto de instância disponíveis para lidar com o tráfego, aumentando ou diminuindo o número de instâncias em resposta à carga de trabalho.

## Compontentes do AS

- **Groups (ASG)**
    - Componentes lógicos. Grupos de webservers, aplicações ou banco de dados.

- **Launch Templates**
    -  Definem as configurações de inicialização usadas pelo ASG para lançar instâncias EC2. Esses templates permitem ajustar diversos detalhes da EC2, como:
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

- Embora você defina manualmente a quantidade de instância, o Auto Scaling executa automaticamente a criação ou remoção das instâncias com base nesses parâmetros.

## Políticas de Escalonamento Automático
### 1. Scheduled Scalling
- Ocorre com base em horários e datas predefinidos.

- Ideal para situações onde você sabe com antecedência quando haverá picos ou quedas de demanda.

### 2. Dynamic Scaling

#### 2.1 Target Tracking
- Define um alvo para o uso de recursos do ASG
- Simples de configurar
- Exemplo: "Uso médio da CPU deve ficar abaixo de 50%"

#### 2.2 Simple Scaling (Integrado ao CloudWatch)
- Define uma ação específica para ser executada quando um alarme do CloudWatch é acionado.
- Exemplo: "Se CPU > 70% por 5 minutos, adicione 1 EC2"

#### 2.3 Step Scaling (Integrado ao CloudWatch)
- Permite definir múltiplos níveis (steps) de ação com base na gravidade do alarme.
- Exemplo:
    - Se CPU > 70% por 5 minutos, adicione 1 EC2
    - Se CPU > 85% por 5 minutos, adicione 3 EC2s
- É considerada a versão mais avançada e moderna do Simple Scaling.


### 3. Predictive Scaling
- Neste método, o ASG analisa dados históricos de carga para escalonar automaticamente baseado em horários e datas.
- Útil para aplicações com padrões de uso previsíveis, como picos diários ou sazonais.

## Integração com Alarmes do CloudWatch
- É possível escalonar um ASG baseado nos alarmes do CloudWatch.

<image src="./images/ASGeCloudWatch.png" alt="ASG e CloudWatch" width="600"/>

- O Alarme é baseado em uma métrica, por exemplo: "Consumo médio da CPU do ASG está muito alto", daí aumentar número de instâncias.

- Dá pra integrar com outros serviços da AWS, tipo o SQS, utilizando a métrica "número máximo de mensagens na fila", por exemplo.

- Baseado no alarme, é possível aumentar (scale-out) ou diminuir(scale-in) o número de instâncias.


## Tipos de Health Checks
Os Auto-Scalling groups podem checar a saúde das instâncias de dois tipos:

- **EC2**: O check via EC2 monitora a saúde do servidor apenas a nível de instância, isto é, só vai verificar se o estado é **"`running`"**, deixando detalhes adicionais como estado da aplicação ou serviços internos de lado.

- **ELB**: ==O check via **ELB** permite monitorar o estado da aplicação hospedada na instância==, isso é feito através do envio de uma requisição para uma rota específica, que é encaminhada para as instâncias do target group em um intervalo de tempo definido por você. Isso permite um monitoramento mais detalhado e interessante. 

**Qual se deve usar?**
 - Depende, se quiser verificar a disponibilidade real da aplicação ou serviços na instância, use o **Health Check ELB**, caso uma verificação simples bastar, use **Health Check EC2**.

## Scaling Cooldown
- O Cooldown é um período de espera após uma ação de escalonamento (scale-out ou scale-in) ser executada.
- Durante esse tempo, o ASG não executa novas ações de escalonamento, permitindo que as mudanças tenham efeito antes de qualquer nova ação ser tomada.
- O período padrão é de 300 segundos (5 minutos).

## Lifecycle Hooks
- Permite pausar o processo de escalonamento em pontos específicos do ciclo de vida da instância (inicialização ou término).

- Durante essa pausa, você pode executar tarefas personalizadas, como configuração adicional ou limpeza de recursos.

- Um caso de uso como é utilizar um lifecycle hook de término para que colete os logs da instância antes dela ser terminada.

- O CodeDeploy faz uso intenso de lifecycle hooks para gerenciar o processo de implantação em instâncias dentro de um ASG, para mais informações ler [notas do CodeDeploy](../automacao-e-aplicacoes/ci-cd/CodeDeploy.md).

- A AWS controla a execução dos lifecycle hooks através de tokens, que são usados para identificar e gerenciar o estado das instâncias durante o processo de escalonamento.
    - Caso você encontre erros que mencionem tokens, é bem provável que o tempo de espera do lifecycle hook tenha expirado (`Lifecycle Action with token<token-Id> was abandoned: Heartbeat Timeout`).

## Termination Policies

- Define a ordem em que as instâncias serão terminadas quando o ASG precisar reduzir sua capacidade.

- O algoritmo padrão tenta manter a distribuição equilibrada:
    - Verificar qual AZ possui a maior quantidade de instâncias e terminar instâncias nessa AZ primeiro.

    - Verificar qual instância possui o launch template mais antigo (ou launch configuration).

    - Caso mais de uma instância atenda aos critérios acima, a instância que estiver em estado de **`InService`** por mais tempo será terminada (Next Billing Hour).

    - Se ainda houver empate, uma instância será escolhida aleatoriamente.

- Abaixo, uma versão visual do processo de decisão:

<image src="./images/default-termination-policy-diagram.png" width="600"/>

- Você pode também modificar a termination policy padrão, escolhendo entre as opções disponíveis:
    - **OldestInstance**: Termina a instância mais antiga no ASG.
    - **NewestInstance**: Termina a instância mais nova no ASG.
    - **OldestLaunchConfiguration**: Termina instâncias que usam o launch configuration mais antigo.
    - **ClosestToNextInstanceHour**: Termina a instância que está mais próxima do próximo ciclo de cobrança (billing hour).
    - **Default**: Usa o algoritmo padrão descrito acima.
    - Ou então definir uma função lambda personalizada para determinar a ordem de término das instâncias ([Documentação](https://docs.aws.amazon.com/autoscaling/ec2/userguide/lambda-custom-termination-policy.html)).

## Detalhes Adicionai
- **Para corrigir algum erros em instâncias de um ASG, basta colocá-la em modo stand-by temporáriamente**.
    - **Observação**: não confunda o modo stand-by com o `detach`, o detach remove a instância do ASG permanentemente, enquanto o stand-by é temporário e utilizado para depuração.

- Quando ocorre um balanceamento, o Auto Scalling cria novas instâncias antes de terminar as antigas, para que a aplicação não tenha sua performance ou disponibilidade comprometida.

- **`DisableApiTermination` vs. Instance Protection**: DisableApiTermination impede ações de usuários, mas não ações automáticas do ASG. O Instance Protection faz o contário.