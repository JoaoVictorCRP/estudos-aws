O **AWS Private Certificate Authority (Private CA)** é um serviço gerenciado da AWS que permite criar e gerenciar uma Autoridade Certificadora(CA) privada para emissão de certificados digitais usados em redes e ambientes internos. ==Ele é parte do AWS Certificate Manager.==

## Para começo de conversa: O que são Certificate Authorities?
Uma **Ceritificate Authority (CA)** é uma entidade confiável responsável por emitir e gerenciar certificados digitais. Esses ==certificados são usados para validar a identidade de sites, serviços e dispositivos, garantindo comunicações seguras e criptografadas através das redes.==

## Como funciona o AWS Private CA?

#### Criação de uma CA privada
- Você cria uma Autoridade Certificadora Raiz (Root CA) ou uma CA Subordinada no AWS Private CA. ***(Ver mais sobre Root e Subordinate no arquivo de Duvidas Comuns)***
	- **Observação: o custo fixo mental de uma CA ativa (root ou subordinate) é ==$400.==** Essa cobrança ocorre independentemente da quantidade de certificados emitidos.

- Essa CA pode emitir certificados privados para uso interno, como para servidores, aplicações e dispositivos IoT.

- Os certificados emitidos ==**não são confiáveis fora do ambiente interno** e não aparecem em navegadores públicos.==

#### Validação e Assinatura
- Quando você cria um certificado, ele é **assinado pela CA privada**.

- A **validação dos certificados é feita localmente**, já que a CA não é pública.

#### Revogação e Gerenciamento
- É possível revogar certificados usando **CRL (Certificate Revocation List)** ou configurar um **OCSP (Online Certificate Status Protocol)**.

- Todas as operações podem ser monitoradas pelo CloudTrail.

## Vantagens do AWS Private CA

- **Totalmente gerenciado**: Não há necessidade de manter servidores ou gerenciar softwares de CA.

- **Integração com o KMS**: É possível integrar com o KMS para proteger as chaves privadas da CA.

- **Integração com o ACM**: Fácil gerenciamento e emissão de certificados direto pelo ACM.

- **==Certificados não possuem resource policies==**. (Errei uma questão no simulado por não saber disso)

## Anotações
- Os usuários podem gerar um **audit report de uma private CA**, o report pode ser salvo em um bucket S3. (Lembre-se de ter uma bucket policy condizente).