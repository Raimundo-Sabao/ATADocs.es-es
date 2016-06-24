---
# required metadata

title: Solución de problemas de ATA con los registros de ATA | Microsoft Advanced Threat Analytics
description: Describe cómo se pueden usar los registros de ATA para ayudar a solucionar problemas
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: b8ad5511-8893-4d1d-81ee-b9a86e378347

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Solución de problemas de ATA con los registros de ATA
Los registros de ATA proporcionan información sobre lo que cada componente de ATA está haciendo en un momento determinado.

## Registros de la puerta de enlace de ATA
En esta sección, todas las referencias a la puerta de enlace de ATA son relevantes también para la puerta de enlace ligera de ATA. 

Los registros de la puerta de enlace de ATA se encuentran en una subcarpeta denominada **Logs** (registros). En la ubicación de instalación predeterminada, se encuentran en **C:\Archivos de programa\Microsoft Advanced Threat Analytics\Gateway\Logs**.

La puerta de enlace de ATA tiene los registros siguientes:

-   **Microsoft.Tri.Gateway.log**: este registro contiene todo lo que ocurre en la puerta de enlace de ATA (incluidos la resolución y los errores). Su uso principal es obtener el estado general de todas las operaciones en el orden cronológico en el que se produjeron.

-   **Microsoft.Tri.Gateway-Resolution.log**: este registro contiene los detalles de resolución de las entidades que se ven en el tráfico de la puerta de enlace de ATA. Su uso principal es investigar los problemas de resolución de entidades.

-   **Microsoft.Tri.Gateway-Errors.log**: este registro solo contiene los errores capturados por la puerta de enlace de ATA. Su uso principal es realizar comprobaciones de estado e investigar los problemas que deben correlacionarse con horas concretas.

-   **Microsoft.Tri.Gateway-ExceptionStatistics.log**: en este registro se agrupan todos los errores y excepciones similares y se cuenta su número.
    Este archivo se encuentra vacío cada vez que se inicia el servicio de la puerta de enlace de ATA y se actualiza cada minuto. Su uso principal es comprender si hay nuevos errores o problemas en la puerta de enlace de ATA. Dado que los errores están agrupados, resulta más fácil leerlos y comprobar si hay algún nuevo tipo de error o problema.

> [!NOTE]
> Los tres primeros archivos de registro tienen un tamaño máximo de 50 MB. Cuando se alcanza este tamaño, se abre un nuevo archivo de registro y se cambia el nombre del anterior a "&lt;nombre de archivo original&gt;-Archived-00000", donde el número se incrementa cada vez que se cambia el nombre.

### Registros del Centro ATA
Los registros del centro ATA se encuentran en una subcarpeta denominada **Logs**. En la ubicación de instalación predeterminada, se encuentran en **C:\Archivos de programa\Microsoft Advanced Threat Analytics\Center\Logs**.

El Centro ATA tiene los registros siguientes:

-   **Microsoft.Tri.Center.log**: este registro contiene todo lo que ocurre en el Centro ATA (incluidos las detecciones y los errores). Su uso principal es obtener el estado general de todas las operaciones en el orden cronológico en el que se produjeron.

-   **Microsoft.Tri.Center-Detection.log**: este registro solo contiene los detalles de detección del Centro ATA. Su uso principal es investigar los problemas de detección.

-   **Microsoft.Tri.Center-Errors.log**: este registro solo contiene los errores capturados por el Centro ATA. Su uso principal es realizar comprobaciones de estado e investigar los problemas que deben correlacionarse con horas concretas.

-   **Microsoft.Tri.Center-ExceptionStatistics.log**: en este registro se agrupan todos los errores y excepciones similares y se cuenta su número.
    Este archivo se encuentra vacío cada vez que se inicia el servicio del Centro ATA y se actualiza cada minuto. Su uso principal es comprender si hay nuevos errores o problemas en el centro ATA. Dado que los errores están agrupados, resulta más fácil leerlos y comprobar si hay algún nuevo tipo de error o problema.

> [!NOTE]
> Los tres primeros archivos de registro tienen un tamaño máximo de 50 MB. Cuando se alcanza este tamaño, se abre un nuevo archivo de registro y se cambia el nombre del anterior a "&lt;nombre de archivo original&gt;-Archived-00000", donde el número se incrementa cada vez que se cambia el nombre.

### Registros de la consola de ATA
Los registros de la consola de ATA (registros de la API de administración) se encuentran en una subcarpeta denominada **Logs**. En la ubicación de instalación predeterminada, se encuentran en **C:\Archivos de programa\Microsoft Advanced Threat Analytics\Center\Management\Logs**.

La consola de ATA tiene los registros siguientes:

-   **w3wp.log**: este registro contiene todo lo que ocurre en el proceso de administración (IIS).


-   **w3wp-Errors.log**: este registro solo contiene los errores capturados por el proceso de administración (IIS).


-   **8e75f9f1-ExceptionStatistics.log**: en este registro se agrupan todos los errores y excepciones similares y se cuenta su número.
    Este archivo se encuentra vacío cada vez que se inicia el servicio de la puerta de enlace y se actualiza cada minuto. Su uso principal es comprender si hay nuevos errores o problemas en el centro ATA. Dado que los errores están agrupados, resulta más fácil leerlos y comprobar si hay algún nuevo tipo de error o problema.

> [!NOTE]
> Los dos primeros archivos de registro tienen un tamaño máximo de 50 MB. Cuando se alcanza este tamaño, se abre un nuevo archivo de registro y se cambia el nombre del anterior a "&lt;nombre de archivo original&gt;-Archived-00000", donde el número se incrementa cada vez que se cambia el nombre.

### Registros de implementación de ATA
Los registros de implementación de ATA se encuentran en el directorio Temp del usuario que instaló el producto. En la ubicación de instalación predeterminada, se encuentran en **C:\Usuarios\Administrador\AppData\Local\Temp** (o en un directorio superior a %temp%).

Registros de implementación del Centro ATA:

-   **Microsoft Advanced Threat Analytics Center_20150601104213.log**: en este registro se enumeran los pasos del proceso de implementación del Centro ATA. Su uso principal es realizar un seguimiento del proceso de implementación del centro ATA.

-   **Microsoft Advanced Threat Analytics Center_20150601104213_0_MongoDBPackage.log**: en este registro se enumeran los pasos del proceso de implementación de MongoDB en el Centro ATA. Su uso principal es realizar un seguimiento del proceso de implementación de MongoDB.

-   **Microsoft Advanced Threat Analytics Center_20150601104213_1_MsiPackage.log**: en este archivo de registro se enumeran los pasos del proceso de implementación de los archivos binarios del Centro ATA. Su uso principal es realizar un seguimiento de la implementación de los archivos binarios del centro ATA.

Registros de implementación de la puerta de enlace de ATA y la puerta de enlace ligera de ATA:

-   **Microsoft Advanced Threat Analytics Gateway_20151214014801.log**: en este registro se enumeran los pasos del proceso de implementación de la puerta de enlace de ATA. Su uso principal es realizar un seguimiento del proceso de implementación de la puerta de enlace de ATA.

-   **Microsoft Advanced Threat Analytics Gateway_20151214014801_001_MsiPackage.log**: en este archivo de registro se enumeran los pasos del proceso de implementación de los archivos binarios de la puerta de enlace de ATA. Su uso principal es realizar un seguimiento de la implementación de los archivos binarios de la puerta de enlace de ATA.

## Véase también
- [Requisitos previos de ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Planeamiento de la capacidad de ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Configurar la recopilación de eventos](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Configurar el reenvío de eventos de Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


