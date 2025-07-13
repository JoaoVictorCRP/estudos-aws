O Control Tower é uma ==**ferramenta de governança que nos ajuda a implementar políticas de segurança e conformidade em toda a sua organização AWS**==. Com a ajuda deste serviço, você pode

- **Implementar políticas de segurança e conformidade** que se aplicam a todos os recursos da organização.

- ==**Realizar auditorias no uso do recursos AWS**== para garantir que a utilização segue as boas práticas de segurança. (Integrado com Cloudtrail e Config)

- **==Gerenciar diferentes ambientes (contas)== para diferentes equipes ou projetos** de maneira centralizada, mantendo a segurança e conformidade.

Para começar a utilizar o **Control Tower**, nós precisamos realizar a criação de uma **Landing Zone**, que é um ambiente centralizado que abriga múltiplas contas sob uma mesma organização.

### Guardrails
- Os Guardrails são políticas que você pode estabelecer em sua organizazção através do Control Tower.

- Por debaixo dos panos, os Guardrails são, na verdade, config rules do **AWS Config** ou **SCPs** aplicadas à nível organizacional.