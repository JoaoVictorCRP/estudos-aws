# VPC Lattice
- O VPC Lattice é um serviço da AWS que simplifica a conexão de aplicação para aplicação (service-to-service), sem interligar a rede inteira.

- Com ele, é possível estabelecer uma conexão segura e consistente entre serviços sem o uso de esquemas de rede complexos como VPC Peering ou Transit Gateway.

- Suporta Service Discovery e roteamento dinâmico.
  - **Service Discovery**: Permite que os serviços descubram uns aos outros de forma automática, sem a necessidade de configuração manual de endereços IP ou nomes de host.

- O principal diferencial entre este serviço e os VPC Endpoints é que o VPC Lattice tem o suporte para service discovery, além de evitar a complexidade de criar múltiplos endpoints, já que aqui você usa o Lattice como ponto central de comunicação entre os serviços.

## Componentes

- **Service Network**: É a rede virtual que conecta os serviços. Ele atua como um backbone para o tráfego entre os serviços, garantindo que a comunicação seja segura e eficiente.

- **Service**: Representa uma aplicação ou microserviço que você deseja expor para outros serviços dentro da Service Network. Cada serviço pode ter múltiplas instâncias, e o VPC Lattice gerencia o tráfego entre essas instâncias.

  - Uma vez que o serviço é criado, ele pode ser acessado via service discovery, permitindo que outros serviços acessem ele por meio do DNS dele.

  - Um service tem seu próprio target group, listeners e regras de roteamento, semelhante a um ALB.

- **Resource**: Entidade que representam componentes da aplicação que não são serviços, como bancos de dados, filas, etc.
  
  - Eles podem ser acessados pelos serviços dentro da Service Network.

  - Obs: Resources são da camada 4, enquanto os services são da camada 7.

- **Auth Policies**: Permitem o controle de acesso granular aos serviços e recursos dentro da Service Network.
  - Com elas, você pode definir quem pode acessar quais serviços e recursos.

  - Uma auth policy pode ser anexada a um service individual ou a toda a service network, permitindo flexibilidade na gestão de permissões.

## Associações
- A VPC Lattice pode ser associada a:
  - **Services**
  
  - **Resources**

  - **VPCs**: Permitindo que clientes dentro da VPC acessem os serviços e recursos da Service Network
    - Os clientes desta VPC podem acessar os serviços atráves do endereço de link local (169.254.171.X)
  
  - **VPC Endpoints**: O acesso ocorrerá por meio do IP associado ao endpoint, que deve ser do tipo `service network endpoint` (e não do tipo `interface endpoint`).