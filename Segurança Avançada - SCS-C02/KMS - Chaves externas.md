Quando lidamos com uma chave que possui conteúdo importado externamente, precisamos entender alguns detalhes:

- Você é 100% responsável pela segurança, disponibilidade e durabilidade da chave fora da AWS.

- A rotação deve ser feita manualmente. (Automatic Key Rotation não funciona aqui).

- Tanto chaves **Simétricas** (chave única) quanto **Assimétricas** (par de chaves) são suportadas.