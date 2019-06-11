title: Processamento Batch
Description: Tem o objetivo de registrar o processamento batch, que poderá ser utilizado em outras rotinas do sistema.
# Processamento Batch

Esta funcionalidade tem o objetivo de registrar a utilização de processamento batch, que
poderá ser utilizado em outras rotinas do sistema.

Rotinas como:

   - Verificação de e-mail
   
   - Verificação da hora do servidor
   
   - Distribuição automática de Tickets com balanceamento carga de trabalho 

Procedimento
----------------

1.  Acessar a funcionalidade através da navegação no menu principal Sistema \>
    Processamento Batch;

2.  Clicar no botão "Novo";

3.  Preencher os campos disponibilizados (descrição, tipo [classe Java,
    RhinoScript, SQL]; situação; expressão cron que define o horário de execução
    da rotina e o conteúdo da rotina, onde será descrito o contexto da rotina a
    ser executada na ferramenta);
    
    Exemplo de conteúdo "Clase Java":
    ```html
    br.com.centralit.citcorpore.quartz.job.JobConfiguracaoAberturaAutomaticaViaEmail
    ```

4.  Clicar em "Gravar".

Rotinas Batch
-----------------

-   Retornar horário do Servidor (baixar script em anexo);

    -   Tipo: RhinoScript
    -   Conteúdo:
    ```html
    br.com.centralit.citcorpore.quartz.job.JobConfiguracaoAberturaAutomaticaViaEmail
    ```

-   Realizar leitura de e-mail (baixar script em anexo).

    -   Tipo: Classe Java
    -   Conteúdo:
        [Baixar Script][2]


!!! tip "About"

    <b>Product/Version:</b> CITSmart | 8.00 &nbsp;&nbsp;
    <b>Updated:</b>01/18/2019 – Anna Martins


[1]:/pt-br/citsmart-platform-8/platform-administration/configuring-automatic-actions/images/rotina-verificar-email.docx
[2]:/pt-br/citsmart-platform-8/platform-administration/configuring-automatic-actions/images/rotina-retorna-hora-servidor.docx
