---
# required metadata

title: Novedades de ATA versión 1.4 | Microsoft Advanced Threat Analytics
description: Se enumeran las novedades de ATA versión 1.4 junto con los problemas conocidos
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: cbea47f9-34c1-42b6-ae9e-6a472b49e1a5

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Novedades de ATA versión 1.4
En estas notas de la versión encontrará información sobre los problemas conocidos de la versión 1.4 de Advanced Threat Analytics.

## ¿Cuáles son las novedades de esta versión?

-   Posibilidad de que el reenvío de eventos de Windows envíe eventos directamente desde los controladores de dominio a la puerta de enlace de ATA.

-   Mejor detección de ataques pass-the-hash en los recursos corporativos al combinar la inspección profunda de paquetes y los registros de eventos de Windows.

-   Mejor detección y visibilidad de los dispositivos no unidos a dominios y dispositivos que no son de Windows.

-   Mejoras en el rendimiento para dar cabida a más tráfico por puerta de enlace de ATA.

-   Mejoras en el rendimiento para dar cabida a más puertas de enlace de ATA por centro ATA.

-   Se agregó un nuevo proceso de resolución automática de nombres que relaciona los nombres de equipo con las direcciones IP: esta función única ahorrará un tiempo muy valioso en el proceso de investigación y proporcionará pruebas irrefutables a los analistas de seguridad

-   Capacidad mejorada para recopilar información de los usuarios y ajustar automáticamente el proceso de detección.

-   Detección automática de dispositivos NAT.

-   Conmutación por error automática cuando no se puede tener acceso a los controladores de dominio.

-   Ahora las notificaciones y el seguimiento de estado del sistema informan del estado general de la implementación, así como de problemas específicos relacionados con la configuración y la conectividad.

-   Visibilidad de los sitios y las ubicaciones donde las entidades operan.

-   Compatibilidad con varios dominios.

-   Compatibilidad con dominios de una sola etiqueta.

-   Posibilidad de modificar la dirección IP y el certificado de las puertas de enlace de ATA y del centro ATA.

-   Telemetría que contribuye a mejorar la experiencia del cliente.

## Problemas conocidos
Esta versión presenta los siguientes problemas conocidos.

### Software de captura de red
El único software de captura de red que se puede instalar en la puerta de enlace de ATA es el [Monitor de red 3.4 de Microsoft](http://www.microsoft.com/en-us/download/details.aspx?id=4865). No instale el Analizador de mensajes de Microsoft ni ningún otro software de captura de red. Instalar otro software hará que la puerta de enlace de ATA deje de funcionar correctamente.

### Instalación desde un archivo ZIP
Al instalar la puerta de enlace de ATA, procure extraer los archivos del archivo ZIP en un directorio local e instalarlos desde allí. No instale la puerta de enlace de ATA directamente desde el archivo ZIP o se producirá un error en la instalación.

### Desinstalación de versiones anteriores de ATA
Si tiene instalada una versión anterior de ATA o las versiones de vista previa pública o privada, deberá desinstalar el centro ATA y las puertas de enlace de ATA antes de instalar esta versión de ATA.

También habrá que eliminar los archivos de base de datos y los archivos de registro. Las bases de datos de versiones anteriores de ATA no son compatibles con la versión de disponibilidad general de ATA.

Si, al tratar de desinstalar el centro ATA o la puerta de enlace de ATA, se abre la instalación de ATA en lugar de la desinstalación, deberá agregar la siguiente clave del Registro y después intentar desinstalar ATA de nuevo.

**Centro ATA**

-   HKLM\SOFTWARE\Microsoft\Microsoft avanzadas amenazas Analytics\Center

-   Agregue un nuevo valor de cadena denominado `InstallationPath` con el valor `C:\Program Files\Microsoft Advanced Threat Analytics\Center`. Este es el directorio de instalación predeterminado. Si cambió la carpeta de instalación en su momento, escriba la ruta de acceso donde ATA está instalado.

    ![Ruta de instalación del centro ATA en el Editor del Registro](media/ATA-uninstall-center-bug.jpg)

**Puerta de enlace de ATA**

-   HKLM\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Gateway

-   Agregue un nuevo valor de cadena denominado `InstallationPath` con el valor `C:\Program Files\Microsoft Advanced Threat Analytics\Gateway`. Este es el directorio de instalación predeterminado.  Si cambió la carpeta de instalación en su momento, escriba la ruta de acceso donde ATA está instalado.

    ![Ruta de instalación de la puerta de enlace de ATA en el Editor del Registro](media/ATA-GW-uninstall-bug.jpg)

Después de desinstalar, elimine la carpeta de instalación en el centro ATA y la puerta de enlace de ATA.  Si instaló la base de datos en otra carpeta, elimine la carpeta de base de datos en el centro ATA.

### Alerta de estado: puerta de enlace de ATA desconectada
Si dispone de más de una puerta de enlace de ATA y tiene alertas de puerta de enlace de ATA desconectada, solo se resolverá automáticamente en una de ellas, mientras que el resto se quedará en un estado abierto. Tendrá que confirmar manualmente que la puerta de enlace de ATA está activa y el servicio se está ejecutando, así como resolver la alerta manualmente.

### KB en el host de virtualización
No instale KB 3047154 en un host de virtualización. Esto puede hacer que la creación de reflejo del puerto deje de funcionar correctamente.

## Véase también

[Actualización de ATA a la versión 1.6 (guía de migración)](ata-update-1.6-migration-guide.md)

[¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)

<!--HONumber=May16_HO3-->


