title: Cadastrar usuário
Description: Disponibiliza ações diversas, tais como, incluir, alterar e excluir um usuário.
# Cadastrar usuário

Para que o colaborador possa acessar o sistema, é necessário criar um usuário.
O sistema enviará um e-mail com o login e a senha do novo usuário que foi criado 
pelo Citsmart.

Esta funcionalidade disponibiliza ações diversas, tais como, incluir, alterar e
excluir um usuário.

!!! warning "ATENÇÃO"

    O envio de login e senha ao cadastrar novo usuário não engloba usuários importados 
    via AD ou LDAP.

Antes de começar
--------------------

Para cadastrar um usuário é necessário registrar previamente o perfil de acesso
e o colaborador.

Configurar os parâmetros:

|#|Descricão|
|--------|---------|
|33|URL de acesso ao sistema.|
|455|ID do modelo de e-mail que será enviado para o usuário com a senha quando o usuário for criado ou alterado|

O administrador poderá criar um novo modelo de e-mail, editando o modelo preexistente:
    
    ID: 205
    ID do Modelo de E-mail: ACCESSCREDENCIAL

Basta incluir as chaves:
    
    Usuário: ${LOGIN}
    Senha: ${NOVASENHA}

Procedimento
----------------

1.  Acessar a funcionalidade através da navegação no menu principal Cadastros
    Gerais \> Gerência de Pessoal \> Usuário;

2.  Preencher os campos disponibilizados;

3.  Clicar em "Gravar".

4. O sistema verifica se existe um template de e-mail para novo colaborador que possua 
   a chave de senha para envio via e-mail;

5. O administrador do sistema cadastra ou altera um login e senha de um colaborador na tela de usuário;

6. O sistema verifica se:
    
    -    o sistema utiliza a política de senha;
    -    o usuário é LDAP ou não;
    
7. O sistema permite o imput de uma nova senha;

8. Ao gravar o sistema envia por e-mail os novos dados ao colaborador.


Relacionado
-----------

[Cadastrar um colaborador](/pt-br/citsmart-platform-8/initial-settings/access-settings/user/register-employee.html)

[Criar perfil de acesso](/pt-br/citsmart-platform-8/initial-settings/access-settings/profile/create-profile-access.html)

!!! tip "About"

    <b>Product/Version:</b> CITSmart | 8.00 &nbsp;&nbsp;
    <b>Updated:</b>01/18/2019 – Anna Martins

