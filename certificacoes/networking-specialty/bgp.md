# BGP

## O que é?
- O Border Gateway Protocol (BGP) é o protocolo de roteamento usado para trocar informações de roteamento entre sistemas autônomos (AS) na Internet. Sendo um protocolo de roteamento externo, ele é fundamental para a operação da Internet, permitindo que diferentes redes se comuniquem e troquem informações de roteamento sem a necessidade de mapear rotas manualmente.

> **Observação**: Um sistema autônomo (AS) é uma coleção de redes IP e roteadores sob o controle de uma única entidade administrativa que apresenta uma política de roteamento comum para a Internet, podemos considerar um AS como um provedor de serviços de Internet (ISP), mas isso não é uma regra, pois um AS pode ser uma grande empresa, universidade ou qualquer organização que gerencie sua própria rede.

## Na AWS
- O BGP é um tópico bem comum na Networking Specialty, pois é muito usado no Site-to-Site VPN e no AWS Direct Connect. 

- Ele é usado para anunciar rotas entre a rede local do cliente e a rede da AWS, permitindo que o tráfego seja roteado de forma eficiente entre os dois ambientes.

## Modo de operação

- Existem dois tipos de BGP: o eBGP (External BGP) e o iBGP (Internal BGP). 

  - O eBGP é usado para trocar informações de roteamento entre diferentes sistemas autônomos.
  
  - Já o iBGP é usado para trocar informações de roteamento dentro do mesmo sistema autônomo.

- A decisão de roteamento é influenciada por alguns parâmetros, como:

  - **AS Path**: O caminho de sistemas autônomos que uma rota percorreu. Rotas com caminhos mais curtos são preferidas. Funciona entre ASs.
  
  - **Local Preference**: Um valor configurado para indicar a preferência de uma rota dentro de um AS. Rotas com maior local preference são preferidas. Funciona dentro de um AS.
  
  - **MED (Multi-Exit Discriminator)**: Um valor usado para influenciar a escolha de rotas entre diferentes AS. Rotas com menor MED são preferidas. Funciona entre ASs.

  - **Weight**: ==Peso atribuído a uma rota, o roteamento escolhe a rota com maior peso==. O weight é específico para o roteador local e não é propagado para outros roteadores, outro detalhe importante é que **esse parâmetro é específico de roteadores da Cisco e só funciona dentro do AS**.