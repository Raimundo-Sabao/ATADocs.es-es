---
# required metadata

title: Instalación de ATA de forma silenciosa | Microsoft Advanced Threat Analytics
description: Describe cómo realizar una instalación silenciosa de ATA.
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

# Instalación silenciosa de ATA
Este artículo proporciona instrucciones para instalar ATA de forma silenciosa.
## Requisitos previos

Microsoft ATA v1.6 requiere la instalación de Microsoft .NET Framework 4.6.1. 

Al instalar o actualizar ATA, .Net Framework 4.6.1 se instalará de forma automática como parte de la implementación de Microsoft ATA.

> [!Note] La instalación de .Net Framework 4.6.1 puede requerir que reinicie el servidor. Al instalar la puerta de enlace de ATA en controladores de dominio, considere la posibilidad de programar una ventana de mantenimiento de estos controladores de dominio.
Al usar el método de instalación silenciosa de ATA, el programa de instalación está configurado para reiniciar automáticamente el servidor al final de la instalación (si es necesario). Para evitar tener que reiniciar el servidor como parte de la instalación, use la marca `-NoRestart`. Cuando se use la marca `-NoRestart` será necesario reiniciar como parte de la instalación, el programa de instalación se pausará hasta que se reinicie el servidor. Para realizar un seguimiento de la implementación, supervise los registros del instalador de ATA que se encuentran en **%AppData%\Local\Temp**.


## Instalar el centro ATA

Use el siguiente comando para instalar el Centro ATA:

**Sintaxis**:

    “Microsoft ATA Center Setup.exe” [/quiet] [/NoRestart] [/Help] [--LicenseAccepted] [NetFrameworkCommandLineArguments=”/q”] [InstallationPath=“<InstallPath>”] [DatabaseDataPath= “<DBPath>”] [CenterIpAddress=<CenterIPAddress>] [CenterPort=<CenterPort>] [CenterCertificateThumbprint=“<CertThumbprint>”] 
    [ConsoleIpAddress=<ConsoleIPAddress>] [ConsoleCertificateThumbprint=”<CertThumbprint >”]
    
**Opciones de instalación**:

|Nombre|Sintaxis|¿Obligatorio para la instalación silenciosa?|Descripción|
|-------------|----------|---------|---------|
|Quiet|/quiet|Sí|Ejecuta el instalador sin mostrar ninguna UI y sin mensajes.|
|NoRestart|/norestart|No|Suprime los intentos de reinicio. De manera predeterminada, la UI le pedirá confirmación antes de reiniciar.|
|Ayuda|/help|No|Proporciona ayuda y una referencia rápida. Muestra el uso correcto del comando de instalación, incluida una lista de todas las opciones y comportamientos.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Sí|Especifica los parámetros para la instalación de .Net Framework. Debe establecerse para exigir la instalación silenciosa de .Net Framework.|
|LicenseAccepted|--LicenseAccepted|Sí|Indica que la licencia se ha leído y aprobado. Se debe establecer en una instalación silenciosa.|

**Parámetros de instalación**:

|Nombre|Sintaxis|¿Obligatorio para la instalación silenciosa?|Descripción|
|-------------|----------|---------|---------|
|InstallationPath|InstallationPath=“<InstallPath>”|No|Establece la ruta de acceso para la instalación de archivos binarios de ATA. Ruta de acceso predeterminada: C:\Archivos de programa\Microsoft Advanced Threat Analytics\Center|
|DatabaseDataPath|DatabaseDataPath= “<DBPath>”|No|Establece la ruta de acceso de la carpeta de datos de la base de datos de ATA. Ruta de acceso predeterminada: C:\Archivos de programa\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data|
|CenterIpAddress|CenterIpAddress=<CenterIPAddress>|Sí|Establece la dirección IP del servicio del Centro ATA|
|CenterPort|CenterPort=<CenterPort>|Sí|Establece el puerto de red del servicio del Centro ATA|
|CenterCertificateThumbprint|CenterCertificateThumbprint=“<CertThumbprint>”|No|Establece la huella digital del certificado para el servicio del Centro ATA. Este certificado se usa para asegurar la comunicación entre el Centro ATA y la puerta de enlace de ATA. Si no se establece, la instalación generará un certificado autofirmado.|
|ConsoleIpAddress|ConsoleIpAddress=<ConsoleIPAddress>|Sí|Establece la dirección IP de la consola de ATA.|
|ConsoleCertificateThumbprint|ConsoleCertificateThumbprint=”<CertThumbprint >”|No|Especifica la huella digital del certificado para la consola de ATA. Este certificado se usa para validar la identidad del sitio web de la consola de ATA. Si no se especifica, la instalación generará un certificado autofirmado|

