---
# required metadata

title: Configurar la recopilación de eventos | Microsoft Advanced Threat Analytics
description: Describe las opciones para configurar la recopilación de eventos con ATA
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 3f0498f9-061d-40e6-ae07-98b8dcad9b20

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Configurar la recopilación de eventos
Para mejorar las capacidades de detección, ATA necesita el identificador 4776 del registro de eventos de Windows. Se puede reenviar a la puerta de enlace de ATA de dos maneras diferentes: mediante la configuración de la puerta de enlace de ATA para que escuche eventos de SIEM o mediante la [configuración del reenvío de eventos de Windows](#configuring-windows-event-forwarding).

## Recopilación de eventos
Además de recopilar y analizar el tráfico de red hacia y desde los controladores de dominio, ATA puede usar el evento 4776 de Windows para mejorar aún más la detección de ataques pass-the-hash. Dicho evento puede recibirse mediante SIEM o mediante el establecimiento del reenvío de eventos de Windows desde el controlador de dominio. Los eventos recopilados proporcionan a ATA información adicional que no está disponible a través del tráfico de red del controlador de dominio.

### SIEM/Syslog
Para que ATA pueda consumir datos de un servidor de Syslog, debe hacer lo siguiente:

-   Configure uno de los servidores de puerta de enlace de ATA para que escuche y acepte los eventos que se reenvían desde el servidor SIEM/Syslog.

-   Configure el servidor SIEM/Syslog para que reenvíe eventos específicos a la puerta de enlace de ATA.

> [!IMPORTANT]
> -   No reenvíe todos los datos de Syslog a la puerta de enlace de ATA.
> -   ATA es compatible con el tráfico UDP procedente del servidor SIEM/Syslog.

Consulte la documentación del producto del servidor SIEM/Syslog para obtener información sobre cómo configurar el reenvío de eventos específicos a otro servidor. 

### Reenvío de eventos de Windows
Si no usa un servidor SIEM/Syslog, puede configurar los controladores de dominio de Windows para que reenvíen el identificador 4776 de evento de Windows para que ATA lo recopile y lo analice. El identificador 4776 de evento de Windows proporciona datos sobre autenticaciones NTLM.

## Configurar la puerta de enlace de ATA para que escuche eventos de SIEM

1.  En la configuración de la puerta de enlace de ATA, habilite **Syslog Listener UDP** (UDP de escucha de Syslog).

    Establezca la dirección IP de escucha tal como se describe en la siguiente imagen. El puerto predeterminado es 514.

    ![Imagen Habilitar UDP de escucha de Syslog](media/ATA-enable-siem-forward-events.png)

2.  Configure el servidor SIEM o Syslog para que reenvíe el identificador 4776 de evento de Windows a la dirección IP seleccionada anteriormente. Para más información sobre cómo configurar SIEM, consulte la Ayuda en pantalla de SIEM o las opciones de soporte técnico de los requisitos de formato específicos de cada servidor SIEM.

### Compatibilidad con SIEM
ATA admite eventos de SIEM en los formatos siguientes:

#### RSA Security Analytics
&lt;Encabezado de Syslog&gt;RsaSA\n2015-May-19 09:07:09\n4776\nMicrosoft-Windows-Security-Auditing\nSecurity\XXXXX.subDomain.domain.org.il\nYYYYY$\nMMMMM \n0x0

-   El encabezado de Syslog es opcional.

-   Es necesario incluir el separador de caracteres "\n" entre todos los campos.

-   Los campos, en orden, son los siguientes:

    1.  Constante RsaSA (debe aparecer).

    2.  Marca de tiempo del evento real (asegúrese de que no es la marca de tiempo de la llegada a SIEM o del envío a ATA). Preferiblemente con una precisión de milisegundos; esto es muy importante.

    3.  Identificador de evento de Windows.

    4.  Nombre del proveedor de eventos de Windows.

    5.  Nombre del registro de eventos de Windows.

    6.  Nombre del equipo que recibe el evento (en este caso, el controlador de dominio).

    7.  Nombre del usuario que se autentica.

    8.  Nombre del host de origen.

    9. Código de resultado de NTLM.

-   El orden es importante y no debe incluirse nada más en el mensaje.

#### HP Arcsight
CEF:0|Microsoft|Microsoft Windows||Microsoft-Windows-Security-Auditing:4776|The domain controller attempted to validate the credentials for an account.|Low| externalId=4776 cat=Security rt=1426218619000 shost=KKKKKK dhost=YYYYYY.subDomain.domain.com duser=XXXXXX cs2=Security cs3=Microsoft-Windows-Security-Auditing cs4=0x0 cs3Label=EventSource cs4Label=Reason or Error Code

-   Debe cumplir la definición de protocolo.

-   No hay encabezado de Syslog.

-   Como se indica en el protocolo, debe existir el elemento de encabezado (es decir, la parte que está separada por una barra vertical).

-   Las claves siguientes de la parte _Extensión_ deben estar presentes en el evento:

    -   externalId = Identificador de evento de Windows.

    -   rt = Marca de tiempo del evento real (asegúrese de que no es la marca de tiempo de la llegada a SIEM o del envío a nosotros). Preferiblemente con una precisión de milisegundos; esto es muy importante.

    -   cat = Nombre del registro de eventos de Windows.

    -   shost = Nombre del host de origen.

    -   dhost = Equipo que recibe el evento (en este caso, el controlador de dominio).

    -   duser = Usuario que se autentica.

-   El orden no es importante en la parte _Extensión_.

-   Debe haber una clave personalizada y keyLabel para estos dos campos:

    -   "EventSource"

    -   "Reason or Error Code" = Código de resultado de NTLM

#### Splunk
&lt;Encabezado de Syslog&gt;\r\nEventCode=4776\r\nLogfile=Security\r\nSourceName=Microsoft-Windows-Security-Auditing\r\nTimeGenerated=20150310132717.784882-000\r\ComputerName=YYYYY\r\nMessage=

El equipo ha intentado validar las credenciales de una cuenta.

Paquete de autenticación: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0

Cuenta de inicio de sesión: Administrador

Estación de trabajo de origen: SIEM

Código de error: 0x0

-   El encabezado de Syslog es opcional.

-   Hay un separador de caracteres "\r\n" entre todos los campos obligatorios.

-   Los campos están en formato clave=valor.

-   Las siguientes claves deben existir y tener un valor:

    -   EventCode = Identificador de evento de Windows.

    -   Logfile = Nombre del registro de eventos de Windows.

    -   SourceName = Nombre del proveedor de eventos de Windows.

    -   TimeGenerated = Marca de tiempo del evento real (asegúrese de que no es la marca de tiempo de la llegada a SIEM o del envío a ATA). El formato debe coincidir con yyyyMMddHHmmss.FFFFFF, preferiblemente con una precisión de milisegundos; esto es muy importante.

    -   ComputerName = Nombre del host de origen.

    -   Message = Texto del evento original tomado del evento de Windows.

-   La clave Message y su valor deben aparecer en último lugar.

-   El orden no es importante en los pares clave=valor.

#### QRadar
QRadar habilita la recopilación de eventos a través de un agente. Si los datos se recopilan mediante un agente, el formato de hora se recopila sin datos de milisegundos. Puesto que ATA necesita datos de milisegundos, es necesario establecer QRadar para que use la recopilación de eventos de Windows sin agente. Para obtener más información, consulte [http://www-01.ibm.com/support/docview.wss?uid=swg21700170](http://www-01.ibm.com/support/docview.wss?uid=swg21700170 "QRadar: Agentless Windows Events Collection using the MSRPC Protocol (QRadar: recopilación de eventos de Windows sin agente mediante el protocolo MSRPC)").

    <13>Feb 11 00:00:00 %IPADDRESS% AgentDevice=WindowsLog AgentLogFile=Security Source=Microsoft-Windows-Security-Auditing Computer=%FQDN% User= Domain= EventID=4776 EventIDCode=4776 EventType=8 EventCategory=14336 RecordNumber=1961417 TimeGenerated=1456144380009 TimeWritten=1456144380009 Message=The computer attempted to validate the credentials for an account. Authentication Package: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0 Logon Account: Administrator Source Workstation: HOSTNAME Error Code: 0x0

Los campos necesarios son:

- El tipo de agente de la recopilación
- El nombre del proveedor del registro de eventos de Windows
- El origen del registro de eventos de Windows
- El nombre de dominio completo del controlador de dominio
- Identificador de evento de Windows.

TimeGenerated es la marca de tiempo del evento real (asegúrese de que no sea la marca de tiempo de la llegada a SIEM o del envío a ATA). El formato debe coincidir con aaaaMMddHHmmss.FFFFFF, preferiblemente con una precisión de milisegundos; esto es muy importante.

Message es el texto del evento original tomado del evento de Windows

Asegúrese de tener \t entre los pares clave-valor.

>[!NOTE] No se admite el uso de la recopilación de eventos WinCollect para Windows.

## Configurar el reenvío de eventos de Windows
Si no tiene un servidor SIEM, puede configurar los controladores de dominio para que reenvíen el identificador 4776 de evento de Windows directamente a una de las puertas de enlace de ATA.

1.  Inicie sesión en todos los controladores de dominio y en los equipos de puerta de enlace de ATA con una cuenta de dominio con privilegios de administrador.
2. Asegúrese de que todos los controladores de dominio y las puertas de enlace de ATA a los que se está conectando están unidos al mismo dominio.
3.  En cada controlador de dominio, escriba lo siguiente en un símbolo del sistema con privilegios elevados:
```
winrm quickconfig
```
4.  En la puerta de enlace de ATA, escriba lo siguiente en un símbolo del sistema con privilegios elevados:
```
wecutil qc
```
5.  En cada controlador de dominio, en **Usuarios y equipos de Active Directory**, vaya a la carpeta **Builtin** y haga doble clic en el grupo **Lectores del registro de eventos**.<br>
![wef_ad_eventlogreaders](media/wef_ad_eventlogreaders.png)<br>
Haga clic con el botón derecho y seleccione **Propiedades**. En la pestaña **Miembros**, agregue la cuenta de equipo de cada puerta de enlace de ATA.
![Elemento emergente de lectores del registro de eventos wef_ad](media/wef_ad-event-log-reader-popup.png)
6.  En la puerta de enlace de ATA, abra el Visor de eventos, haga clic con el botón derecho en **Suscripciones** y seleccione **Crear suscripción**.  

    a. En **Tipo de suscripción y equipos de origen**, haga clic en **Seleccionar equipos**, agregue los controladores de dominio y pruebe la conectividad.
    ![Propiedades de wef_subscription](media/wef_subscription-prop.png)

    b. En **Eventos que se recopilarán**, haga clic en **Seleccionar eventos**. Seleccione **Por registro** y desplácese hacia abajo para seleccionar **Seguridad**. Después, en **Incluye o excluye a los Id. de evento**, escriba **4776**.<br>
    ![wef_4776](media/wef_4776.png)

    c. En **Cambiar cuenta de usuario o configurar opciones avanzadas**, haga clic en **Avanzadas**.
Establezca el **Protocolo** en **HTTP** y el **Puerto** en **5985**.<br>
    ![wef_http](media/wef_http.png)

7.  [Opcional] Si quiere un intervalo de sondeo más corto, en la puerta de enlace de ATA establezca el latido de la suscripción en 5 segundos para que la velocidad de sondeo sea más rápida.
    wecutil ss <CollectionName>/cm:custom
    wecutil ss <CollectionName> /hi:5000

8. En la página de configuración de la puerta de enlace de ATA, habilite **Colección de reenvío de eventos de Windows**.

> [!NOTE]
Cuando se habilita esta configuración, la puerta de enlace de ATA buscará en el registro de eventos reenviados los eventos de Windows que se le reenviaron desde controladores de dominio.

Para más información, consulte [Configurar equipos para reenviar y recopilar eventos](https://technet.microsoft.com/en-us/library/cc748890).

## Véase también
- [Instalación de ATA](install-ata.md)
- [¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


