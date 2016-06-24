---
# required metadata

title: Guía de migración de la actualización de ATA a 1.6 | Microsoft Advanced Threat Analytics
description: Procedimientos para actualizar ATA a la versión 1.6
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

# Guía de migración de la actualización de ATA a 1.6
La actualización a ATA 1.6 ofrece mejoras en las siguientes áreas:

-   Nuevas detecciones

-   Mejoras en las detecciones existentes

-   La puerta de enlace ligera de ATA

-   Actualizaciones automáticas

-   Rendimiento mejorado del centro ATA

-   Requisitos de almacenamiento inferiores

-   Compatibilidad con IBM QRadar

## Actualización de ATA a la versión 1.6
> [!NOTE] Si ATA no está instalado en el entorno, descargue la versión completa, que incluye la versión 1.6, y siga el procedimiento de instalación estándar descrito en [Instalación de ATA](/advanced-threat-analytics/deploy-use/install-ata).

Si ya tiene implementada la versión 1.5 de ATA, este procedimiento le indicará lo que tiene que hacer para actualizar la implementación.

> [!NOTE] No se puede instalar la versión 1.6 de ATA directamente sobre la versión 1.4. Primero hay que instalar la versión 1.5 de ATA. Si accidentalmente intentó instalar ATA 1.6 sin instalar ATA 1.5, obtendrá un error que indica que **Ya existe una versión más reciente instalada en el equipo**. Debe desinstalar los remanentes de ATA 1.6 que queden en el equipo, aunque se produjera un error en la instalación, antes de instalar la versión 1.5 de ATA.

Siga estos pasos para actualizar a la versión 1.6 de ATA:

1. Antes de comenzar el proceso de actualización, asegúrese de seguir el procedimiento para controlar el [Error de migración al actualizar a la versión 1.6 de ATA](whats-new-version-1.6#Migration-failure-when-updating-from-ATA-1.5)
2. Asegúrese de contar con el espacio necesario para completar la actualización. Puede realizar la instalación hasta la comprobación de preparación para obtener una estimación de cuánto espacio libre necesita y luego reiniciar la actualización tras asignar el espacio en disco necesario. La actualización usará al menos un 2 % del tamaño de la base de datos, consulte [ATA Capacity Planning (Planeamiento de la capacidad de ATA)](/advanced-threat-analytics/plan-design/ata-capacity-planning) para obtener más información.
1.  [Descargar la actualización 1.6](http://www.microsoft.com/en-us/evalcenter/evaluate-microsoft-advanced-threat-analytics)<br>
En esta versión, se usa el mismo archivo de instalación (Microsoft ATA Center Setup.exe) para instalar una nueva implementación de ATA y para actualizar implementaciones existentes.

2.  Actualizar el centro ATA

3.  Descargar el paquete de puerta de enlace de ATA actualizado

4.  Actualizar las puertas de enlace de ATA

    > [!IMPORTANT] Actualice todas las puertas de enlace de ATA para procurar que ATA funcione correctamente.

### Paso 1: Actualizar el centro de ATA

1.  Haga una copia de seguridad de la base de datos (opcional):

    -   Si el centro ATA se ejecuta como una máquina virtual y quiere usar un punto de control, cierre primero la máquina virtual.

    -   Si el centro ATA se ejecuta en un servidor físico, siga el procedimiento recomendado para [hacer una copia de seguridad de MongoDB](https://docs.mongodb.org/manual/core/backups/).

2.  Ejecute el archivo de instalación (Microsoft ATA Center Setup.exe) y siga las instrucciones en pantalla para instalar la actualización.

    1.  ATA 1.6 requiere la instalación de .NET Framework 4.6.1. Si aún no está instalado, la instalación de ATA instalará .Net Framework 4.6.1 como parte de la instalación<br>
    > [!NOTE]La instalación de .Net Framework 4.6.1 puede requerir que reinicie el servidor. La instalación de ATA continuará después de que se haya reiniciado el servidor.
5.  En la **página principal**, seleccione su idioma y haga clic en **Siguiente**.

    6.  Lea el Contrato de licencia para el usuario final y, si acepta las condiciones, haga clic en **Siguiente**.

    7.  Ahora se puede usar Microsoft Update para que ATA permanezca actualizado.  En la página de Microsoft Update, seleccione **Usar Microsoft Update al buscar actualizaciones (recomendado)**.
    ![Imagen de mantenimiento de ATA al día](media/ata_ms_update.png) Esto ajustará la configuración de Windows para habilitar las actualizaciones de otros productos de Microsoft (incluido ATA), como se ve aquí. 
     ![Imagen de actualización automática de Windows](media/ata_installupdatesautomatically.png)

    8.  Antes de comenzar la instalación, ATA llevará a cabo una comprobación de preparación. Revise los resultados de la comprobación para asegurarse de que los requisitos previos están configurados correctamente y de que tiene al menos la cantidad mínima de espacio en disco. 
    ![Imagen de comprobación de preparación de ATA](media/ata_install_readinesschecks.png)

    3.  Haga clic en **Actualizar**. Después de hacer clic en Actualizar, ATA permanecerá sin conexión hasta que el proceso de actualización se complete.

4.  Tras actualizar el centro ATA, las puertas de enlace de ATA indicarán que ahora están obsoletas.

    ![Imagen de puertas de enlace obsoletas](media/ATA-center-outdated.png)

> [!IMPORTANT]
> - Actualice todas las puertas de enlace de ATA para procurar que ATA funcione correctamente.

### Paso 2. Descargar el paquete de instalación de puerta de enlace de ATA
Después de configurar la conectividad de dominio, puede descargar el paquete de instalación de puerta de enlace de ATA.

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

1.  En cada puerta de enlace de ATA, extraiga los archivos del paquete de puerta de enlace de ATA y ejecute el archivo **Microsoft ATA Gateway Setup.exe**.

    > [!NOTE] También puede usar este paquete de puerta de enlace de ATA para instalar nuevas puertas de enlace de ATA.

2.  La configuración anterior se conservará, pero es posible que el servicio tarde unos minutos en reiniciarse.

3.  Repita este paso en el resto de puertas de enlace de ATA implementadas.

> [!NOTE] Después de actualizar correctamente una puerta de enlace de ATA, la notificación de puerta de enlace de ATA obsoleta se resolverá.

Sabrá que las puertas de enlace de ATA se han actualizado correctamente cuando todas las puertas de enlace de ATA indiquen que están bien sincronizadas y ya no se muestre el mensaje que informa de que hay disponible un paquete actualizado de puerta de enlace de ATA.

![Imagen de puertas de enlace actualizadas](media/ATA-gw-updated.png)


## Véase también

- [¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO4-->


