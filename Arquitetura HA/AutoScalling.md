# Auto Scaling
Esse é o <span style="background-color: #e0a800; color: black;font-weight:bold">serviço que ajusta automaticamente a capacidade dos seus recursos de computação com base nas demandas da aplicação</span>. Ele garante que você tenha o número correto de instância disponíveis para lidar com o tráfego, aumentando ou diminuindo o número de instâncias em resposta à carga de trabalho.

## Compontentes do AS

- **Groups (ASG)**
    - Componentes lógicos. Grupos de webservers, aplicações ou banco de dados.

- **Configuration Templates**
    - <span style="background-color: #e0a800; color: black;font-weight:bold">Definem as configurações de inicialização usadas pelo ASG para lançar instâncias EC2</span>. Esses templates permitem especificar a AMI, tipo de instância, pares de chaves (key pairs), grupos de segurança, e armazenamento.

- **Scaling Options**
    - Fornece diferentes estratégias para ajustar a capacidade dos ASGs. Isso pode ser feito com base em condições dinâmicas (Dynamic Scaling) ou através de agendamento.

## Tipos de Escalonamento
### Manutenção de Nível Fixo:
- Mantém um número específico de instâncias rodando continuamente.

- Realiza verificações periódicas de saúde (**Health Checks**) nas instâncias.

- Se uma instância for detectada como **Unhealthy**, ela será substituída automaticamente por uma nova.

### Escalonamento Manual:

- Permite ajustar manualmente o número mínimo, máximo ou desejado de instâncias no ASG

- <span style="background-color: #e0a800; color: black;font-weight:bold">Embora o escalonamento seja feito manualmente, o Auto Scaling gerencia a criação ou remoção das instâncias automaticamente com base nos parâmetros fornecidos.</span>

### Escalonamento Baseado em Agendamento:

- Ocorre com base em horários e datas predefinidos.

- <span style="background-color: #e0a800; color: black;font-weight:bold">Ideal para situações onde você sabe com antecedência quando haverá picos ou quedas de demanda, como em horários de pico previsíveis.</span>

###  Escalonamento Baseado em Demanda (Dynamic Scaling):

- O método mais avançado de escalonamento, usando políticas baseadas em métricas, como uso de CPU ou tráfego de rede.

- Permite que o Auto Scaling ajuste automaticamente a capacidade 
conforme mudanças na demanda da aplicação.

- É a abordagem de escalonamento mais comumente usada na AWS.

## ANOTAÇÕES
- <span style="color:red; font-weight: bold"> NÃO CONFUNDA AUTO-SCALLING GROUPS COM PLACEMENT GROUPS </span> 