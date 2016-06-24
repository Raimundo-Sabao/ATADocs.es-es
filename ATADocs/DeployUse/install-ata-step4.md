---
# required metadata

title: "Instalación de ATA: paso 4 | Microsoft Advanced Threat Analytics"
description: "El paso cuatro de la instalación de ATA le ayudará a instalar la puerta de enlace de ATA."
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 6bbc50c3-bfa8-41db-a2f9-56eed68ef5d2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Instalación de ATA: paso 4

>[!div class="step-by-step"]
[« Paso 3](install-ata-step3.md)
[Paso 5 »](install-ata-step5.md)

## Paso 4. Instalar la puerta de enlace de ATA

Antes de instalar la puerta de enlace de ATA en un servidor dedicado, compruebe que la creación de reflejo del puerto está correctamente configurada y que la puerta de enlace de ATA puede ver el tráfico hacia y desde los controladores de dominio. Consulte [Validate port mirroring (Validar la creación de reflejo del puerto)](validate-port-mirroring.md) para obtener más información.


> [!IMPORTANT]
> Asegúrese de que se ha instalado [KB2919355](http://support.microsoft.com/kb/2919355/).  Ejecute el siguiente cmdlet de PowerShell para comprobar si se ha instalado la revisión:
>
> `Get-HotFix -Id kb2919355`

Lleve a cabo los pasos siguientes en el servidor de puerta de enlace de ATA.

1.  Extraiga los archivos del archivo ZIP. 
> [!NOTE] Se producirá un error al instalar directamente desde el archivo zip.

2.  Desde un símbolo del sistema con privilegios elevados, ejecute **Microsoft ATA Gateway Setup.exe** y siga los pasos del Asistente para instalación.

3.  En la **página principal**, seleccione el idioma y haga clic en **Siguiente**.

4.  En **Configuración de la puerta de enlace de ATA**, escriba la siguiente información en función de su entorno:

    ![Imagen de la configuración de la puerta de enlace de ATA](media/ATA-Gateway-Configuration.JPG)

    |Campo|Descripción|Comentarios|
    |---------|---------------|------------|
    |Ruta de instalación|Esta es la ubicación donde se instalará la puerta de enlace de ATA. De forma predeterminada es %programfiles%\Microsoft Advanced Threat Analytics\Gateway|Deje el valor predeterminado.|
    |Certificado SSL de servicio de la puerta de enlace de ATA|Este es el certificado que usará la puerta de enlace de ATA.|Use un certificado autofirmado solamente para entornos de laboratorio.|
    |Registro de la puerta de enlace de ATA|Escriba el nombre de usuario y la contraseña del administrador de ATA.|Para que la puerta de enlace de ATA se registre en el Centro ATA, escriba el nombre de usuario y la contraseña del usuario que instaló el Centro ATA. Este usuario debe ser miembro de uno de los siguientes grupos locales en el Centro ATA.<br /><br />- Administradores.<br />- Administradores de Microsoft Advanced Threat Analytics. **Nota:** Estas credenciales solo se usan para el registro y no se almacenan en ATA.|
    Los siguientes componentes se instalan y se configuran durante la instalación de la puerta de enlace de ATA:

    -   KB 3047154

        > [!IMPORTANT]
        > -   No instale KB 3047154 en un host de virtualización (el host que está ejecutando la virtualización, es correcto ejecutarlo en una máquina virtual). Esto puede hacer que la creación de reflejo del puerto deje de funcionar correctamente. 
        > -   No instale el Analizador de mensajes, Wireshark u otro software de captura de red en la puerta de enlace de ATA. Si necesita capturar el tráfico de red, instale y use Microsoft Network Monitor 3.4.

    -   Servicio de puerta de enlace de ATA

    -   Microsoft Visual C++ 2013 Redistributable

    -   Conjunto de recopilación de datos del Monitor de rendimiento personalizado

5.  Una vez finalizada la instalación, en el caso de la puerta de enlace de ATA, haga clic en **Iniciar** para abrir el explorador e inicie sesión en la consola de ATA, mientras que en el caso de la puerta de enlace ligera de ATA, haga clic en **Finalizar**.


>[!div class="step-by-step"]
[« Paso 3](install-ata-step3.md)
[Paso 5 »](install-ata-step5.md)

## Véase también

- [¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Configurar la recopilación de eventos](configure-event-collection.md)
- [Requisitos previos de ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=May16_HO1-->


