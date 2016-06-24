---
# required metadata

title: "Cambiar la configuración de ATA: dirección IP del Centro ATA | Microsoft Advanced Threat Analytics"
description: "Describe cómo cambiar la dirección IP, el puerto o el certificado del Centro ATA."
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 93b27f15-f7e5-49bb-870a-d81d09dfe9fc

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Cambiar la configuración de ATA: dirección IP del Centro ATA

>[!div class="step-by-step"]
[Certificado del Centro ATA »](modifying-ata-config-centercert.md)

Tras la implementación inicial, las modificaciones en el Centro ATA se deben realizar con cuidado. Siga los procedimientos que se indican a continuación al actualizar la dirección IP y el puerto o el certificado.

## Cambiar la dirección IP usada por el servidor del Centro ATA
Si necesita cambiar la dirección IP y el puerto o el certificado del Centro ATA, tenga en cuenta lo siguiente.

Las puertas de enlace de ATA almacenan localmente la dirección IP del Centro ATA con el que deben conectarse. De forma periódica, se conectan con el Centro ATA y extraen los cambios de configuración. El proceso de cambiar la manera en que las puertas de enlace de ATA se conectan con el Centro ATA se lleva a cabo en dos fases.

-   Primera fase: actualice la dirección IP y el puerto que quiere que use el servicio del Centro ATA. En este momento, el Centro ATA todavía escucha en la dirección IP original y la próxima vez que la puerta de enlace de ATA sincronice su configuración tendrá dos direcciones IP para el Centro ATA. Siempre que la puerta de enlace de ATA pueda conectarse con la dirección IP original (la primera), no intentará hacerlo con la dirección IP y el puerto nuevos.

-   Segunda fase: después de que las puertas de enlace de ATA se sincronicen con la configuración actualizada, active la nueva dirección IP y el puerto en el que escucha el Centro ATA. Al activar la dirección IP nueva, el servicio del Centro ATA se enlazará con la nueva dirección IP. Las puertas de enlace de ATA no podrán conectarse con la dirección original e intentarán conectarse con la segunda dirección IP (la nueva) que tienen para el Centro ATA. Después de conectarse con el Centro ATA con la nueva dirección IP, la puerta de enlace de ATA extraerá la configuración más reciente y tendrá una sola dirección IP para el Centro ATA. (A menos que haya vuelto a iniciar el proceso).

> [!NOTE]
> -   Si una puerta de enlace de ATA estaba desconectada durante la primera fase y nunca se llegó a actualizar su configuración, deberá actualizar manualmente el archivo de configuración JSON en la puerta de enlace de ATA.
> -   Si la nueva dirección IP se instala en el servidor del Centro ATA, puede seleccionarla en la lista de direcciones IP al realizar el cambio. Sin embargo, si por algún motivo no puede instalar la dirección IP en el servidor del Centro ATA, puede seleccionar la dirección IP personalizada y agregarla manualmente. No podrá activar la nueva dirección IP hasta que la dirección IP esté instalada en el servidor.
> -   Si necesita implementar una nueva puerta de enlace de ATA después de activar la nueva dirección IP, debe volver a descargar el paquete de instalación de puerta de enlace de ATA.

1.  Abra la consola de ATA.

2.  Seleccione la opción de configuración en la barra de herramientas y, luego, **Configuración**.

    ![Icono de los valores de configuración de ATA](media/ATA-config-icon.JPG)

3.  Seleccione **General**.

4.  En **Dirección IP del servicio del Centro ATA: puerto**, seleccione una de las direcciones IP existentes o **Agregar dirección IP personalizada** y escriba una dirección IP.

5.  Haga clic en **Guardar**..

6.  Verá una notificación que indique cuántas puertas de enlace de ATA se sincronizaron con la configuración más reciente.

    ![Imagen de las puertas de enlace sincronizadas del Centro ATA](media/ATA-chge-IP-after-clicking-save.png)

    >[!IMPORTANT]
    >Antes de activar la nueva configuración, compruebe que todas las puertas de enlace de ATA estén sincronizadas con la configuración más reciente. La activación de la nueva configuración antes de que todas las puertas de enlace de ATA estén sincronizadas puede provocar que la puerta de enlace de ATA deje de funcionar según lo esperado. Si cualquiera de las puertas de enlace de ATA no está sincronizada, obtendrá este error cuando haga clic en Activar:
    >
    >    ![Error de sincronización de la puerta de enlace de ATA](media/ataGW-not-synced.png)


7.  Después de que se sincronicen todas las puertas de enlace de ATA, haga clic en **Activar** para activar la nueva dirección IP.

    > [!NOTE]
    > Si escribió una dirección IP personalizada, no podrá hacer clic en **Activar** mientras no instale la dirección IP en el Centro ATA.

8.  Asegúrese de que todas las puertas de enlace de ATA son capaces de sincronizar las configuraciones después de que se haya activado el cambio. La barra de notificaciones indicará cuántas puertas de enlace de ATA sincronizaron correctamente su configuración.

>[!div class="step-by-step"]
[Cambiar el certificado del Centro ATA »](modifying-ata-config-centercert.md)


## Véase también
- [Trabajar con la consola de ATA](working-with-ata-console.md)
- [Instalación de ATA](install-ata.md)
- [¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


