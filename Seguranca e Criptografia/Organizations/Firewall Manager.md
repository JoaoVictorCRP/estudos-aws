- O AWS Firewall Manager é um serviço de gerenciamento de segurança centralizado, que é aplicado as contas e aplicações de uma organização. Através dele é possível controlar **QUASE** todos as regras de inbound/outbound da sua organização.

- Quais recursos dá pra controlar a partir do Firewall Manager?

	- **WAF**: Configure e gerencie regras do WAF.
	
	- **Shield Advanced**: Proteção avançada contra ataques DDOS.
	
	- **Security Groups**: Configuração e auditoria de grupos de segurança.
	
	- **Route 53 Resolver**: Associação de regras de firewall de DNS às suas VPCs.
	
	- **AWS Network Firewall**: (ver a seção "Sobre o Network Firewall")
	
	- **Firewalls de Terceiros do AWS Marketplace**: Montoramento centralizado dos firewalls adquiridos no Marketplace da AWS.
## Sobre o Network Firewall
- Este é um recurso totalmente gerenciado dentro do Firewall Manager. Ele oferece recursos de segurança mais avançados, como:
	- Inspeção do tráfego dos pacotes de rede.

	- Detecção de intrusões (e o bloqueio delas)

	- Filtragem de tráfego por domínio e endereço IP

- ==Embora o AWS Network Firewall ofereça funcionalidades mais avançadas em comparação com as NACLs, ele não substitui diretamente as NACLs.== As NACLs continuam sendo usadas para controle básico de tráfego em nível de sub-rede, enquanto o AWS Network Firewall fornece recursos de segurança adicionais e mais granulares.