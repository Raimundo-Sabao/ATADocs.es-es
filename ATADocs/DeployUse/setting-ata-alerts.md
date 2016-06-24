---
# required metadata

title: Establecer notificaciones de ATA | Microsoft Advanced Threat Analytics
description: Describe cómo establecer alertas de ATA para que se le informe cuando se detecten actividades sospechosas.
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

# Establecer notificaciones de ATA
ATA puede enviar notificaciones cuando detecta una actividad sospechosa, ya sea por correo electrónico o mediante el reenvío de eventos de ATA, y reenviar el evento al servidor SIEM/Syslog. Antes de seleccionar las notificaciones que quiere recibir, tendrá que [configurar el servidor de correo electrónico y el servidor de Syslog](setting-syslog-email-server-settings.md).

> [!NOTE]
> -   Las notificaciones de correo electrónico incluyen un vínculo que llevará al usuario directamente a la actividad sospechosa que se ha detectado. La parte del nombre de host del vínculo se toma de la configuración de la dirección URL de la consola de ATA en la página del Centro ATA. De forma predeterminada, la dirección URL de la consola de ATA es la dirección IP seleccionada durante la instalación del Centro ATA.  Si va a configurar notificaciones de correo electrónico, se recomienda usar un FQDN como dirección URL de la consola de ATA.
> -   Las notificaciones se envían desde el centro ATA al servidor SMTP o al servidor de Syslog.

Para recibir notificaciones de correo electrónico, establezca lo siguiente:


1. En la consola de ATA, seleccione la opción de configuración en la barra de herramientas y, luego, **Configuración**.
![Icono de los valores de configuración de ATA](media/ATA-config-icon.JPG)

2. Seleccione **Notificaciones**.
3. En **Notificaciones por correo electrónico**, use los conmutadores para seleccionar las notificaciones que se enviarán:


    - Se detectó actividad sospechosa nueva
    - Se detectó un problema de estado nuevo
    - Hay disponible una nueva actualización de software

4. Especifique los destinatarios que recibirán las notificaciones por correo electrónico.

    [Nota:]Las alertas de correo electrónico sobre actividades sospechosas solo se envían cuando se crea la actividad sospechosa.


5. Haga clic en **Guardar**.

Para recibir notificaciones de Syslog, establezca lo siguiente:


1. En la consola de ATA, seleccione la opción de configuración en la barra de herramientas y, luego, **Configuración**.
![Icono de los valores de configuración de ATA](media/ATA-config-icon.JPG)

2. Seleccione **Notificaciones**.
3. En **Notificaciones de Syslog**, use los conmutadores para seleccionar las notificaciones que se enviarán:


    - Se detectó actividad sospechosa nueva
    - Se actualizó la actividad sospechosa existente
    - Se detectó un problema de estado nuevo
5. Haga clic en **Guardar**.
![Imagen de configuración de notificación de ATA](media/ATA-notification-settings.png)




## Véase también
[¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Jun16_HO1-->


