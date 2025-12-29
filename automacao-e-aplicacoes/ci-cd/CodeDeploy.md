# CodeDeploy

- O CodeDeploy é um serviço de implantação automatizada da AWS que facilita a implantação de aplicações em instâncias EC2, servidores on-premises e funções Lambda.
  - Deploys na própria AWS não geram custos adicionais, apenas o uso de recursos subjacentes (EC2, S3, etc).

- Ele permite que você automatize o processo de implantação, reduzindo o tempo de inatividade e minimizando erros humanos durante as atualizações de software.

## Conceitos Principais

### Aplicações e Deployment Groups
- Uma aplicação no CodeDeploy é uma coleção lógica de recursos que você deseja implantar.

- Um Deployment Group é uma coleção de instâncias ou servidores onde a aplicação será implantada

### Agent do CodeDeploy
- O agente do CodeDeploy é um software que deve ser instalado nas instâncias EC2 ou servidores on-premises para permitir a comunicação com o serviço CodeDeploy.
- Ele gerencia o processo de implantação, baixando os artefatos e executando os scripts conforme definido no arquivo AppSpec.

### Ciclo de Vida da Implantação
- O CodeDeploy suporta diferentes ciclos de vida de implantação, incluindo Blue/Green e In-Place.

- Blue/Green envolve a criação de um novo ambiente para a nova versão da aplicação, enquanto In-Place atualiza a aplicação diretamente nas instâncias existentes.

### Rollback Automático
- O CodeDeploy pode ser configurado para reverter automaticamente para a versão anterior da aplicação em caso de falhas durante o processo de implantação, garantindo maior confiabilidade.

- **Você pode configurar o disparo de um rollback com base em alarmes do CloudWatch** ou falhas de implantação.

### AppSpec File
- O arquivo AppSpec é um arquivo YAML ou JSON que define como o CodeDeploy deve implantar a aplicação.
- Ele especifica os arquivos a serem copiados, os scripts a serem executados em diferentes fases do ciclo de vida da implantação, e outras configurações necessárias.

#### Hooks do Ciclo de Vida
- Os hooks do ciclo de vida permitem que você execute scripts em pontos específicos durante o processo de implantação, como antes da instalação, após a instalação, antes da reinicialização, etc.

### Estratégias de Implantação
- O CodeDeploy oferece várias estratégias de implantação, incluindo:
  - **All-at-Once**: Implanta a nova versão em todas as instâncias simultaneamente.
  - **Rolling Update**: Implanta a nova versão em lotes, reduzindo o impacto em caso de falhas.
  - **Canary**: Implanta a nova versão em uma pequena porcentagem de instâncias antes de expandir para o restante.
  - **Blue/Green**: Cria um novo ambiente para a nova versão, permitindo uma transição suave.