title: Automatically create a ticket from the receiving of an email
Description: Allows to automatic create ticket when an email message is sent to a a certain address.
#Automatically create a ticket from the receiving of an email

This functionality allows to automatic create ticket when an email message is
sent to a a certain address. In this context, the solution constantly monitors
the presence of messages in the mailbox, and if some message has the status of
not read, this will be used to register a new ticket.

For example, an user should request a service by sending a message to
service\@company.com, after receiving the email, the functionality, after check
the existence of a message, automatically registers the ticket. It's important
to highlight that after the ticket registration, the email is marked as read.

Before getting started
--------------------------

To create a ticket through email receiving, it's necessary to configure an email
account to allow the access through IMAP.

Procedure
-------------

*Step 1*

1.  Access the functionality through the main menu System \> Automatic actions
    \> Incident/Request/Procedure Actions (see Register automatic
    actions of incident/request/procedure).

*Step 2*

1.  Create the email automatic action by accessing the main menu System \>
    Settings \> Automatic Action Setting Via Email (see Create
    automatic action via email).

*Step 3*

1.  Create batch routine, by accessing the main menu System \> Batch Processing
    (see Batch Processing):

    -   Download script attached.

!!! Abstract "ATTENTION"

    The information contained in the content of the email message, the addresses
    of the sender, recipient and hidden copy of the email that is read and used
    to register a service request will be collected.

    For this information to be viewed via the Rhino script, the following
    example is attached.


Related
-------

[Register automatic actions of incident/request/procedure](/en-us/citsmart-platform-8/additional-features/automation-of-operation/configuration/register-automatic-actions-incident-request-procedure.html)

[Create automatic action via email](/en-us/citsmart-platform-8/platform-administration/configuring-automatic-actions/email-create-automatic-action-via-email.html)

[Batch Processing](/en-us/citsmart-platform-8/platform-administration/configuring-automatic-actions/batch-batch-processing.html)



Attachment
------------

[Download - Verify email][1]

[Download -Script Rhino email data][2]

!!! tip "About"

    <b>Product/Version:</b> CITSmart Platform | 8.00 &nbsp;&nbsp;
    <b>Updated:</b>01/17/2019 – Anna Martins


[1]:/en-us/citsmart-platform-8/processes/tickets/configuration/images/verify-email.docx

[2]:/en-us/citsmart-platform-8/processes/tickets/images/script-rhino-email.rtf