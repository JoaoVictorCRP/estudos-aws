# Dúvidas Comuns
Aqui estão explicações quanto a algumas dúvidas que eu possuo nos serviços, especialmente em serviços parecidos.

___
## Dedicated Instance x Host
Ambos são utilizados para ter controle específico do hardware somente para a sua conta, porém possuem algumas diferenças.

- **Dedicated hosts** nunca sofrem realocação, ideal para máquinas que usam softwares com modelo BYOL (Bring Your Own License).

- Já os **Dedicated Instance** sofrem realocação DENTRO DA SUA CONTA. 


- ==**OBSERVAÇÃO: Dedicated Host é mais caro que Dedicated Instance.**==
___
## Site-to-Site VPN x Client VPN
- **Site-to-Site** é utilizada para conectar uma rede local inteira à sua VPC (Ou Transit Gateway).

- **Client VPN** conecta UM usuário a AWS ou recursos dela através de um cliente de software VPN.

___
## PrivateLink x Direct Connect
- **AWS PrivateLink**: Usado para acessar **serviços dentro da AWS** (ou em outras VPCs) de forma **privada e segura**. É feito para manter o tráfego dentro do ambiente da AWS e ==**NÃO é destinado a conexões on-premises**.==

- **AWS Direct Connect**: Fornece uma **conexão física dedicada entre seu data center/empresa e a AWS**. Ideal para transferências de dados em alta velocidade e segurança entre o ambiente on-premises e a nuvem AWS.

___
## Virtual Private Gateway x Transit Gateway
- O VPG é utilizado para realizar conexões de redes um-para-um. Útil para configurar uma VPN. Ele pode ser usado tanto com uma VPN ou Direct Connect.

- Já o TGW é utilizado como um ponto central de conexão entre múltiplas redes, permitindo a comunicação entre todas as redes associadas ao TGW, bem útil, principalmente considerando que você não precisa lidar com topologias ou criação de conexões individuais.

![Diagrama](VPG-x-TGW.png)

___
## CloudFront x Global Accelerator
Os dois serviços estão relacionados a melhoria da performance e disponibilidade em escala global, no entanto, possuem propósitos e funcionamentos diferentes:

- O **CloudFront** é um serviço de CDN que distribui conteúdo estático e dinâmico para <ins>usuários finais</ins> através das **Edge Locations** que apontam para um destino específicado (Servidor HTTP ou bucket S3). Ele suporta cache de conteúdo estático e também otimiza a entrega de conteúdo dinâmico sem cache.
	-  Tem como endpoint um único DNS.

- O **Global Accelerator**, por sua vez, também utiliza a rede global da Amazon, no entanto ele não faz cache de conteúdo. Seu principal ponto de destaque são os dois IPs estáticos anycast que ele oferece, esses dois IPs podem ser utilizados em qualquer região da AWS, possuem baixa latência e e alta disponibilidade. Os IP do global accelerator podem ser atrelados a vários serviços, como um ELB, uma EC2, ou um Bucket S3. 
	- OBS: Um IP anycast é um IP que referencia múltiplas máquinas de uma rede, nesse caso, as máquinas da rede de distribuição da Amazon, quando o cliente acessar tal IP ele será direcionado para a edge location mais próxima dele. Legal!

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

___ 
## CNAME vs Alias (Route 53)
| ==**CNAME**==                                 | ==**Alias**==                                                                     |
| --------------------------------------------- | --------------------------------------------------------------------------------- |
| **Redireciona** um nome de domínio para outro | **Atalho** para serviços AWS (S3, CloudFront, ELB)                                |
| Não pode ser usado no **domínio raiz**        | Pode ser usado tanto no **domínio raiz** quanto em **subdomínios**                |
| Pode ser usado para **qualquer domínio**      | Específico para **recursos AWS** e domínios pertencentes a uma mesma hosted zone. |
| Pode gerar **custo** adicional                | **Sem custo adicional** para consultas (em serviços AWS)                          |

___
### Signed URLs vs Signed Cookies

- ==**Signed URLs** são usadas para **UM ÚNICO ARQUIVO**== de um bucket s3. Através dela, você pode criar uma URL para um único conteúdo específico por um prazo determinado de tempo. 
	- **Caso de uso:** Exibir um único arquivo do bucket para um cliente.

- ==**Signed Cookies** são usados para garantir acesso a **múltiplos arquivos**== dentro de um bucket ou domínio, também é possível definir um prazo de validade para eles.
	- **Caso de uso**: Restringir acesso ao conteúdo do site apenas para clientes VIPs.

___
### S3 Select vs Amazon Athena

Ambos serviços permitem que você realize uma query SQL dentro de um bucket S3, porém há uma diferença:
- ==O **S3 Select** faz queries== apenas ==dentro de um único objeto==.

- ==O **Amazon Athena** faz buscas dentro de um bucket inteiro==, incluindo os prefixos e os prefixos dentro dos prefixos, eita!