## O que é o AWS ACM?
O ACM é um serviço gerenciado da AWS que facilita muito o provisionamento, gerenciamento e renovação automática de certificados SSL/TLS para proteger recursos na nuvem da AWS.
___
## Principais Funcionalidades do ACM

- **Emissão e gerenciamento de certificados SSL/TLS**: Tanto certificados públicos quanto privados (através do <ins>Private CA</ins>) podem ser emitidos através do ACM.

- **Renovação automática**: os certificados públicos emitidos pelo ACM são renovados automaticamente antes da expiração. **==Observação: certificados importados ou privados exigem renovação manual.==**
___
## Tipos de Certificados

#### Certificados públicos
- Gratuitos.
- Gerenciados pela AWS.
- Renovação automática.
#### Certificados privados (AWS Private CA)
- Utilizado para ambientes internos e privados.
- Emitidos via **AWS Private CA**.
- Ideal para VPNs, intranets e dipositivos IoT.

#### Certificados importados
- Certificados adquiridos de CAs externas (*DigiCert, GlobalSign, Let's Encrypt*)
- **Necessário realizar a renovação manualmente**.
___
## OBSERVAÇÕES

- **O ACM é um serviço regional**, portanto caso você possua uma aplicação global, com múltiplos ALBs, por exemplo, você vai precisar gerenciar múltiplos certificados SSL em cada região em que a aplicação está hospedada.

- Não é possível copiar certificados entre regiões.

- **==Os certificados do ACM não são instalados em servidores, e sim em serviços da AWS==** (ELB, CloudFront, API Gateway), é justamente por isso que eles são gratuitos.

- Como escrito acima, **os certificados do ACM não podem ser associados à instâncias EC2.**