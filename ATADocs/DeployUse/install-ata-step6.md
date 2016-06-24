---
# required metadata

title: Instalación de ATA | Microsoft Advanced Threat Analytics
description: En el paso final de la instalación de ATA, configurará las subredes de concesión a corto plazo y el usuario de honeytoken.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Instalación de ATA: paso 6

>[!div class="step-by-step"]
[« Paso 5](install-ata-step5.md)

## Paso 6. Configurar las subredes de concesión a corto plazo y el usuario de honeytoken
Las subredes de concesión a corto plazo son subredes en que la asignación de direcciones IP cambia muy rápidamente, en cuestión de segundos o minutos. Por ejemplo,las direcciones IP usadas para las VPN y las direcciones IP Wi-Fi. Para especificar la lista de subredes de concesión a corto plazo que se usan en su organización, siga estos pasos:

1.  Desde la consola de ATA en el equipo de puerta de enlace de ATA, haga clic en el icono de configuración y seleccione **Configuración**.

    ![Valores de configuración de ATA](media/ATA-config-icon.JPG)

2.  En **Detección**, escriba lo siguiente para las subredes de concesión a corto plazo. Escriba las subredes de concesión a corto plazo con el formato de notación de barra diagonal, por ejemplo: `192.168.0.0/24` y haga clic en el signo más.

3.  En el caso de SID de cuenta de honeytoken, escriba el SID de la cuenta de usuario que no tendrá actividad de red y haga clic en el signo más. Por ejemplo: `S-1-5-21-72081277-1610778489-2625714895-10511`.

    > [!NOTE]
    > Para encontrar el SID de un usuario, busque el usuario en la consola de ATA y luego haga clic en la pestaña **Información de cuenta**. 

4.  Configurar exclusiones: puede configurar direcciones IP para que se excluyan de determinadas actividades sospechosas. Consulte [Trabajar con la configuración de detección de ATA](working-with-detection-settings.md) para obtener más información.

5.  Haga clic en **Guardar**..

![Guardar cambios](media/ATA-VPN-Subnets.JPG)

Enhorabuena, ha implementado correctamente Microsoft Advanced Threat Analytics.

Compruebe la línea de tiempo de ataque para ver las actividades sospechosas detectadas y para buscar usuarios o equipos y ver sus perfiles.

ATA iniciará la exploración para detectar actividades sospechosas inmediatamente. Algunas actividades, por ejemplo algunas de las de comportamiento sospechoso, no estarán disponibles hasta que ATA haya tenido tiempo de generar perfiles de comportamiento (mínimo de tres semanas).


>[!div class="step-by-step"]
[« Paso 5](install-ata-step5.md)


## Véase también

- [¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Configurar la recopilación de eventos](configure-event-collection.md)
- [Requisitos previos de ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=May16_HO1-->