**Ejemplos**:
Para instalar el Centro ATA con rutas de instalación predeterminadas y una dirección IP única:

    “Microsoft ATA Center Setup.exe” /quiet --LicenseAccepted NetFrameworkCommandLineArguments="/q" CenterIpAddress=192.168.0.10
    CenterPort=444 ConsoleIpAddress=192.168.0.10

Para instalar el Centro ATA con rutas de instalación predeterminadas, dos direcciones IP y huellas digitales de certificados definidas por el usuario:

    “Microsoft ATA Center Setup.exe” /quiet --LicenseAccepted NetFrameworkCommandLineArguments ="/q" CenterIpAddress=192.168.0.10 CenterPort=443 CenterCertificateThumbprint= ‎"1E2079739F624148ABDF502BF9C799FCB8C7212F”
    ConsoleIpAddress=192.168.0.11  ConsoleCertificateThumbprint=”G9530253C976BFA9342FD1A716C0EC94207BFD5A”

## Actualizar el centro ATA

Use el siguiente comando para actualizar el Centro ATA:

**Sintaxis**:

    Microsoft ATA Center Setup.exe” [/quiet] [-NoRestart] /Help] [NetFrameworkCommandLineArguments=”/q”]


**Opciones de instalación**:

|Nombre|Sintaxis|¿Obligatorio para la instalación silenciosa?|Descripción|
|-------------|----------|---------|---------|
|Quiet|/quiet|Sí|Ejecuta el instalador sin mostrar ninguna UI y sin mensajes.|
|NoRestart|/norestart|No|Suprime los intentos de reinicio. De manera predeterminada, la UI le pedirá confirmación antes de reiniciar.|
|Ayuda|/help|No|Proporciona ayuda y una referencia rápida. Muestra el uso correcto del comando de instalación, incluida una lista de todas las opciones y comportamientos.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Sí|Especifica los parámetros para la instalación de .Net Framework. Debe establecerse para exigir la instalación silenciosa de .Net Framework.|


Al actualizar ATA, el programa de instalación detecta automáticamente que ATA ya está instalado en el servidor y no se requiere ninguna opción de instalación de actualización.

**Ejemplos**:
Para actualizar el Centro ATA de forma silenciosa. En entornos grandes, la actualización del Centro ATA puede tardar un tiempo en completarse. Supervise los registros de ATA para realizar un seguimiento del progreso de la actualización.

        “Microsoft ATA Center Setup.exe” /quiet NetFrameworkCommandLineArguments="/q"

## Desinstalar el Centro ATA de forma silenciosa

Use el siguiente comando para realizar una desinstalación silenciosa del Centro ATA:
**Sintaxis**:

    Microsoft ATA Center Setup.exe [/quiet] [/Uninstall] [/NoRestart] [/Help]
     [--DeleteExistingDatabaseData]

**Opciones de instalación**:

|Nombre|Sintaxis|¿Obligatorio para la desinstalación silenciosa?|Descripción|
|-------------|----------|---------|---------|
|Quiet|/quiet|Sí|Ejecuta el desinstalador sin mostrar ninguna UI y sin mensajes.|
|Desinstalar|/uninstall|Sí|Ejecuta la desinstalación silenciosa del Centro ATA del servidor.|
|NoRestart|/norestart|No|Suprime los intentos de reinicio. De manera predeterminada, la UI le pedirá confirmación antes de reiniciar.|
|Ayuda|/help|No|Proporciona ayuda y una referencia rápida. Muestra el uso correcto del comando de instalación, incluida una lista de todas las opciones y comportamientos.|

**Parámetros de instalación**:

|Nombre|Sintaxis|¿Obligatorio para la desinstalación silenciosa?|Descripción|
|-------------|----------|---------|---------|
|DeleteExistingDatabaseData|DeleteExistingDatabaseData|No|Elimina todos los archivos de la base de datos existente.|

**Ejemplos**:
Para desinstalar de forma silenciosa el Centro ATA del servidor y quitar todos los datos de las bases de datos existentes:


    “Microsoft ATA Center Setup.exe” /quiet /uninstall --DeleteExistingDatabaseData

## Instalación silenciosa de la puerta de enlace de ATA
Use el siguiente comando para instalar de forma silenciosa la puerta de enlace de ATA:

**Sintaxis**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/NoRestart] [/Help] [NetFrameworkCommandLineArguments ="/q"] 
    [GatewayCertificateThumbprint=”<CertThumbprint >”] [ConsoleAccountName=”<AccountName>”] 
    [ConsoleAccountPassword=”<AccountPassword>”]

**Opciones de instalación**:

