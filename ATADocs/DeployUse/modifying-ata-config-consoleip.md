---
# required metadata

title: "Cambiar la configuración de ATA: dirección IP de la consola de ATA | Microsoft Advanced Threat Analytics"
description: "Describe cómo cambiar la dirección IP de la consola de ATA, que se usa para crear un acceso directo a la consola de ATA en las puertas de enlace de ATA."
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 50118465-df34-4e04-b0cc-48808b6a96b1

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Cambiar la configuración de ATA: dirección IP de la consola de ATA

>[!div class="step-by-step"]
[« Certificado del Centro ATA](modifying-ata-config-centercert.md)
[Certificado de IIS »](modifying-ata-config-iiscert.md)

## Cambiar la dirección IP de la consola de ATA
De forma predeterminada, la dirección URL de la consola de ATA es la dirección IP seleccionada para la dirección IP de la consola de ATA cuando se instaló el Centro ATA.

La dirección URL se usa en los escenarios siguientes:

-   Instalación de puertas de enlace de ATA: cuando se instala una puerta de enlace de ATA, se registra automáticamente en el Centro ATA. Este proceso de registro se lleva a cabo a través de la conexión con la consola de ATA. Si especifica un FQDN para la dirección URL de la consola de ATA, debe asegurarse de que la puerta de enlace de ATA pueda resolver el FQDN en la dirección IP con la que está enlazada la consola de ATA en IIS. Además, la dirección URL se usa para crear el acceso directo a la consola de ATA en las puertas de enlace de ATA.

-   Alertas: cuando ATA envía un correo electrónico SIEM o de alerta, incluye un vínculo a la actividad sospechosa. La parte del host del vínculo es el valor de la dirección URL de la consola de ATA.

-   Si ha instalado un certificado desde la entidad de certificación (CA) interna, probablemente le interesará que la dirección URL coincida con el nombre del firmante del certificado, para que los usuarios no obtengan un mensaje de advertencia al conectarse a la consola de ATA.

-   El uso de un FQDN para la dirección URL de la consola de ATA permite modificar la dirección IP que IIS usa para la consola de ATA sin interrumpir las alertas que se enviaron en el pasado y sin que sea necesario volver a descargar el paquete de puerta de enlace de ATA. Solo tendrá que actualizar el DNS con la nueva dirección IP.

> [!NOTE]
> Después de modificar la dirección URL de la consola de ATA, debe descargar el paquete de instalación de puerta de enlace de ATA antes de instalar nuevas puertas de enlace de ATA.

Si necesita modificar la dirección IP que IIS usa para la consola de ATA, siga estos pasos en el servidor del Centro ATA:

1.  Instale la dirección IP en el servidor del Centro ATA.

2.  Abra el Administrador de Internet Information Services (IIS).

3.  Expanda el nombre del servidor y **Sitios**.

4.  Seleccione el sitio de la consola de Microsoft ATA y, en el panel **Acciones**, haga clic en **Enlaces**.

    ![Imagen de la acción de enlaces de la consola de ATA](media/ATA-console-change-IP-bindings.jpg)

5.  Seleccione **HTTP** y haga clic en **Editar** para seleccionar la nueva dirección IP. Haga lo mismo para **HTTPS** seleccionando la misma dirección IP.

    ![Imagen de la edición del enlace de sitio](media/ATA-change-console-IP.jpg)

6.  En el panel **Acción**, haga clic en **Reiniciar** en **Administrar sitio web**.

7.  Abra un símbolo del sistema de administrador y escriba los comandos siguientes para actualizar el controlador HTTP.SYS:

    -   Para agregar la nueva dirección IP: `netsh http add iplisten ipaddress=newipaddress`

    -   Para comprobar que se esté usando la nueva dirección: `netsh http show iplisten`

    -   Para eliminar la dirección IP antigua: `netsh http delete iplisten ipaddress=oldipaddress`

8.  Si la dirección URL de la consola de ATA sigue usando una dirección IP, actualice la dirección URL de la consola de ATA con la nueva dirección IP y descargue el paquete de instalación de puerta de enlace de ATA antes de implementar nuevas puertas de enlace de ATA.

9. Si la dirección URL de la consola de ATA es un FQDN, actualice el DNS con la nueva dirección IP del FQDN.

>[!div class="step-by-step"]
[« Certificado del Centro ATA](modifying-ata-config-centercert.md)
[Certificado de IIS »](modifying-ata-config-iiscert.md)


## Véase también
- [Trabajar con la consola de ATA](working-with-ata-console.md)
- [Instalación de ATA](install-ata.md)
- [¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


