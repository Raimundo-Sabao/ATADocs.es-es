---
# required metadata

title: "Instalación de ATA: paso 2 | Microsoft Advanced Threat Analytics"
description: "El paso dos de la instalación de ATA ayuda a configurar las opciones de conectividad de dominio en el servidor del Centro ATA"
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Instalación de ATA: paso 2

>[!div class="step-by-step"] [« Paso 1](install-ata-step1.md)
[Paso 3 »](install-ata-step3.md)

## Paso 2. Configuración general de la puerta de enlace de ATA
Las opciones de la pestaña de configuración **General** se aplican a todas las puertas de enlace de ATA administradas por el centro ATA.

Para configurar las opciones generales de puertas de enlace de ATA haga lo siguiente:

1.  Abra la consola de ATA e inicie sesión. Para obtener instrucciones, consulte [Working with the ATA Console (Trabajar con la consola de ATA)](working-with-ata-console.md).

2.  Haga clic en el icono de configuración y seleccione **Configuración**.

    ![Opciones de configuración de la puerta de enlace de ATA](media/ATA-config-icon.JPG)

3.  En la pestaña **General**, en **Puertas de enlace de ATA**, escriba la información siguiente y haga clic en **Guardar**.

    |Campo|Comentarios|
    |---------|------------|
    |**Nombre de usuario** (obligatorio)|Escriba el nombre del usuario de solo lectura, por ejemplo: **user1**.|
    |**Contraseña** (obligatorio)|Escriba la contraseña del usuario de solo lectura, por ejemplo: **Pencil1**. **Nota:** Asegúrese de que esta contraseña es correcta. Si guarda una contraseña incorrecta, el servicio de ATA dejará de ejecutarse en los servidores de puerta de enlace de ATA.|
    |**Dominio** (obligatorio)|Escriba el dominio del usuario de solo lectura, por ejemplo: **contoso.com**. **Nota:** Es importante que escriba el FQDN completo del dominio donde se encuentra el usuario. Por ejemplo, si la cuenta de usuario está en el dominio corp.contoso.com, debe escribir `corp.contoso.com`, no contoso.com|
    |Actualizar automáticamente todas las puertas de enlace de ATA |Si habilita esta opción, en próximas versiones, cuando actualice el centro ATA, todas las puertas de enlace de ATA se actualizarán automáticamente.|

    ![Imagen de la configuración de la conectividad de dominio de ATA](media/ata-domain-connectivity-user.jpg)



>[!div class="step-by-step"] [« Paso 1](install-ata-step1.md)
[Paso 3 »](install-ata-step3.md)


## Véase también

- [¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Configurar la recopilación de eventos](configure-event-collection.md)
- [Requisitos previos de ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)


<!--HONumber=May16_HO3-->


