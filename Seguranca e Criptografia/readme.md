# Sobre Criptografia
A AWS oferece diversas opções de criptografia para diferentes dados, arquivos e serviços. Vejamos alguns dos tipos de criptografia.

## Criptografia Em Trânsito
- Dados são criptografados antes de serem enviados e são descriptografados quando chegam ao destino.

- Certificados TLS são responsáveis pela criprografia na web (HTTPS).

- Esse tipo de criptografia garante segurança contra ataques *Man In The Middle*.

## Criptografia Server-side (at rest)
- Dados são criptografados após o servidor ter recebido eles.

- Dados são descriptografados antes de serem enviados.

- A criptografia ocorre graças a uma chave (data key).
	- A chave, por sua vez, precisa ser alocada em algum lugar onde o servidor possa ter acesso.

## Criptografia Client-side
- Dados são criptografados pelo cliente e NUNCA SERÃO DESCRIPTOGRAFADOS pelo servidor.

- Os dados serão descriptografados apenas pelo próprio cliente que os criptografou.

- Neste modelo, o servidor nunca terá acesso aos dados descriptografados.