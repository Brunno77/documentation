title: Crear ticket automático desde el recebimiento del correo electrónico
Description: Permite la creación automática de un ticket cuando se envía un mensaje de correo electrónico a una dirección determinada.
#Crear ticket automático desde el recebimiento del correo electrónico


Esta funcionalidad permite la creación automática de un ticket cuando se envía
un mensaje de correo electrónico a una dirección determinada. En este contexto,
la solución monitorea constantemente la presencia de mensajes en el buzón de
correo, y si algún mensaje tiene el estado no leído, éste se utilizará para
registrar un nuevo ticket.

Por ejemplo, un usuario podría solicitar cierto servicio enviando un mensaje a
servico\@empresa.com, después de recibir el correo electrónico, la
funcionalidad, luego que comprobar que existe un mensaje, registra un ticket
automáticamente. Es importante destacar que después del registro del ticket, el
correo electrónico es marcado como leído.

Antes de empezar
--------------------

Para crear un ticket a través del recibimiento del correo electrónico, es
necesario configurar previamente una cuenta de correo electrónico para permitir
el acceso a través del IMAP.

Procedimiento
-----------------

*Paso 1*

1.  Acceder al menú principal Sistema \> Acciones Automaticas \> Acciones de
    Incidentes/Requerimientos/Procedimientos (ver Registrar acciones
    automaticas de incidentes/requerimientos/precedimientos).

*Paso 2*

1.  Crear acción automatica de correo electrónico al acceder al menú principal
    Sistema \> Configuración \> Configuración de la acción automatica a través
    de correo electrónico (ver Crear acción automatica de correo
    electrónico).

*Paso 3*

1.  Crear Rutina Batch al acceder al menú principal Sistema \> Procesamiento
    Batch (ver Procesamiento Batch):

    -   Descargar el guión.

!!! Abstract "ATENCIÓN"

    Se recopilará la información contenida en el contenido del mensaje de correo electrónico, las direcciones del remitente, el             destinatario y la copia oculta del correo electrónico que se lee y se utiliza para registrar una solicitud de servicio.
    
    Para que esta información se vea a través de la secuencia de comandos Rhino, sigue el ejemplo adjunto.


Relacionado
-------

[Registrar acciones automaticas de incidentes/solicitudes/procedimientos](/es-es/citsmart-esp-8/additional-features/automation-of-operation/configuration/register-automatic-actions-incident-request-procedure.html)

[Crear acción automatica via correo eletronico](/es-es/citsmart-esp-8/platform-administration/configuring-automatic-actions/email-create-automatic-action-via-email.html)

[Procesamiento Batch](/es-es/citsmart-esp-8/platform-administration/configuring-automatic-actions/batch-batch-processing.html)


<i class='fa fa-youtube-play  fa-2x' style='color:#97ce17;vertical-align: middle;'> </i> [Video Library](https://www.youtube.com/playlist?list=PLB5qK2uzf2ROl8PJLi-kszYhGzr17uvz-)'

Adjunto
------------
[Download - Comprobar email][1]

[Download -Script Rhino datos del email][2]


!!! tip "About"

    <b>Product/Version:</b> CITSmart ESP | 8.00 &nbsp;&nbsp;
    <b>Updated:</b>01/25/2019 – Anna Martins
    
[1]:/es-es/citsmart-esp-8/processes/tickets/images/rotina-verificar-email.docx
  
[2]:/es-es/citsmart-esp-8/processes/tickets/images/script-rhino-dados-email.rtf
