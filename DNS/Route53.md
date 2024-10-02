# Route 53
O Route 53 é o serviço de DNS da AWS, é bem interessante e faz muitas coisas além da resolução de nomes de domínio.


## O Protocolo DNS
Dentro do protocolo DNS temos dois tipos principais para registro do nome de domínio, são eles:

- **Tipo A**: "A" para "Address", ele mapeia um nome de domínio para um endereço IPv4. Quando um usuário digita um nome de domínio, o servidor DNS consulta o registro A para encontrar o endereço IP correspondente.

- **CNAME**: Canonical Name Record, é utilizado para apontar um nome de domínio para um outro nome de domínio, útil em casos de redirecionamento (Um é exemplo é quando buscamos por *Twitter.com* e somos redirecionados para *X.com*)

- **Alias**: Funciona da mesma maneira que o CNAME, no entanto esse carinha suporta "domínios naked", isto é, um domínio com `https://` ou `www.` na frente.

### Registro SOA
O Start of Authority é o primeiro registro a ser logado em um servidor DNS, nele são incluídas informações importantes do domínio, como:
- Servidor de Origem
- Email do administrador do domínio
- Número de série (para identificar uma atualização do arquivo)
- Valor em segundo do *Time-To-Live* do registro


## Os Domínios
- O custo de registro de um domínio muda de acordo com o TLD selecionado, atualmente o TLD ".com" custa $15.
- Pode levar até 72 horas para o registro ocorrer, dependendo da circunstância.

## Routing Policy
As seguintes Routing Policies estão disponíveis no Route53:

- **Simple Routing**: Neste modelo, você poderá ter somente um registro com múltiplos endereços IP. <span style="background-color: #e0a800; color: black;font-weight:bold">No caso de você colocar múltiplos endereços IP, o route 53 escolherá o IP de destino do usuário de maneira aleatória.</span>

- **Weighted Routing**:<span style="background-color: #e0a800; color: black;font-weight:bold">Permite que você divida o tráfico baseando em peso.
    </span> Por exemplo: Colocar 10% do tráfico para a região US-EAST-1 e 90% para SA-EAST-1.

- **Latency-based Routing**:<span style="background-color: #e0a800; color: black;font-weight:bold"> Permite rotear o tráfico baseado no ponto de menor latência para o usuário final (região de menor latência)</span>. Para isso, é necessário ativar a opção de registro de latência na EC2 ou ELB que vai receber o apontamento, lembrando que: **Não é porque a região está mais próxima de você que ela terá uma latência menor**. 
![Slide Latency Based](LatencyBased.png)

- **Failover Routing**: Utilizado quando você deseja montar um esquema de backup. Exemplo, Seu site primário fica na EU-WEST-2 e seu site secundário fica na AP-SOUTHEAST-2, se o primário falhar no health check, o apontamento passará a pontar para o secundário

- **Geolocation Routing**: Este roteamento permite que você escolha para onde o tráfico vai baseado na localização do usuário final (isto é, de qual local do mundo a requisição se originou). <span style="background-color: #e0a800; color: black;font-weight:bold">É bem útil para localizar o conteúdo. Exemplo: Rotear todas as requisições da França para a versão do site na linguagem francesa e com os preços em Euro.</span>


- **Geoproximity Routing**:<span style="background-color: #e0a800; color: black;font-weight:bold">Este modo de roteamento está disponível apenas no painel de Traffic Flow, permite fazer uma estrutura de resposta bem mais específica e complexa, baseando em lat. e long. e incluir um bias (margem de erro) para esta localização.</span> Muito interessante!

- **Multivalue Answer Routing**: Permite configurar o Route 53 para retornar múltiplos valores, isto é, desde que o valor esteja com seu health check ok.  <span style="background-color: #e0a800; color: black;font-weight:bold">Este roteamento é bem similar ao simple, no entanto ele permite que você coloque um health-check em cada um dos registros.</span>

## Health Checks
O route 53 também oferece um sistema de verificação de integridade do domínio e seus recursos. Garantindo que as requisições DNS sejam direcionadas corretamente.

- Se  um registro falhar no health check, ele será removido do Route 53 até que ele seja aprovado novamente em um novo teste.

- É possível também definir uma notificação no SNS para quando algum registro falhar no health check.

## Anotações
- **(OFF)** Uma coisa que eu não sabia é que dá pra consultar todos os domínios top-level registrados no mundo apenas consultado o site da IANA (Internet Assigned Numbers Authority), veja: https://www.iana.org/domains/root/db.

- **ELBs não possuem um IPv4 definido, portanto é preciso resolver o domínio deles na hora de colocar no Route 53.**

- Por padrão, a quantidade de domínios que você pode registrar em uma única conta é 50. No entanto, é possível aumentar este limite contatando o suporte da AWS.