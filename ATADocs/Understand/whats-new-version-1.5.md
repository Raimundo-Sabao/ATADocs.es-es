---
# required metadata

title: Novedades de ATA versión 1.5 | Microsoft Advanced Threat Analytics
description: Se enumeran las novedades de ATA versión 1.5 junto con los problemas conocidos
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: a0d64aff-ca9e-4300-b3f8-eb3c8b8ae045

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Novedades de ATA versión 1.5
En estas notas de la versión encontrará información sobre los problemas conocidos de esta versión de Advanced Threat Analytics.

## ¿Cuáles son las novedades de la actualización de ATA 1.5?
La actualización de ATA 1.5 ofrece mejoras en las siguientes áreas:

-   Tiempos de detección más rápidos

-   Algoritmo de detección automática mejorado para dispositivos NAT (traducción de direcciones de red)

-   Proceso de resolución de nombres mejorado para dispositivos no unidos a dominios

-   Posibilidad de migrar datos durante las actualizaciones del producto

-   Mejor capacidad de respuesta de la interfaz de usuario para detectar actividades sospechosas con miles de entidades involucradas

-   Mejor resolución automática de las alertas de supervisión

-   Más contadores de rendimiento que mejoran la supervisión y solución de problemas

## Problemas conocidos
Esta versión presenta los siguientes problemas conocidos.

### Error de instalación de nuevas puertas de enlace de ATA
Tras actualizar la implementación de ATA a la versión 1.5, obtiene el siguiente error al instalar una nueva puerta de enlace de ATA: La puerta de enlace de Microsoft Advanced Threat Analytics no está instalada

![Error de puerta de enlace de ATA](media/ata-install-error.png)

<b>Solución alternativa:</b> envíe un correo electrónico a <ataeval@microsoft.com> para solicitar los pasos para solucionar el problema.
### Implementación
La carpeta especificada en "Ruta de acceso a datos de base de datos" y "Ruta de acceso al diario de la base de datos" debe estar vacía (no debe contener archivos ni subcarpetas).
Si no está vacía, la implementación no continuará.

### Instalación desde un archivo ZIP
Al instalar la puerta de enlace de ATA, procure extraer los archivos del archivo ZIP en un directorio local e instalarlos desde allí. No instale la puerta de enlace de ATA directamente desde el archivo ZIP o se producirá un error en la instalación.

### Configuración
Tras configurar una puerta de enlace de ATA, cuando esa puerta de enlace de ATA se inicia por primera vez, aparece la etiqueta "No sincronizado" hasta que el servicio se inicie totalmente, lo que puede tardar hasta 10 minutos la primera vez que el servicio se inicia.

### Software de captura de red
El único software de captura de red que se puede instalar en la puerta de enlace de ATA es el [Monitor de red 3.4 de Microsoft](http://www.microsoft.com/en-us/download/details.aspx?id=4865). No instale el Analizador de mensajes de Microsoft ni ningún otro software de captura de red. Instalar otro software hará que la puerta de enlace de ATA deje de funcionar correctamente.

### KB en el host de virtualización
No instale KB 3047154 en un host de virtualización. Esto puede hacer que la creación de reflejo del puerto deje de funcionar correctamente.

## Véase también

[Actualización de ATA a la versión 1.5 (guía de migración)](ata-update-1.5-migration-guide.md)

[Actualización de ATA a la versión 1.6 (guía de migración)](ata-update-1.6-migration-guide.md)

[¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


