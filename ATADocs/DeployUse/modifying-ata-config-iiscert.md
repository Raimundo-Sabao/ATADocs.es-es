---
# required metadata

title: "Cambiar la configuración de ATA: certificado de IIS | Microsoft Advanced Threat Analytics"
description: "Describe cómo cambiar el certificado que IIS usa para el Centro ATA."
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: e58a0390-57ef-4c68-a987-2e75e5f3d6b3

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Cambiar la configuración de ATA: certificado de IIS

>[!div class="step-by-step"]
[« Dirección IP de la consola de ATA](modifying-ata-config-consoleip.md)
[Contraseña de conectividad del dominio »](modifying-ata-config-dcpassword.md)

## Cambiar el certificado de IIS
En la consola, puede seleccionar y cambiar el certificado del servicio del Centro ATA, pero no puede cambiar el certificado que IIS usa.

Si quiere cambiarlo, siga este procedimiento:

> [!NOTE]
> Después de modificar el certificado de IIS, debe descargar el paquete de instalación de puerta de enlace de ATA antes de instalar nuevas puertas de enlace de ATA.

Si necesita modificar el certificado que IIS usa para el Centro ATA, siga estos pasos en el servidor del Centro ATA.

1.  Instale el nuevo certificado en el servidor del Centro ATA.

2.  Abra el Administrador de Internet Information Services (IIS).

3.  Expanda el nombre del servidor y **Sitios**.

4.  Seleccione el sitio de la consola de Microsoft ATA y, en el panel **Acciones**, haga clic en **Enlaces**.

    ![Acciones de enlaces de la consola de ATA](media/ATA-console-change-IP-bindings.jpg)

5.  Seleccione **HTTPS** y haga clic en **Editar**.

6.  En **Certificado SSL**, seleccione el nuevo certificado.

7.  Descargue el paquete de instalación de puerta de enlace de ATA antes de instalar una nueva puerta de enlace de ATA.

>[!div class="step-by-step"]
[« Dirección IP de la consola de ATA](modifying-ata-config-consoleip.md)
[Contraseña de conectividad del dominio »](modifying-ata-config-dcpassword.md)

## Véase también
- [Trabajar con la consola de ATA](working-with-ata-console.md)
- [Instalación de ATA](install-ata.md)
- [¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


