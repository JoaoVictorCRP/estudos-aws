# Systems Manager
O Systems Manager é um serviço muito útil para o gerenciamento de sua infraestrutura na nuvem (EC2) ou on premise.

- Permite receber insights operacionais sobre o estado da infraestrutura.
- Facilita a detecção de problemas.
- ==Permite automação de patches, cumprindo com requisitos de conformidade.==
- Funciona tanto com Linux quanto Windows
- Integra com métricas e dashboards do Cloudwatch.
- Integra com o AWS Config
- **Serviço gratuito** (Você só paga pelos recursos em que você está administrando)

## Systems Manager Inventory
- Feature bem legal do SSM que permite **coletar metadados de servidores** (==EC2 ou on-premises==).

- Os metadados coletados podem ser **softwares instalados**, versão do SO, pastas e arquivos, configurações de rede e muito mais.

## Patch Baselines

- Permite definir regras para aplicação automática de patches em instâncias gerenciadas pelo SSM.

- Você pode criar **Patch Groups** para organizar suas instâncias e aplicar políticas de patch específicas para cada grupo.

- Suporta tanto patches de segurança quanto atualizações de software (Os patches podem ser aplicados em períodos de janela de manutenção definidos por você, evitando indisponibilidades indesejadas).

- **É possível definir a aplicação de patches customizados** (usando um repositório apt ou yum próprio, por exemplo).