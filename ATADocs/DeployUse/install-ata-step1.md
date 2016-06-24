---
# required metadata

title: "Instalación de ATA: paso 1 | Microsoft Advanced Threat Analytics"
description: "El primer paso para instalar ATA consiste en descargar e instalar el Centro ATA en el servidor seleccionado."
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Instalación de ATA: paso 1

>[!div class="step-by-step"]

[Paso 2 »](install-ata-step2.md)

Este procedimiento de instalación proporciona instrucciones para realizar una instalación nueva de ATA 1.6. Para obtener información sobre la actualización de una implementación existente de ATA desde una versión anterior, consulte [la guía de migración de ATA para la versión 1.6](/advanced-threat-analytics/understand-explore/ata-update-1.6-migration-guide).

> [!IMPORTANT] Instale KB2934520 en el servidor del Centro ATA y en los servidores de puerta de enlace de ATA antes de comenzar la instalación. En caso contrario, la instalación de ATA instalará esta actualización y requerirá un reinicio durante la instalación de ATA.

## Paso 1. Descargar e instalar el Centro ATA
Después de comprobar que el servidor cumple los requisitos, puede continuar con la instalación del Centro ATA.

Lleve a cabo los pasos siguientes en el servidor del Centro ATA.

1.  Descargue ATA desde [Microsoft Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/default.aspx), [TechNet Evaluation Center](http://www.microsoft.com/en-us/evalcenter/) o [MSDN](https://msdn.microsoft.com/en-us/subscriptions/downloads).

2.  Inicie sesión en el equipo en el que va a instalar el centro ATA como usuario miembro del grupo de administradores locales.

3.  Ejecute **Microsoft ATA Center Setup.EXE** y siga los pasos del Asistente para instalación.

4.  Si Microsoft .Net Framework no está instalado, se le pedirá que lo instale al comenzar la instalación. Es posible que se le pida reiniciar después de la instalación de .NET Framework.
5.  En la **página principal**, seleccione el idioma que se usará en las pantallas de instalación de ATA y haga clic en **Siguiente**.

6.  Lea los Términos de licencia del software de Microsoft y, si los acepta, haga clic en la casilla y luego en **Siguiente**.

7.  Se recomienda establecer ATA para actualizarse automáticamente. Si Windows no está configurado para hacer esto en el equipo, aparecerá la pantalla **Usar Microsoft Update para mantener el equipo seguro y actualizado**. 
    ![Imagen de mantenimiento de ATA al día](media/ata_ms_update.png)

8. Seleccione **Usar Microsoft Update al buscar actualizaciones (recomendado)**. Esto ajustará la configuración de Windows para habilitar las actualizaciones de otros productos de Microsoft (incluido ATA), como se ve aquí. 
    ![Imagen de actualización automática de Windows](media/ata_installupdatesautomatically.png)

8.  En la página **Configuración del centro ATA**, escriba la siguiente información en función del entorno:

    |Campo|Descripción|Comentarios|
    |---------|---------------|------------|
    |Ruta de instalación|Esta es la ubicación donde se instalará el Centro ATA. De forma predeterminada es %programfiles%\Microsoft Advanced Threat Analytics\Center|Deje el valor predeterminado.|
    |Ruta de acceso a datos de la base de datos|Esta es la ubicación donde se encontrarán los archivos de la base de datos MongoDB. De forma predeterminada es %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data|Cambie la ubicación a un lugar donde haya espacio suficiente para crecer en función de su tamaño. **Nota:** <ul><li>En entornos de producción, debe usar una unidad que tenga espacio suficiente en función de la planeación de la capacidad.</li><li>En el caso de implementaciones grandes, la base de datos debe estar en un disco físico independiente.</li></ul>Consulte [ATA capacity planning (Planificación de la capacidad de ATA)](/advanced-threat-analytics/plan-design/ata-capacity-planning) para obtener información sobre tamaños.|
    |Dirección IP del servicio del Centro ATA: puerto|Se trata de la dirección IP en la que el servicio del Centro ATA escuchará la comunicación de las puertas de enlace de ATA.<br /><br />**Puerto predeterminado:** 443.|Haga clic en la flecha abajo para seleccionar la dirección IP que va a usar el servicio del Centro ATA.<br /><br />La dirección IP y el puerto del servicio del Centro ATA no pueden ser iguales a la dirección IP y el puerto de la consola de ATA. Asegúrese de cambiar el puerto de la consola de ATA.|
    |Certificado SSL del servicio del Centro ATA|Este es el certificado que usará el servicio del Centro ATA.|Haga clic en el icono de llave para seleccionar un certificado instalado o active el certificado autofirmado al realizar la implementación en un entorno de laboratorio.|
    |Dirección IP de la consola de ATA|Se trata de la dirección IP que IIS usará para la consola de ATA.|Haga clic en la flecha abajo para seleccionar la dirección IP que va a usar la consola de ATA. **Nota:** Apunte esta dirección IP para que sea más fácil acceder a la consola de ATA desde la puerta de enlace de ATA.|
    |Certificado SSL de la consola de ATA|Este es el certificado que va a usar IIS.|Haga clic en el icono de llave para seleccionar un certificado instalado o active el certificado autofirmado al realizar la implementación en un entorno de laboratorio.|

    ![Imagen de la configuración del Centro ATA](media/ATA-Center-Configuration.JPG)

10.  Haga clic en **Instalar** para instalar el centro ATA y sus componentes.
    Durante la instalación del Centro ATA se instalan y se configuran los siguientes componentes:

    -   Internet Information Services (IIS)

    -   Servicio del Centro ATA y sitio de IIS de la consola de ATA

    -   MongoDB

    -   Conjunto de recopilación de datos del Monitor de rendimiento personalizado

    -   Certificados autofirmados (si se selecciona durante la instalación)

11.  Cuando finalice la instalación, haga clic en **Iniciar** para conectarse a la consola de ATA.
En este punto aparecerá automáticamente la página de configuración **General** para continuar con la configuración y la implementación de las puertas de enlace de ATA.
Dado que está iniciando sesión en el sitio mediante una dirección IP, recibirá una advertencia relacionada con el certificado. Esto es normal, así que debe hacer clic en **Pasar a este sitio web**.

### Validar la instalación

1.  Compruebe que el servicio denominado **Microsoft Advanced Threat Analytics Center** se esté ejecutando.
2.  En el escritorio, haga clic en el acceso directo **Microsoft Advanced Threat Analytics** para conectarse a la consola de ATA. Inicie sesión con las mismas credenciales de usuario que usó para instalar el Centro ATA.



>[!div class="step-by-step"] [« Previo a la instalación](preinstall-ata.md)
[Paso 2 »](install-ata-step2.md)

## Véase también

- [¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Configurar la recopilación de eventos](configure-event-collection.md)
- [Requisitos previos de ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=May16_HO4-->


