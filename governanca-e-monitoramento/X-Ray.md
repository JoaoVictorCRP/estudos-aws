# X-Ray

- O Amazon X-Ray é um serviço utilizado para traçar o fluxo de trabalho das suas aplicações na AWS e como elas se interconectam, tudo de maneira visual.

- Também é possível ==traçar e monitorar requisições== enviadas a recursos integrados que se integram ao XRay, que são:
	- **EC2** (*Necessário instalar o X-Ray Agent*)
	- **ECS** (*Necessário instalar o X-Ray Agent ou rodá-lo em um container*)
	- **Lambda**
	- **Beanstalk**
	- **API Gateway**

- Ele é ==especialmente bom quando precisamos depurar e identificar gargalos em aplicações distribuídas== (microsserviços). Se o exame falar sobre troubleshooting de aplicações distribuída, então a resposta vai estar relacionada ao X-Ray.

