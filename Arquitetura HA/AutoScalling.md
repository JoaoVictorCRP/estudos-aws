# Auto Scaling
Este é um serviço da AWS que ajusta automaticamente a capacidade dos seus recursos de computação com base nas demandas da aplicação. Ele garante que você tenha o número correto de instância disponíveis para lidar com o tráfego, aumentando ou diminuindo o número de instâncias em resposta à carga de trabalho.

## Compontentes do AS

- **Groups (ASG)**
    - Componentes lógicos. Grupos de webservers, aplicações ou banco de dados.

- **Configuration Templates**
    - Grupos utilizam uma definição de inicialização como template de configuração para as EC2 que ele tem dentro.
    - Permite a especificação de informações como a ID da imagem (AMI), tipo de instância, key pair, security groups e armazenamento para as instâncias.

- **Scaling Options**
    - Oferece diversas estratégias para dimensionamento dos ASGs.
    - Por exemplo, você pode configurar um grupo para dimensionar baseado na ocorrência de condições específicas (Dynamic Scaling) ou por agendamento.

## Opções de Escalonamento
- **Manter os níveis atuais da instância a todo momento**
    - Mantém um número específico de instâncias rodando a todo momento.

    - Para gerenciar as instâncias, o Auto-Scaling realiza um Health Check periódico nas instâncias dentro de um grupo definido.

    - Quando o Auto Scaling notar uma instância Unhealthy, a instância será terminada e uma nova será lançada.



- **Escalonar manualmente**
    - É a maneira mais básica de escalonar seus recursos, onde você especifica somente a mudança máxima, mínima ou capacidade desejada  para seu ASG.
    - O processo de criar ou terminar instâncias de acordo com a capacidade fica por conta do próprio serviço, basicamente de maneira semi-automática.

- **Escalonamento baseado em agendamento**
    - As ações serão realizadas automaticamente de acordo com um horário ou data definida.
    - Essa opção é bem útil para quando você exatamente quando aumentar ou diminuir a capacidade das suas instâncias.

- **Escalonamento baseado em demanda**
    - Método mais avançado de escalonar recursos, usando políticas de escalonamento.
    - Permite a definição de parâmetros que controlarão o processo.
    - É o tipo de escalonamento mais popular da AWS.