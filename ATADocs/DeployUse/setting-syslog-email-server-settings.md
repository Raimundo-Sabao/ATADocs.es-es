---
# required metadata

title: Establecer notificaciones de ATA | Microsoft Advanced Threat Analytics
description: Se explica cómo hacer que ATA envíe notificaciones (por correo electrónico o mediante el reenvío de eventos de ATA) cuando detecte actividades sospechosas 
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

## Proporcionar a ATA la configuración del servidor de correo electrónico
ATA puede enviar una notificación cuando detecta una actividad sospechosa. Para que ATA pueda enviar notificaciones por correo electrónico, primero hay que configurar las **opciones del servidor de correo electrónico**.

1.  En el servidor del Centro ATA, haga clic en el icono **Administración de Microsoft Advanced Threat Analytics** del escritorio.

2.  Escriba el nombre de usuario y la contraseña y haga clic en **Iniciar sesión**.

3.  Seleccione la opción de configuración en la barra de herramientas y, luego, **Configuración**.

    ![Icono de los valores de configuración de ATA](media/ATA-config-icon.JPG)

4.  En la pestaña **General**, en **Servidor de correo electrónico**, escriba la siguiente información:

    |Campo|Descripción|Valor|
    |---------|---------------|---------|
    |Punto de conexión del servidor SMTP (obligatorio)|Escriba el FQDN del servidor SMTP.|Por ejemplo:<br />smtp.contoso.com|
    |SSL|Cambie a SSL si el servidor SMTP requiere SSL. **Nota:** Si habilita SSL, también deberá cambiar el número de puerto.|El valor predeterminado está deshabilitado|
    |Autenticación|Habilítela si el servidor SMTP requiere autenticación. **Nota:** Si habilita la autenticación, debe proporcionar un nombre de usuario y contraseña de una cuenta de correo electrónico que tenga permiso para conectarse al servidor SMTP.|El valor predeterminado está deshabilitado|
    |Enviar desde (obligatorio)|Escriba una dirección de correo electrónico desde la que se enviará el correo electrónico.|Por ejemplo:<br />ATA@contoso.com|
    ![Imagen de configuración del servidor de correo electrónico de ATA](media/ATA-email-server.png)

## Proporcionar a ATA la configuración del servidor Syslog
ATA puede avisar cuando detecta una actividad sospechosa mediante el envío de una notificación al servidor de Syslog. Si habilita las notificaciones de Syslog, puede establecer lo que se indica a continuación.

1.  Antes de configurar las notificaciones de Syslog, colabore con el administrador de SIEM para averiguar la información siguiente:

    -   FQDN o dirección IP del servidor SIEM

    -   Puerto en el que escucha el servidor SIEM

    -   Tipo de transporte que se va a usar: UDP, TCP o TLS (Syslog seguro)

    -   Formato en el que se va a enviar los datos: RFC 3164 o 5424

2.  En el servidor del Centro ATA, haga clic en el icono **Administración de Microsoft Advanced Threat Analytics** del escritorio.

3.  Escriba el nombre de usuario y la contraseña y haga clic en **Iniciar sesión**.

4.  Seleccione la opción de configuración en la barra de herramientas y, luego, **Configuración**.

    ![Icono de los valores de configuración de ATA](media/ATA-config-icon.JPG)

5.  Seleccione **Servidor de Syslog** y escriba la información siguiente:

    |Campo|Descripción|
    |---------|---------------|
    |Punto de conexión del servidor de Syslog|FQDN del servidor de Syslog|
    |Transporte|Puede ser CDU, TCP o TLS (Syslog seguro)|
    |Formato|Este es el formato que ATA usa para enviar eventos al servidor SIEM: RFC 5424 o RFC 3164.|





## Véase también
[¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


