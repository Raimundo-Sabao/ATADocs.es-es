---
# required metadata

title: "Instalación de ATA: paso 3 | Microsoft Advanced Threat Analytics"
description: "El paso tres de la instalación ATA le ayuda a descargar el paquete de instalación de la puerta de enlace de ATA."
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 7fb024e6-297a-4ad9-b962-481bb75a0ba3

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Instalación de ATA: paso 3

>[!div class="step-by-step"]
[« Paso 2](install-ata-step2.md)
[Paso 4 »](install-ata-step4.md)

## Paso 3: Descargar el paquete de instalación de puerta de enlace de ATA
Después de configurar la conectividad de dominio puede descargar el paquete de instalación de puerta de enlace de ATA. La puerta de enlace de ATA se puede instalar en un servidor dedicado o en un controlador de dominio. Si la instala en un controlador de dominio, se instalará como una puerta de enlace ligera de ATA. Para obtener más información sobre la puerta de enlace ligera de ATA, consulte [ATA Architecture (Arquitectura de ATA)](/advanced-threat-analytics/plan-design/ata-architecture). 

Para descargarlo:

1.  Desde la consola de ATA, haga clic en el icono de configuración y seleccione **Configuración**.

    ![Opciones de configuración de la puerta de enlace de ATA](media/ATA-config-icon.JPG)

2.  En la pestaña **Puertas de enlace de ATA**, haga clic en **Descargar configuración de puerta de enlace de ATA**.

3.  Guarde el paquete localmente.
4.  Copie el paquete en el servidor dedicado o el controlador de dominio en el que va a instalar la puerta de enlace de ATA. También puede abrir la consola de ATA desde el servidor dedicado o el controlador de dominio y omitir este paso.

El archivo ZIP incluye los siguientes elementos:

-   Instalador de puerta de enlace de ATA

-   Archivo de configuración con la información necesaria para conectarse al Centro ATA


>[!div class="step-by-step"]
[« Paso 2](install-ata-step2.md)
[Paso 4 »](install-ata-step4.md)

## Véase también

- [¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Configurar la recopilación de eventos](configure-event-collection.md)
- [Requisitos previos de ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)


<!--HONumber=May16_HO1-->


