---
# required metadata

title: "Cambiar la configuración de ATA: certificado del Centro ATA | Microsoft Advanced Threat Analytics"
description: "Describe el proceso en dos fases para renovar o reemplazar el certificado ubicado en el almacén del equipo local en el servidor del Centro ATA." 
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: c8855287-de3b-4cdd-be8f-2128f48a6f27

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Cambiar la configuración de ATA: certificado del Centro ATA

>[!div class="step-by-step"]
[« Dirección IP del servidor del Centro ATA](modifying-ata-config-centerip.md)
[Dirección IP de la consola de ATA »](modifying-ata-config-consoleip.md)

## Cambiar el certificado del Centro ATA
Si los certificados van a expirar y necesita renovarlos o reemplazarlos después de instalar el nuevo certificado en el almacén del equipo local en el servidor del Centro ATA, reemplace el certificado siguiendo este proceso en dos fases:

-   Primera fase: actualice el certificado que quiera que use el servicio del Centro ATA. En este momento, el servicio del Centro ATA todavía está enlazado al certificado original. Cuando las puertas de enlace de ATA sincronicen su configuración, tendrán dos certificados potenciales válidos para la autenticación mutua. Siempre que la puerta de enlace de ATA pueda conectarse con el certificado original, no intentará hacerlo con el nuevo.

-   Segunda fase: después de que las puertas de enlace de ATA se sincronicen con la configuración actualizada, puede activar el nuevo certificado con el que está enlazado el servicio del Centro ATA. Al activar el certificado nuevo, el servicio del Centro ATA se enlazará con el certificado. Las puertas de enlace de ATA no podrán autenticar mutuamente el servicio del Centro ATA de forma correcta e intentarán autenticar el segundo certificado. Después de conectarse con el servicio del Centro ATA, la puerta de enlace de ATA extraerá la configuración más reciente y tendrá un solo certificado para el Centro ATA. (A menos que haya vuelto a iniciar el proceso).

> [!NOTE]
> -   Si una puerta de enlace de ATA estaba desconectada durante la primera fase y nunca se llegó a actualizar su configuración, deberá actualizar manualmente el archivo de configuración JSON en la puerta de enlace de ATA.
> -   El certificado que use debe ser de confianza para las puertas de enlace de ATA.
> -   Si necesita implementar una nueva puerta de enlace de ATA después de activar el certificado nuevo, debe volver a descargar el paquete de instalación de puerta de enlace de ATA.

1.  Abra la consola de ATA.

2.  Seleccione la opción de configuración en la barra de herramientas y, luego, **Configuración**.

    ![Icono de los valores de configuración de ATA](media/ATA-config-icon.JPG)

3.  Seleccione **Centro ATA**.

4.  En **Certificado**, seleccione uno de los certificados de la lista.

5.  Haga clic en **Guardar**..

6.  Verá una notificación que indica cuántas puertas de enlace de ATA se sincronizaron con la configuración más reciente.

7.  Después de que se sincronicen todas las puertas de enlace de ATA, haga clic en **Activar** para activar el certificado nuevo.
    >[!IMPORTANT]
    >Antes de activar la nueva configuración, compruebe que todas las puertas de enlace de ATA estén sincronizadas con la configuración más reciente. La activación de la nueva configuración antes de que todas las puertas de enlace de ATA estén sincronizadas puede provocar que la puerta de enlace de ATA deje de funcionar según lo esperado. Si cualquiera de las puertas de enlace de ATA no está sincronizada, obtendrá este error cuando haga clic en Activar:
    >
    >    ![Error de sincronización de la puerta de enlace de ATA](media/ataGW-not-synced.png)

8.  Asegúrese de que todas las puertas de enlace de ATA son capaces de sincronizar las configuraciones después de que se haya activado el cambio.

>[!div class="step-by-step"]
[« Dirección IP del servidor del Centro ATA](modifying-ata-config-centerip.md)
[Dirección IP de la consola de ATA »](modifying-ata-config-consoleip.md)

## Véase también
- [Trabajar con la consola de ATA](working-with-ata-console.md)
- [Instalación de ATA](install-ata.md)
- [¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


