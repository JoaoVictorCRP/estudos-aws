# Revisões - RDS
Aqui estão algumas perguntas sobre o RDS que eu errei no simulado.

- <span style="background-color:red; color:#fff"> Em vermelho, a resposta que eu assinalei.</span>

- <span style="background-color:green; color:#fff">Em verde, a reposta correta.
</span>



## Criptografia SSL/TLS
_**"A company uses an Amazon RDS MySQL database instance to store customer order data. The security team have requested that SSL/TLS encryption in transit must be used for encrypting connections to the database from application servers. The data in the database is currently encrypted at rest using an AWS KMS key."**_

- [ ] <span style="background-color:green; color:#fff"> A. Download the AWS-provided root certificates. Use the certificates when connecting to the RDS DB instance.
</span>



- [x] <span style="background-color:red;color:#fff">B. Take a snapshot of the RDS instance. Restore the snapshot to a new instance with en cryption in transit enabled.

</span> 

- [ ] C. Add a self-signed certificate to the RDS DB instance. Use the certificates in all connections to the RDS DB instance.

- [ ] D. Enable encryption in transit using the RDS Management console and obtain a key using AWS KMS.

### Explicação
Não há necessidade de criar uma snapshot da instâncias RDS e recriá-la, já que um certificado para criptografia é criado quando as instâncias de BD são bootadas no RDS.

_Read The Docs:_ [Using SSL/TLS to encrypt a connection to a DB instance](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/UsingWithRDS.SSL.html).


## Read Replicas
_**An Amazon RDS Read Replica is being deployed in a separate region. The master database is not encrypted but all data in the new region must be encrypted. <br>How can this be achieved?**_

- [ ] <span style="background-color:green; color:#fff">Encrypt a snapshot from the master DB instance, create a new encrypted master DB instance, and then create an encrypted cross-region Read Replica</span> 

- [ ] Enable encryption using Key Management Service (KMS) when creating the cross-region Read Replica

- [ ] Enabled encryption on the master DB instance, then create an encrypted cross-region Read Replica

- [X] <span style="background-color:red; color:#fff"> Encrypt a snapshot from the master DB instance, create an encrypted cross-region Read Replica from the snapshot</span>

### Explicação
Não é possível criar uma read replica criptografada de um DB master. Também não é possível habilitar a criptografia depois que o master DB já foi inicializado. <br>
Por conta disso, é preciso criar um novo master DB a partir de um snapshot do DB existente, daí é só criptografar e criar um CR Read Replica desse (novo) master DB.

**Meu erro**: A opção que eu assinalei está quase certa, Faltou só um detalhe: É preciso que o master DB  também seja criptografado e não só a CR Read Replica.