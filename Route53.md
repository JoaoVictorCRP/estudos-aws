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






## Anotações
- **(OFF)** Uma coisa que eu não sabia é que dá pra consultar todos os domínios top-level registrados no mundo apenas consultado o site da IANA (Internet Assigned Numbers Authority), veja: https://www.iana.org/domains/root/db.

- ELBs não possuem um IPv4 definido, portanto é preciso resolver o domínio deles na hora de colocar no Route 53.