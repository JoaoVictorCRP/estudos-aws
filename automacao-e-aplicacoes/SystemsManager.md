# Systems Manager
O Systems Manager é um serviço muito útil para o gerenciamento de sua infraestrutura na nuvem (EC2) ou on premise.

- Permite receber insights operacionais sobre o estado da infraestrutura.
- Facilita a detecção de problemas.
- ==Permite automação de patches, cumprindo com requisitos de conformidade.==
- Funciona tanto com Linux quanto Windows
- Integra com métricas e dashboards do Cloudwatch.
- Integra com o AWS Config
- **Serviço gratuito** (Você só paga pelos recursos em que você está administrando)

## SSM Documents
- Os SSM Documents são arquivos em JSON ou YAML que definem as ações a serem executadas pelo Systems Manager.

- São o "manual de instruções" para o SSM, descrevendo os comandos e scripts que devem ser executados nas instâncias gerenciadas.

- SSM Documents possuem dois tipos principais:
  - **Command Documents**: Usados para executar comandos simples ou scripts nas instâncias.
  - **Automation Documents**: Usados para automatizar tarefas complexas, como atualizações de software, backups e outras operações de manutenção.
  - **Policy Documents**: Usados para definir políticas de conformidade e segurança para as instâncias gerenciadas, utilizados pelo State Manager.

## State Manager
- O State Manager é um recurso do Systems Manager que permite definir e manter o estado desejado das instâncias gerenciadas.

- Com ele, podemos definir configurações a nível de instância, como instalação de software, configurações de rede, políticas de segurança, entre outros.

- O state manager aplica um document (SSM Document) nas instâncias gerenciadas de forma automática e contínua, garantindo que elas estejam sempre em conformidade com o estado desejado, sem drift.

## Systems Manager Inventory
- Feature bem legal do SSM que permite **coletar metadados de servidores** (==EC2 ou on-premises==).

- Os metadados coletados podem ser **softwares instalados**, versão do SO, pastas e arquivos, configurações de rede e muito mais.

## Patch Baselines

- Permite definir regras para aplicação automática de patches em instâncias gerenciadas pelo SSM.

- Você pode criar **Patch Groups** para organizar suas instâncias e aplicar políticas de patch específicas para cada grupo.

- Suporta tanto patches de segurança quanto atualizações de software (Os patches podem ser aplicados em períodos de janela de manutenção definidos por você, evitando indisponibilidades indesejadas).

- **É possível definir a aplicação de patches customizados** (usando um repositório apt ou yum próprio, por exemplo).

## SSM on-premises

- O Systems Manager também pode gerenciar servidores on-premises (fora da AWS), isto é feito através da seção **Hybrid Activations** no console do SSM.

- Para cada servidor on-premises, você deve criar um **Activation** no SSM, que gera um código e um ID.

- Ao instalar o agente do SSM no servidor on-premises, você deve fornecer esse código e ID para registrar o servidor no Systems Manager.

- Após o registro, o servidor on-premises pode ser gerenciado da mesma forma que uma instância EC2, incluindo a aplicação de patches, coleta de inventário e execução de comandos remotos.
  - No console do SSM, as instância on-premises aparecem com o prefixo "mi-" (Managed Instance), diferentemente das instâncias EC2 que aparecem com o prefixo "i-".

## Session Manager

- O Session Manager é uma feature que permite a conexão com instâncias EC2 ou servidores on-premises de forma segura, sem a necessidade de abrir portas de SSH ou RDP.

  - As conexões são feitas através do console do SSM ou da AWS CLI, utilizando o agente do SSM instalado na instância.

- Para estabelecer uma sessão, a instância deve ter a role do IAM correta anexada, com permissões para o Systems Manager.

- **Se quiser realizar uma conexão privada via SSM**, sem passar pela internet, **você deve configurar um VPC endpoint para o Systems Manager**.