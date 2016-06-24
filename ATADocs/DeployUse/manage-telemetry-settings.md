---
# required metadata

title: Administrar la configuración de telemetría | Microsoft Advanced Threat Analytics
description: Describe los datos que recopila ATA y proporciona los pasos necesarios para desactivar la recopilación de datos.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 8c1c7a1b-a3de-4105-9fd0-08a061952172

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Administrar la configuración de telemetría
Advanced Threat Analytics (ATA) recopila datos de telemetría anonimizados sobre ATA y los transmite a través de una conexión HTTPS a servidores de Microsoft.  Microsoft usa estos datos para ayudar a mejorar las versiones futuras de ATA.

## Datos recopilados
Entre los datos recopilados anonimizados se incluye lo siguiente:

-   Contadores de rendimiento del centro ATA y de la puerta de enlace de ATA

-   Identificador de producto de las copias con licencia de ATA

-   Fecha de implementación del Centro ATA

-   Número de puertas de enlace de ATA implementadas

-   La siguiente información anonimizada de Active Directory:

    -   Identificador de dominio para el dominio cuyo nombre será el primero cuando se ordene alfabéticamente

    -   Número de controladores de dominio

    -   Número de controladores de dominio que supervisa ATA a través de la creación de reflejo del puerto

    -   Número de sitios

    -   Cantidad de equipos

    -   Número de grupos

    -   Número de usuarios

-   Actividades sospechosas: se recopilan los siguientes datos anonimizados de cada actividad sospechosa:

    (**No** se recopilan nombres de equipo, nombres de usuario y direcciones IP)

    -   Tipo de actividad sospechosa

    -   Identificador de actividad sospechosa

    -   Estado

    -   Hora de inicio y finalización

    -   Entrada proporcionada

### Deshabilitar la recopilación de datos
Para dejar de recopilar y de enviar datos de telemetría a Microsoft, siga estos pasos:

1.  Inicie sesión en la consola de ATA, haga clic en los tres puntos de la barra de herramientas y seleccione **Acerca de**.

2.  Desactive la casilla de **Envíenos información de uso para ayudarnos a mejorar su experiencia de cliente en el futuro**.

## Véase también
- [Novedades en la versión 1.6](/advanced-threat-analytics/understand-explore/whats-new-version-1.6)
- [¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


