
title: Habilitar Event Monitor
Description: Módulo que pretende ser un intermediario entre CITSmart Platform y soluciones de los clientes.
#Habilitar Event Monitor


Event Monitor - EVM - es un módulo que pretende ser un intermediario entre CITSmart Platform y soluciones de los clientes (por ejemplo, Nagios, CITSmart Inventory), sirviendo como un repositorio de informaciones de eventos, generado por herramientas de monitoreo o proceso de inventario.

Para activarlo en una instancia del CITSmart Platform, es necesario descargar el paquete WAR y ejecutar la implementación en el servidor de aplicaciones Wildfly, que puede ser el mismo que el CITSmart Platform. Es importante observar que el EVM debe estar disponible en un puerto diferente de la aplicación ESP. Además, notamos que el EVM no posee su propia interfaz, porque la gestión es hecha a través de la aplicación ESP.

Procedimiento 
----------

1. Descargar el paquete war del component EVM;  
2. Descomprimir los archivos;  
3. Copiar el paquete a la carpeta de implementación del servidor de la aplicación Wildfly;  
4. Configurar [Propriedades del Sistema][1] con los datos de acceso del Mongo y de la instancia del CITSmart Platform;  

Lo que hacer después
---------

Para probar el EVM, [configurar][2] las conexiones en la instancia del CITSmart Platform.  

[1]:/es-es/citsmart-esp-8/get-started/installation-and-upgrade/perform-installation.html
[2]:/es-es/citsmart-esp-8/processes/event/configuration/register-event-monitor-connection.html
