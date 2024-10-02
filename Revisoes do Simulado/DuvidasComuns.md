# Dúvidas Comuns
Aqui estão explicações quanto a algumas dúvidas que eu possuo nos serviços, especialmente em serviços parecidos.

___
## Dedicated Instance x Host
Ambos são utilizados para ter controle específico do hardware somente para a sua conta, porém possuem algumas diferenças.

- **Dedicated hosts** nunca sofrem realocação, ideal para máquinas que usam softwares com modelo BYOL (Bring Your Own License).

- Já os **Dedicated Instance** sofrem realocação DENTRO DA SUA CONTA. 

___
## Site-to-Site VPN x Client VPN
- **Site-to-Site** é utilizada para conectar uma rede local à sua VPC (Ou Transit Gateway).

- **Client VPN** conecta usuários a AWS ou recursos dela através de um cliente de software CPN.

___
## PrivateLink x Direct Connect
- **AWS PrivateLink**: Usado para acessar **serviços dentro da AWS** (ou em outras VPCs) de forma **privada e segura**. É feito para manter o tráfego dentro do ambiente da AWS e **NÃO é destinado a conexões on-premises**.

- **AWS Direct Connect**: Fornece uma **conexão física dedicada entre seu data center/empresa e a AWS**. Ideal para transferências de dados em alta velocidade e segurança entre o ambiente on-premises e a nuvem AWS.

___
## Virtual Private Gateway x Transit Gateway
- O VPG é utilizado para realizar conexões de redes um-para-um. Útil para configurar uma VPN. Ele pode ser usado tanto com uma VPN ou Direct Connect.

- Já o TGW é utilizado como um ponto central de conexão entre múltiplas redes, permitindo a comunicação entre todas as redes associadas ao TGW, bem útil, principalmente considerando que você não precisa lidar com topologias ou criação de conexões individuais.

![Diagrama](./images/VPG-x-TGW.png)