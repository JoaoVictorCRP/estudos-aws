Este é um serviço gerenciado de streaming de aplicações e desktops virtuais, ou seja, ==ele permite que softwares e ambientes inteiros de desktop sejam executados na AWS, mas acessados via navegador por qualquer dispositivo, bem bacana.==

## Como funciona?
- Você instala sua aplicação em uma imagem gerenciada na nuvem da AWS. (É uma imagem própria do AppStream, não uma AMI ou Imagem de Container)

- Os usuários acessam essa aplicação **sem precisar instalar nada localmente**, apenas usando o navegador.

- A renderização da aplicação ocorre no backend da AWS, e o que é transmitido ao usuário é só o **vídeo da interface + os eventos do mouse/teclado**, como um streaming interativo. (Isso me lembra o ==XCloud==)

## Benefícios
- **Escalável**: Dá pra adicionar/remover usuários com facilidade.
- **Seguro**: Os dados nunca saem da AWS (ideal para evitar vazamento).
- **Compatível com AD e SSO**.
- **Paga apenas pelo uso** (streaming + instâncias)

## Observações
- Você pode copiar imagens entre regiões caso precise.