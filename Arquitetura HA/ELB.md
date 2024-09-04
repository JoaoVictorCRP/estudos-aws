# Elastic Load Balancer (ELB)
## O que é?
O **Elastic Load Balancer** faz exatamente o que seu nome diz, ele equilibra a carga de trabalho entre múltiplos servidores, há 4 tipos de apicação para um LB, vejamos:

## Tipos 
### 1. Application LB (ALB)
- Ideal para tráfego HTTP/HTTPS, roteamento de aplicação (caminho da URL, cabeçalhos, etc.)
- <span style="background-color: #e0a800; color: black;font-weight:bold">Operam na primeira camada da pilha OSI, que é a camada da aplicação.</span>

- São inteligentes, você pode criar um roteamento avançado de requests, de forma que mande requests específicos para determinados web servers.

- ELBs São "application-aware", isso significa que eles são capazes de analisar atribuitos da aplicação como caminho da URL, cabeçalhos HTTP e parâmetros de consulta para tomar decisões inteligentes para o roteamento do tráfego.

    #### Como o ALB toma decisões inteligentes?
    -  **Roteamento baseado em conteúdo**: O ALB permite que você direcione o tráfego para diferentes grupos de destino com base em regras específicas. Por exemplo, você pode rotear solicitações que contenham `/login` para um servidor específico e `/products` para outro.

    - **Suporte a microserviços e contêineres**: <span style="background-color: #e0a800; color: black;font-weight:bold">Ele é ideal para arquiteturas baseadas em microserviços</span>, pois permite que diferentes partes de uma aplicação sejam gerenciadas e dimensionadas separadamente.

    - **Autenticação integrada**: <span style="background-color: #e0a800; color: black;font-weight:bold">O ALB pode integrar autenticação de usuários diretamente na camada de balanceamento</span>, utilizando o Amazon Cognito para gerenciar identidades de usuários a sem necessidade de modificar a aplicação.


### 2. Network LB (NLB)
<span style="background-color: #e0a800; color: black;font-weight:bold">São otimizados para o balanceamento de carga do tráfego TCP, onde a extrema performance é desejada, operando na camada 4 (transporte de rede), NLBs são capazes de gerenciar milhões de requests por segundo</span>, tudo isso mantendo uma latência ultra baixa.

### 3. Gateway LB (GWLB)
- Opera nas camadas 3 (rede) e 4 (transporte)
- <span style="background-color: #e0a800; color: black;font-weight:bold">Facilita  a implantação, escalabilidade e gerenciamento de dispositivos virtuais de rede, como firewalls e sistemas de inspeção de pacotes</span>.
- Ideal na implementação de dispositivos de segurança como firewalls, sistemas de prevenção de intrusão (IPS), ou proxies.

### 4. Classic LB (CLB)
São ELBs legado, com eles você pode fazer o balanceamento de carga de HTTP/HTTPS de aplicações e também utilizar atriutos específicos da camada de aplicação, como <span style="background-color: green; color: black;font-weight:bold">X-Forwarded e sticky sessions</span>. Também é possível o usar estritamente a camada 4 para o balaceamento de aplicações que dependem puramente do protocolo TCP.

#### X-Forwarded-For
Este é um método de cabeçalho HTTP que <span style="background-color: #e0a800; color: black;font-weight:bold">identifica o real IP de origem do usuário que fez uma requisição para o ELB</span>, uma vez que a requisição chega na instância como se fosse originada únicamente do ELB.
![Diagrama X-Forwarded-For](xForwarded.png)


## Erros Comuns em LBs
- **CLB**: Se a sua aplicação parar de responder, um ELB em modelo CLB responderá um <span style="background-color: #e0a800; color: black;font-weight:bold">erro 504</span>. Isso <span style="background-color: #e0a800; color: black;font-weight:bold">significa que a aplicação está enfrentando problema, não o ELB</span>. A causa pode tanto estar na camada do servidor web quanto na camada da aplicação