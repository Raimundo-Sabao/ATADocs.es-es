---
# required metadata

title: Trabajar con la configuración de detección de ATA | Microsoft Advanced Threat Analytics
description: Se describe cómo configurar una lista de direcciones IP y subredes que presentan circunstancias poco habituales y que, como tales, se deben tratar de forma distinta a otras entidades de la red
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: f4f2ae30-4849-4a4f-8f6d-bfe99a32c746

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Trabajar con la configuración de detección de ATA
En la página de configuración **Detección** puede configurar una lista de direcciones IP y subredes que presentan circunstancias poco habituales y que, como tales, se deben tratar de forma ligeramente distinta a otras entidades de la red.

## Configurar la detección
En la página **Detección** se pueden definir los siguientes elementos:

-   **Subredes de concesión de corto plazo:** si su organización tiene subredes donde las direcciones IP son muy a corto plazo (por ejemplo, subredes de direcciones IP de VPN o subredes de Wi-Fi), es importante dejar constancia de estas direcciones IP y subredes en ATA para que, de este modo, ATA sepa que la asociación entre un equipo y una dirección IP incluida en estos intervalos debe almacenarse durante un período de tiempo más corto que el de otras direcciones IP.

-   **SID de cuenta de honeytoken:** se trata de una cuenta de usuario que no debe tener ninguna actividad de red. Esta cuenta se configurará como el usuario de honeytoken de ATA. Si alguien intenta usar esta cuenta de usuario de ATA, se creará una actividad sospechosa, lo cual es señal de actividad malintencionada. Para configurar el usuario de honeytoken, necesitará el SID de la cuenta de usuario, no el nombre de usuario.

Puede excluir direcciones IP de las siguientes detecciones. Si una dirección IP figura en una de estas listas, ATA la excluirá de ese tipo específico de actividad detectada.

-   Exclusiones de dirección IP por reconocimiento de DNS

-   Exclusiones de dirección IP por pass-the-ticket

## Véase también
- [Trabajar con actividades sospechosas](working-with-suspicious-activities.md)
- [Modifying ATA configuration (Cambiar la configuración de ATA)](modifying-ata-configuration.md)
- [¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