|Nombre|Sintaxis|¿Obligatorio para la instalación silenciosa?|Descripción|
|-------------|----------|---------|---------|
|Quiet|/quiet|Sí|Ejecuta el instalador sin mostrar ninguna UI y sin mensajes.|
|NoRestart|/norestart|No|Suprime los intentos de reinicio. De manera predeterminada, la UI le pedirá confirmación antes de reiniciar.|
|Ayuda|/help|No|Proporciona ayuda y una referencia rápida. Muestra el uso correcto del comando de instalación, incluida una lista de todas las opciones y comportamientos.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Sí|Especifica los parámetros para la instalación de .Net Framework. Debe establecerse para exigir la instalación silenciosa de .Net Framework.|
|LicenseAccepted|--LicenseAccepted|Sí|Indica que la licencia se ha leído y aprobado. Se debe establecer en una instalación silenciosa.|

**Parámetros de instalación**:

|Nombre|Sintaxis|¿Obligatorio para la instalación silenciosa?|Descripción|
|-------------|----------|---------|---------|
|GatewayCertificateThumbprint|GatewayCertificateThumbprint=”<CertThumbprint >”|No|Establece la huella digital del certificado para el servicio del Centro ATA. Este certificado se usa para asegurar la comunicación entre el Centro ATA y la puerta de enlace de ATA. Si no se establece, la instalación generará un certificado autofirmado.|
|ConsoleAccountName|ConsoleAccountName=”<AccountName>”|Sí|Establece el nombre de la cuenta de usuario (user@domain.com) que se usa para registrar la puerta de enlace de ATA con el Centro ATA.|
|ConsoleAccountPassword|ConsoleAccountPassword=”<AccountPassword>”|Sí|Establece la contraseña de la cuenta de usuario (user@domain.com) que se usa para registrar la puerta de enlace de ATA con el Centro ATA.|

**Ejemplos**:
Para instalar la puerta de enlace de ATA de forma silenciosa y registrarla con el Centro ATA con las credenciales especificadas:

    “Microsoft ATA Gateway Setup.exe” /quiet NetFrameworkCommandLineArguments="/q" 
    ConsoleAccountName=”user@contoso.com” ConsoleAccountPassword=“userpwd”
    

## Actualizar la puerta de enlace de ATA

Use el siguiente comando para actualizar de forma silenciosa la puerta de enlace de ATA:

**Sintaxis**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/NoRestart] /Help] [NetFrameworkCommandLineArguments="/q"]


**Opciones de instalación**:

|Nombre|Sintaxis|¿Obligatorio para la instalación silenciosa?|Descripción|
|-------------|----------|---------|---------|
|Quiet|/quiet|Sí|Ejecuta el instalador sin mostrar ninguna UI y sin mensajes.|
|NoRestart|/norestart|No|Suprime los intentos de reinicio. De manera predeterminada, la UI le pedirá confirmación antes de reiniciar.|
|Ayuda|/help|No|Proporciona ayuda y una referencia rápida. Muestra el uso correcto del comando de instalación, incluida una lista de todas las opciones y comportamientos.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Sí|Especifica los parámetros para la instalación de .Net Framework. Debe establecerse para exigir la instalación silenciosa de .Net Framework.|


**Ejemplos**:
Para actualizar la puerta de enlace de ATA de forma silenciosa:

        Microsoft ATA Gateway Setup.exe /quiet NetFrameworkCommandLineArguments="/q"

## Desinstalar la puerta de enlace de ATA de forma silenciosa

Use el siguiente comando para realizar una desinstalación silenciosa de la puerta de enlace de ATA:
**Sintaxis**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/Uninstall] [/NoRestart] [/Help]
    
**Opciones de instalación**:

|Nombre|Sintaxis|¿Obligatorio para la desinstalación silenciosa?|Descripción|
|-------------|----------|---------|---------|
|Quiet|/quiet|Sí|Ejecuta el desinstalador sin mostrar ninguna UI y sin mensajes.|
|Desinstalar|/uninstall|Sí|Ejecuta la desinstalación silenciosa de la puerta de enlace de ATA del servidor.|
|NoRestart|/norestart|No|Suprime los intentos de reinicio. De manera predeterminada, la UI le pedirá confirmación antes de reiniciar.|
|Ayuda|/help|No|Proporciona ayuda y una referencia rápida. Muestra el uso correcto del comando de instalación, incluida una lista de todas las opciones y comportamientos.|

**Ejemplos**:
Para desinstalar de forma silenciosa la puerta de enlace de ATA del servidor:


    Microsoft ATA Gateway Setup.exe /quiet /uninstall
    









## Véase también

- [¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Configurar la recopilación de eventos](configure-event-collection.md)
- [Requisitos previos de ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)

<!--HONumber=May16_HO1-->


