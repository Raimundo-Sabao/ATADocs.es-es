---
# required metadata

title: "Cambiar la configuración de ATA: contraseña de conectividad de dominio | Microsoft Advanced Threat Analytics"
description: "Describe cómo cambiar la contraseña de conectividad de dominio en la puerta de enlace de ATA."
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 4a25561b-a5ed-44aa-9b72-366976b3c72a

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Cambiar la configuración de ATA: contraseña de conectividad de dominio

>[!div class="step-by-step"]
[« Certificado de IIS](modifying-ata-config-iiscert.md)


## Cambiar la contraseña de conectividad del dominio
Si modifica la contraseña de conectividad de dominio, asegúrese de que la contraseña escrita es correcta. Si no lo es, el servicio de puerta de enlace de ATA dejará de ejecutarse en las puertas de enlace de ATA.

Si sospecha que esto es lo que ha ocurrido, en la puerta de enlace de ATA, busque lo siguiente en el archivo Microsoft.Tri.Gateway-Errors.log:
`The supplied credential is invalid.`

Para corregirlo, siga este procedimiento para actualizar la contraseña de conectividad de dominio en la puerta de enlace de ATA:

1.  Abra la consola de ATA en la puerta de enlace de ATA.

2.  Seleccione la opción de configuración en la barra de herramientas y, luego, **Configuración**.

    ![Icono de los valores de configuración de ATA](media/ATA-config-icon.JPG)

3.  Seleccione **General**.

    ![Imagen de cambio de contraseña de la puerta de enlace de ATA](media/ATA-GW-change-DC-password.JPG)

4.  En **General**, cambie la contraseña.

5.  Haga clic en **Guardar**..

6.  Después de cambiar la contraseña, compruebe manualmente que el servicio de puerta de enlace de ATA se está ejecutando en los servidores de puerta de enlace de ATA.

>[!div class="step-by-step"]
[« Certificado de IIS](modifying-ata-config-iiscert.md)

## Véase también
- [Trabajar con la consola de ATA](working-with-ata-console.md)
- [Instalación de ATA](install-ata.md)
- [¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


