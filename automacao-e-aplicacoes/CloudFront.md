# CloudFront

- O CloudFront é a rede CDN da AWS, que utiliza uma rede global de **Edge Locations** para fazer o **cache** do conteúdo e entregá-lo aos usuários de forma mais rápida e eficiente.

- Para configurar o CloudFront, você define um ponto de origem, que pode ser um S3, instância EC2, Load Balancer, ou até mesmo um servidor externo (on-premises).

- Quando o usuário mandar uma requisição para a sua URL, você configura para bater na edge location que fará um **CACHE HIT ou CACHE MISS**, nesse último caso, ele irá fazer um Origin Fetch (buscar o conteúdo na origem).

- Este serviço é ideal para ser utilizado quando você tem usuários localizados em um lugar distante da região onde sua aplicação está hospedada, permitindo que você faça um cache da sua aplicação em uma região mais próxima dos usuários finais.

## Segurança Avançada: Key Groups e Signed URLs
- O CloudFront permite que você controle o acesso ao seu conteúdo utilizando **Key Groups** e **Signed URLs**.

- **Key Groups**: São grupos de chaves públicas que você pode associar às suas distribuições do CloudFront. Essas chaves são usadas para verificar a autenticidade das URLs assinadas que serão utilizadas para acessar o conteúdo protegido.

- **Signed URLs**: São URLs que contêm uma assinatura digital, permitindo o acesso a conteúdos restritos por um período de tempo específico. Você pode gerar essas URLs assinadas usando as chaves privadas associadas aos Key Groups.

- Anteriormente, também existia um método chamada **Cloudfront Key Pairs**, mas atualmente o recomendado é utilizar Key Groups e Signed URLs para maior flexibilidade e segurança.
	- Um detalhe era que os Key Pairs só podiam ser gerenciados pelo root e não podia ser automatizado, tornando um processo manual, complexo e propenso a falhas.

## Anotações
- O envio de dados da origem para as Edge Location NÃO POSSUEM CUSTOS ASSOCIADOS. No entanto, as requisições que o CloudFront faz possuem custo.

- Se você precisar aumentar ou diminuir a duração de um cache para os conteúdos:
	- Você pode alterar o TTL (Isso afetará todos os conteúdos)

	- Ou então, você pode adicionar o elemento Cache-Control Header na requisição de determinados elementos que você quer que tenha um TTL diferente dos demais. (Ideal para conteúdo dinâmico)

- **Se você quiser usar o Amazon CloudFront com um certificado SSL/TLS de terceiros**, você **precisa importar esse certificado na região North Virginia (us-east-1)**.