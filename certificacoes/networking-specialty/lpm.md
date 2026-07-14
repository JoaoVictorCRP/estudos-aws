# LPM - Longest Prefix Match

- Imagine que você tem os seguintes CIDRs em sua VPC: `192.168.20.0/24` (Primário) e `192.168.100.0/24` (Secundário), além de uma conexão VPN com a sua rede on-premises que possui o CIDR `192.168.128.0/17`.

- A sua route table, por sua vez, possui as seguintes rotas:
```
192.168.20.0/24 -> Rota local
192.168.100.0/24 -> Rota local
192.168.0.0/16 -> Rota para o On-Premises (VPN)
```

- Olhando isso, vocÊ pode pensar que qualquer tráfego interno vai ser direcionado para o On-Premises, já que o CIDR é mais abrangente, mas na verdade, o tráfego interno vai ser direcionado para a rota local, pois o CIDR é mais específico.

- Essa é uma regra chamada **LPM (Longest Prefix Match)**, que significa que a rota mais específica (com o prefixo mais longo) será a escolhida para rotear o tráfego.

- Este é um conceito muito importante para entender o roteamento em redes, especialmente em ambientes de nuvem como a AWS, onde múltiplas rotas podem existir e a escolha da rota correta é crucial para o funcionamento adequado da rede.