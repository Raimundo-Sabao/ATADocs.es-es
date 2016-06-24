---
# required metadata

title: Centro de mantenimiento de ATA | Microsoft Advanced Threat Analytics
description: Use el centro de mantenimiento de ATA para saber cómo funciona el servicio de ATA y recibir alertas de posibles problemas.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: d6c783b2-46c5-4211-b21a-d6b17f08d03d

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Centro de mantenimiento de ATA
El centro de mantenimiento de ATA permite conocer el rendimiento del servicio de ATA y alerta de posibles problemas.

## Trabajar con el centro de mantenimiento de ATA
Con el centro de mantenimiento de ATA, sabrá que hay un problema porque verá un punto rojo (señal de alerta) encima del icono del centro de mantenimiento en la barra de menús.

![Barra de herramientas de punto rojo del centro de mantenimiento de ATA](media/ATA-Health-Center-Alert-red-dot.png)

### Administrar el estado de ATA
Para comprobar el estado general del sistema, haga clic en el icono del centro de mantenimiento en la barra de menús. ![Icono del centro de mantenimiento de ATA](media/ATA-red-dot.png)

-   Todas las alertas abiertas se pueden administrar estableciéndolas en **Resuelta** o **Descartada**. En la alerta en cuestión, haga clic en **Abrir** y desplácese hasta **Resuelta** o **Descartada**.

-   Si resuelve un problema y ATA detecta que el problema persiste, el problema volverá a incluirse automáticamente en la lista de problemas **abiertos**. Si ATA detecta que un problema abierto se ha resuelto, se moverá automáticamente a la lista de problemas **resueltos**.

-   Los problemas **descartados** son aquellos que no quiere que ATA siga comprobando; por ejemplo, si recibe alertas de un problema que sabe que existe, pero que no tiene intención de resolver, y no quiere seguir recibiendo notificaciones ni verlo en la lista de problemas **abiertos**, puede configurarlo como **descartado**.

![Imagen de problemas del centro de mantenimiento de ATA](media/ATA-Health-Issue.JPG)

## Véase también
- [Trabajar con la configuración de detección de ATA](working-with-detection-settings.md)
- [Trabajar con actividades sospechosas](working-with-suspicious-activities.md)
- [¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


