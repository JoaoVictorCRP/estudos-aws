## O que é o IAM?
O **Identity Access Management** é o sistema utilizado para gerenciar os usuários da AWS e seus respectivos privilégios, se quiser usar a AWS, é necessário entender o IAM.

## Features
- Controle do acesso aos recursos da conta.
- Permissões granulares 
- Identity Federation (Logar com a conta do Facebook, Linkedin, Active Directory etc.).
- Autenticação multi-fator
- Acesso temporário para usuários/dispositivos quando necessário.
- Definição de uma política de senha rotacional

## Gerenciamento de Certificados SSL/TLS com IAM Certificate
- O IAM pode ser usado para gerenciar certificados SSL/TLS para serviços como ELB e CloudFront.

- Não há opção de criar certificados diretamente no IAM, você deve importar certificados existentes.

- O principal caso de uso para este recurso é quando você está em uma região que não suporta o AWS Certificate Manager (ACM), ou quando você precisa de usar certificados compatíveis com navegadores mais antigos que não suportam SNI (Server Name Indication).

- A AWS recomenda o uso do ACM sempre que possível, pois ele possui recursos adicionais, como a renovação automática de certificados públicos. **O uso do IAM Certificate é algo legado e reservado para casos específicos**.

## Anotações
- Quando você cria uma conta AWS, você cria apenas o usuário raiz, o qual deve ter seu uso evitado.

- Para criar usuários na conta, basta acessar o painel do IAM e criar os usuários, dessa forma você também pode definir os privilégios de cada um deles.

- Um usuário pode pertencer a vários grupos.

- As roles (funções) são permissões que são atribuídas para a entidades da AWS, tanto usuários quanto serviços (EC2, Lambda, etc)

- Através do IAM, é possível gerar um relatório das credenciais dos usuários na opção **"Credencial Report"**.

- Ao clicar nos detalhes do usuário, você pode ir no painel **Access Advisor para visualizar quais serviços o usuário acessou, qual período ele acessou pela última vez e qual política deu a ele esse direito**, bem útil para validar a granularidade.

- As políticas IAM são definidas em formato JSON. As permissões são definidas de fato no valor de “Statementˮ.