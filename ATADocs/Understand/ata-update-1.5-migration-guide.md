---
# required metadata

title: Guía de migración de la actualización de ATA a 1.5 | Microsoft Advanced Threat Analytics
description: Procedimientos para actualizar ATA a la versión 1.5
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: fb65eb41-b215-4530-93a2-0b8991f4e980

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Guía de migración de la actualización de ATA a 1.5
La actualización de ATA 1.5 ofrece mejoras en las siguientes áreas:

-   Tiempos de detección más rápidos

-   Algoritmo de detección automática mejorado para dispositivos NAT (traducción de direcciones de red)

-   Proceso de resolución de nombres mejorado para dispositivos no unidos a dominios

-   Posibilidad de migrar datos durante las actualizaciones del producto

-   Mejor capacidad de respuesta de la interfaz de usuario para detectar actividades sospechosas con miles de entidades involucradas

-   Mejor resolución automática de las alertas de supervisión

-   Más contadores de rendimiento que mejoran la supervisión y solución de problemas

## Actualización de ATA a la versión 1.5
> [!NOTE]
> Si ATA no está instalado en su entorno, descargue la versión completa de ATA, que incluye la versión 1.5, y siga el procedimiento de instalación estándar descrito en [Instalación de ATA](/advanced-threat-analytics/deploy-use/install-ata).

Si ya tiene implementada la versión 1.4 de ATA, este procedimiento le indicará lo que tiene que hacer para actualizar la instalación.

Siga estos pasos para actualizar a la versión 1.5 de ATA:

1.  [Descarar la actualización 1.5](http://aka.ms/ata1_5update)
      > [!NOTE]
         También puede usar la versión completa actualizada de ATA para realizar la actualización a la versión 1.5.


2.  Actualizar el centro ATA

3.  Descargar el paquete de puerta de enlace de ATA actualizado

4.  Actualizar las puertas de enlace de ATA

    > [!IMPORTANT]
    > Actualice todas las puertas de enlace de ATA para procurar que ATA funcione correctamente.

### Paso 1: Actualizar el centro de ATA

1.  Haga una copia de seguridad de la base de datos (opcional):

    -   Si el centro ATA se ejecuta como una máquina virtual y quiere usar un punto de control, cierre primero la máquina virtual.

    -   Si el centro ATA se ejecuta en un servidor físico, siga el procedimiento recomendado para [hacer una copia de seguridad de MongoDB](https://docs.mongodb.org/manual/core/backups/).

2.  Ejecute el archivo de actualización (Microsoft ATA Center Update.exe) y siga las instrucciones en pantalla para instalar la actualización.

    1.  En la **página principal**, seleccione el idioma y haga clic en **Siguiente**.

    2.  Lea el Contrato de licencia para el usuario final y, si acepta las condiciones, active la casilla y haga clic en **Siguiente**.

    3.  Seleccione si quiere realizar una migración parcial o completa (valor predeterminado).

        ![Selección de migración parcial o completa](media/ATA-center-fullpartial.png)

        -   Si selecciona **Parcial**, se eliminarán el tráfico de red recopilado y los eventos de Windows reenviados que ATA haya analizado, y los perfiles de comportamiento de los usuarios tendrán que volver a crearse, lo que conlleva un mínimo de tres semanas. Si tiene poco espacio en disco, merece la pena hacer una migración **parcial**.

        -   Si va a realizar una migración **completa**, necesitará más espacio en disco, según se haya calculado automáticamente en la página de actualización, y la migración podrá tardar más tiempo en función del tráfico de red. Con la migración completa se conservan todos los datos recopilados previamente y los perfiles de comportamiento de los usuarios, lo que significa que ATA no tendrá que invertir tiempo en asimilar los perfiles de comportamiento y podrá detectar comportamientos anómalos inmediatamente después de la actualización.

3.  Haga clic en **Actualizar**. Cuando haga clic en Actualizar, ATA permanecerá sin conexión hasta que el proceso de actualización se complete.

4.  Tras actualizar el centro ATA, las puertas de enlace de ATA indicarán que ahora están obsoletas.

    ![Imagen de puertas de enlace obsoletas](media/ATA-center-outdated.png)

> [!IMPORTANT]
> - Actualice todas las puertas de enlace de ATA para procurar que ATA funcione correctamente.

### Paso 2. Descargar el paquete de instalación de puerta de enlace de ATA
Después de configurar la conectividad de dominio puede descargar el paquete de instalación de puerta de enlace de ATA.

Para descargarlo:

1.  Elimine las versiones anteriores del paquete de puerta de enlace de ATA que haya descargado.

2.  En el equipo con la puerta de enlace de ATA, abra una ventana del explorador y escriba la dirección IP que configuró en el centro ATA para la consola de ATA. Cuando se abra la consola de ATA, haga clic en el icono de configuración y seleccione **Configuración**.

    ![Icono de configuración de ATA](media/ATA-config-icon.JPG)

3.  En la pestaña **Puertas de enlace de ATA**, haga clic en **Descargar configuración de puerta de enlace de ATA**.

4.  Guarde el paquete localmente.

El archivo ZIP incluye los siguientes elementos:

-   Instalador de puerta de enlace de ATA

-   Archivo de configuración con la información necesaria para conectarse al centro ATA

### Paso 3: Actualizar las puertas de enlace de ATA

1.  En cada puerta de enlace de ATA, extraiga los archivos del paquete de puerta de enlace de ATA y ejecute el archivo Microsoft ATA Gateway Setup.

    > [!NOTE]
    > También puede usar este paquete de puerta de enlace de ATA para instalar nuevas puertas de enlace de ATA.

2.  La configuración anterior se conservará, pero es posible que el servicio tarde unos minutos en reiniciarse.

3.  Repita este paso en el resto de puertas de enlace de ATA implementadas.

> [!NOTE]
> Después de actualizar correctamente una puerta de enlace de ATA, la notificación de puerta de enlace de ATA obsoleta desaparecerá.

Sabrá que las puertas de enlace de ATA se han actualizado correctamente cuando todas las puertas de enlace de ATA indiquen que están bien sincronizadas y ya no se muestre el mensaje que informa de que hay disponible un paquete actualizado de puerta de enlace de ATA.

![Imagen de puertas de enlace actualizadas](media/ATA-gw-updated.png)

## Véase también

- [¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


