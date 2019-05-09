title:  System audit
Description: It allows to manage possible risks to the system
# System audit

This functionality allows to manage the possible risks to the system, when auditing all the executions made in the system in form of logs.

Before getting started 
-----------------

It's necessary to have installed the following products:

-   ACTIVEMQ with version 5.15.8 or higher;

-   Mongodb.

It's also necessary to set the following parameters in CITSmart (Parametrization \>
Citsmart Parameters):

-   In parameter 52, set the value “true”;

-   In parameter 53, inform the type of log you want. The types are: ‘CIT_LOG’
    (log file) and ‘DB_LOG’ (save in the base);

-   In parameter 425, inform the URL access to the CITSmart Audit (Eg.:
    http://localhost:8088);

-   IN parameter 424, inform the URL access to the ActiveMQ (Eg.:tcp://citACTIVEMQ:61616).

Procedure
------------

***Process to configure the Audit***

*Configuration to create a backup of the audits.*

First, it's essential to configure the specific parameters of the functionality.

1.  Access the main menu Parametrization \> Audit Parametrization;

2.  Inform in the field "Directory" the folder where it'll be kept all *logs* of
    the audits made;

3.  In the "Frequency in days" field, it's possible to adjust a backup routine of
    the audit logs, by choosing the periodicity of the backup in days.

    !!! Abstract "NOTE"

        The choice of frequency should be from 1 (one) day to the execution of the backup.  

4.  The possibility of determining a specific period (start and end date) for the
    generation of system audit logs is made available.

    !!! note "IMPORTANT"

        It's offered three types of system audit: audit of system data, system access
        and system licenses .

***System data audit***

*It presentes the history of all change, inclusion, and deletion of data in the
system.*

1.  Access the main menu System \> Audit trail \> System logs;

2.  It'll be presented the audit logs of every move performed in the program,
    showing the date and time of the updates, the IP address, the executor
    name of the update, the name of the table, the type of operation made in 
    the system. Clicking on the data button, it'll show what was actually updated in the program.

    !!! Abstract "NOTE"  

        The "Operations" field presents the type of action made in the system 
        in thesis. It's defined by symbols, and their meanings are:  
        
        -   The letter "C" stands for "Change" in the system data;  
        
        -   The letter "I" stands for "Insertion" of new data into the system;  

        -   The letter "D" stands for "Deletion" of system data.  

3.  It's also released the search of a *log* through filters available in the screen.

***System access audit***

*It presentes the history of access in the system (login and logout).*

1.  Access the main menu System \>
    Audit trail \> Access audit;

2.  It'll present the users that made login and logout in the system, alos
    registering the date and hour of each of theses activities;

    !!! Abstract "NOTE"  
        
        If the system expires, it will not be possible to capture the system logout,
        so only the login information of the access session will be registered.  

3.  There are filters to help in the search of an access.

***System license audit***

*Inform the licenses used to validate the system.*

1.  Access the main menu System \>
    Audit trail \> Audit license;

2.  It presents the license data acquired and used to execute the system;

3.  It's possible to search for a license and its deadline by the filters
    in the main screen.
    
!!! tip "About"

    <b>Product/Version:</b> CITSmart Platform | 8.00 &nbsp;&nbsp;
    <b>Updated:</b>02/15/2019 – Larissa Lourenço
