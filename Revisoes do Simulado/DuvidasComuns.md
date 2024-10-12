# Dúvidas Comuns
Aqui estão explicações quanto a algumas dúvidas que eu possuo nos serviços, especialmente em serviços parecidos.

___
## Dedicated Instance x Host
Ambos são utilizados para ter controle específico do hardware somente para a sua conta, porém possuem algumas diferenças.

- **Dedicated hosts** nunca sofrem realocação, ideal para máquinas que usam softwares com modelo BYOL (Bring Your Own License).

- Já os **Dedicated Instance** sofrem realocação DENTRO DA SUA CONTA. 

___
## Site-to-Site VPN x Client VPN
- **Site-to-Site** é utilizada para conectar uma rede local inteira à sua VPC (Ou Transit Gateway).

- **Client VPN** conecta um usuário a AWS ou recursos dela através de um cliente de software VPN.

___
## PrivateLink x Direct Connect
- **AWS PrivateLink**: Usado para acessar **serviços dentro da AWS** (ou em outras VPCs) de forma **privada e segura**. É feito para manter o tráfego dentro do ambiente da AWS e **NÃO é destinado a conexões on-premises**.

- **AWS Direct Connect**: Fornece uma **conexão física dedicada entre seu data center/empresa e a AWS**. Ideal para transferências de dados em alta velocidade e segurança entre o ambiente on-premises e a nuvem AWS.

___
## Virtual Private Gateway x Transit Gateway
- O VPG é utilizado para realizar conexões de redes um-para-um. Útil para configurar uma VPN. Ele pode ser usado tanto com uma VPN ou Direct Connect.

- Já o TGW é utilizado como um ponto central de conexão entre múltiplas redes, permitindo a comunicação entre todas as redes associadas ao TGW, bem útil, principalmente considerando que você não precisa lidar com topologias ou criação de conexões individuais.

![Diagrama](VPG-x-TGW.png)

___
## CloudFront x Global Accelerator
Os dois serviços estão relacionados a melhoria da performance e disponibilidade em escala global, no entanto, possuem propósitos e funcionamentos diferentes:

- O **CloudFront** é um serviço de CDN que distribui conteúdo estático e dinâmico para <ins>usuários finais</ins> através das **Edge Locations** que apontam para um destino específicado (instância EC2 ou bucket S3).
	-  Tem como endpoint um único DNS.

- Já o **Global Accelerator** realiza o roteamento <ins>para componentes da aplicação</ins>, isto é, APIs REST, por exemplo. Ao contrário do CloudFront, o GA não faz cache de conteúdo, justamente por conta disso ele não é utilizado no roteamento de requisições de usuários finais.
	- Tem dois endpoints, que são <ins>DOIS IPs fixos</ins>.

___

## WAF x Shield x Firewall Manager
Os três serviços são utilizados para segurança. 
Eles podem inclusive ser utilizados em conjunto, ou não.

**WAF**
- Define as regras de acesso à sua aplicação web, operando na camada 7.
- Permite bloqueio baseado em IP, região ou quantidade de chamados para a API.
- Protege contra ataques como **SQL injection** e **cross-site scripting (XSS)**.

- Pode ser utilizado com **Amazon CloudFront**, **ALB**, e **API Gateway** para proteger aplicações.

-  <span style="background-color:red; font-weight: bold; color:#fff">Shield Advanced</span> é uma **camada premium** que fornece proteção mais robusta contra ataques DDoS, com monitoramento 24/7, mitigação em tempo real, e suporte especializado de resposta a incidentes. Legal, mas custa <span style="background-color:red; color:#fff">$3000 por mês</span>.

**Shield**
- Utilizado para proteção contra ataques DDOS.
- **Shield Standard** é aplicado **automaticamente e sem custo** adicional a todos os clientes AWS, oferecendo proteção básica contra DDoS.

**Firewall Manager**
- Painel unificado do AWS Organizations para gerenciamento das regras de acesso aos recursos de cada uma das contas.
- Pode controlar WAF, Shield, NACLs, Security Groups e policies.

___
## Storage Gateway x DataSync
Ambos serviços são focados em migração de dados on-premise para a nuvem, porém possuem estratégias diferentes e aplicabilidades distintas.

- O **Storage Gateway** funciona como se fosse um copy-on-write do seu on-premise para a nuvem AWS, permite que você possa continuar utilizando seu sistema de arquivos on-premise sem sequer notar que tudo que você está criando localmente está indo para a nuvem também, show de bola!

- Já o **DataSync** possui uma visão mais bruta sobre a migração, ele se aplica em contextos onde você quer largar mão de armazenamento on-premise e quer colocar tudo na nuvem.

Em suma:
- Imagine o Storage gateway como um baú do nether do minecraft, tudo o que você colocar no baú, será replicado no seu par. 
- Pense no DataSync como um grande caminhão de mudanças, que vai levar todos os seus móveis para uma casa nova.