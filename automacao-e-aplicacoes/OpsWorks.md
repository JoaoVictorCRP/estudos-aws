# AWS OpsWorks

- O AWS OpsWorks é um serviço de gerenciamento de configuração que facilita a automação do gerenciamento de servidores e aplicativos na nuvem AWS.
  - Ele atua como uma plataforma de gerenciamento de configuração baseada em Chef e Puppet, permitindo que você defina a infraestrutura como código.
  - Chef e Puppet são duas ferramentas open-source de gerenciamento de configuração que ajudam a automatizar a implantação, configuração e gerenciamento de servidores e aplicações.

- Basicamente, é uma alternativa ao AWS Systems Manager, com foco maior em automação de configuração usando Chef e Puppet.

- A principal premissa por trás de usar o Chef/Puppet é o fato de que são ferramentas Open Source e agnósticas de nuvem (ou seja, podem ser usadas em qualquer ambiente, não apenas na AWS).

## Automações com Chef/Puppet

- Permite criar "stacks" e "layers" para organizar e gerenciar seus recursos de forma estruturada.
  - Stacks representam a aplicação completa, enquanto layers representam componentes individuais da aplicação (como servidores web, bancos de dados, etc.).

- Funciona tanto em Linux quanto em Windows.

- Permite definir receitas (**recipes**) do Chef ou **manifests** do Puppet para configurar automaticamente os servidores conforme necessário.
  - Estes arquivos permitem automatizar tarefas como instalação de software, configuração de serviços, gerenciamento de usuários e muito mais.

