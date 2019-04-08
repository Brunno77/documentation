title: Como ensinar ANUVA Assitent
#Como ensinar ANUVA Assitent

ANUVA aprende a partir dos diálogos adicionados à sua base de conhecimento. Esses diálogos são estruturados em Interesses (possíveis frases
utilizadas na interação do usuário) e Habilidades (possíveis respostas do chatbot às interações do usuário).
Como a ANUVA Assistant funciona de forma reativa às interações do usuário, para formar diálogos precisamos agrupar interesses e habilidades
em pares. Contextos serão empregados apenas quando, durante o diálogo, for necessário armazenar alguma informação citada pelo usuário para 
utilizar em um outro ponto da conversa.

Cabe ao administrador do chatbot fornecer esses dados ao sistema, estruturando os possíveis diálogos e para que seja realizado o treinamento
do conjunto. O treinamento deve ser agendado pela interface da ANUVA, e ao final do treinamento, a sua assistente será atualizada automaticamente.

Procedimento
------------

1. Acessar o menu principal “Diálogos”;

2. Clicar no botão "Cadastrar" e selecionar uma das opções Simples (apenas um interação Interesse-Habilidade) ou Complexo 
(para unir vários diálogos simples);

3. Informar o Tema relacionado ao Diálogo, isto ajudará a categorizá-los, posteriormente. Um novo tema pode ser cadastrado no menu “Tema”.

4. Na seção **Interesses**, preencher as frases relacionadas ao Interesse do usuário e clicar em “Adicionar”;

5. Na seção **Habilidades**, preencher os campos disponibilizados, atentando-se ao tipo da habilidade:

    - Padrão: será utilizada para representar habilidades que são respondidas através de uma resposta de texto pré-definida. Podem ser 
     atribuídas várias frases pré-definidas de respostas sempre visando responder a mesma pergunta;

    - Personalizada: será utilizada quando, para responder a um interesse do usuário, ANUVA precisar buscar informações em um outro         sistema.

    - Botão: será utilizada sempre que for necessário limitar as respostas do usuário a uma determinada interação da ANUVA. Ao utilizar     essa opção, ANUVA responderá a interação do usuário exibindo botões. Um botão é definido por seu Nome e Valor. No campo Nome, é         definido o botão que aparecerá para o usuário. No campo Valor, é definido para a ANUVA como ela deve interpretar o interesse do         usuário ao clicar no botão;
 
    - Imagem: pode ser utilizada quando desejar responder o usuário utilizando texto e imagem. A imagem associada a resposta será           exibida na janela de chat.

6. Clicar em “Salvar”.

!!! Abstract "NOTA"

    - Diálogos complexos ajudam ANUVA a ser mais assertiva numa conversa que é longa, utilizá-lo para orientá-la
    a como responder nessas situações;
    
    - A compreensão da ANUVA é feita por aproximação, sendo assim, quanto mais frases é adicionada ao Interesse,
    mais precisa ela será no entendimento da interação do usuário. Lembrando que o usuário não precisa digitar 
    a frase exata que foi adicionada ao interesse, pois ANUVA trabalha com Inteligência Artificial;
                
    - Adicionar pelo menos um diálogo com habilidade de *fallback*. Ela será utilizada quando a ANUVA não 
    conseguir entender o interesse do usuário ou entender com uma acurácia inferior a 20%. É possível visualizar 
    a acurácia de cada interação no menu Analytics > Listar conversas.
 
 
Relacionado
--------
 
[Como treinar ANUVA Assistant](/pt-br/anuva/trainning-anuva.html)
 
 

!!! tip "About"

    <b>Product/Version:</b> CITSmart Platform | 8.00 &nbsp;&nbsp;
    <b>Updated:</b>04/07/2019 - Anna Martins
    