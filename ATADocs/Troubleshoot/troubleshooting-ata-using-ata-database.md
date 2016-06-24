---
# required metadata

title: Solución de problemas de ATA con la base de datos de ATA | Microsoft Advanced Threat Analytics
description: Describe cómo se puede usar la base de datos de ATA para ayudar a solucionar problemas 
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Solución de problemas de ATA con la base de datos de ATA
ATA usa MongoDB como base de datos.
Puede interactuar con la base de datos mediante la línea de comandos predeterminada o mediante una herramienta de interfaz de usuario para realizar tareas avanzadas y solucionar problemas.

## Interactuar con la base de datos
La manera predeterminada y más sencilla de consultar la base de datos es mediante el shell de Mongo:

1.  Abra una ventana de línea de comandos y cambie la ruta de acceso a la carpeta bin de MongoDB. La ruta de acceso predeterminada es: **C:\Archivos de programa\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**.

2.  Ejecute `mongo.exe ATA`. Asegúrese de que escribe ATA con todas las letras en mayúscula.

|Cómo…|Sintaxis|Notas|
|-------------|----------|---------|
|Buscar colecciones en la base de datos.|`show collections`|Resulta útil como prueba de un extremo a otro para comprobar que el tráfico se escribe en la base de datos y que ATA recibe el evento 4776.|
|Obtener los detalles de un usuario, equipo o grupo (UniqueEntity), como el identificador de usuario.|`db.UniqueEntity.find({SearchNames: "<name of entity in lower case>"})`||
|Buscar el tráfico de autenticación Kerberos que se origina en un equipo específico un día concreto.|`db.KerberosAs_<datetime>.find({SourceComputerId: "<Id of the source computer>"})`|Para obtener el &lt;identificador del equipo de origen&gt; puede consultar las colecciones UniqueEntity, tal como se muestra en el ejemplo.<br /><br />Cada tipo de actividad de red, por ejemplo, las autenticaciones Kerberos, tiene su propia colección por fecha UTC.|
|Buscar el tráfico NTLM procedente de un equipo específico relacionado con una cuenta específica en un día concreto.|`db.Ntlm_<datetime>.find({SourceComputerId: "<Id of the source computer>", SourceAccountId: "<Id of the account>"})`|Para obtener el &lt;identificador del equipo de origen&gt; y el &lt;identificador de la cuenta&gt; puede consultar las colecciones UniqueEntity, tal como se muestra en el ejemplo.<br /><br />Cada tipo de actividad de red, por ejemplo, las autenticaciones NTLM, tiene su propia colección por fecha UTC.|
|Buscar propiedades avanzadas, como las fechas activas de una cuenta. |`db.UniqueEntityProfile.find({UniqueEntityId: "<Id of the account>")`|Para obtener el &lt;identificador de la cuenta&gt; puede consultar las colecciones UniqueEntity, tal como se muestra en el ejemplo.<br>El nombre de propiedad que muestra las fechas en las que ha estado activa la cuenta se denomina "ActiveDates". <br>
Por ejemplo, podría interesarle saber si una cuenta tiene al menos 21 días de actividad para poder ejecutar en ella el algoritmo de aprendizaje automático de comportamiento anómalo.|
|Realizar cambios de configuración avanzada. En este ejemplo se cambia a 10 000 el tamaño de la cola de envío de todas las puertas de enlace de ATA.|`db.SystemProfile.update( {_t: "GatewaySystemProfile"} ,`<br>`{$set:{"Configuration.EntitySenderConfiguration.EntityBatchBlockMaxSize" : "10000"}})`|`|

En el ejemplo siguiente se ofrece código de ejemplo con la sintaxis proporcionada anteriormente. Si está investigando una actividad sospechosa que se produjo el 20/10/2015 y quiere obtener más información sobre las actividades NTLM que "John Doe" realizó ese día:<br /><br />En primer lugar, busque el identificador de "John Doe"

`db.UniqueEntity.find({Name: "John Doe"})`<br>Tome nota de su identificador, indicado por el valor de "`_id`". En nuestro ejemplo, supongamos que el identificador es "`123bdd24-b269-h6e1-9c72-7737as875351`".<br>A continuación, busque la colección con la fecha más cercana que sea anterior a la fecha que está buscando, en nuestro ejemplo 20/10/2015.<br>Después, busque las actividades NTLM de la cuenta de John Doe: 

`db.Ntlms_<closest date>.find({SourceAccountId: "123bdd24-b269-h6e1-9c72-7737as875351"})`
## Archivo de configuración de ATA
La configuración de ATA se almacena en la colección "SystemProfile" de la base de datos.
El servicio del Centro ATA realiza una copia de seguridad de esta colección cada hora en un archivo denominado "SystemProfile.json". Dicho archivo se encuentra en una subcarpeta denominada "Backup". En la ubicación de la instalación de ATA predeterminada, se encuentra aquí:  **C:\Archivos de programa\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile.json**. 

**Nota**: Se recomienda realizar una copia de seguridad de este archivo en algún lugar cuando vaya a realizar cambios importantes en ATA.

Puede restaurar toda la configuración si ejecuta el comando siguiente:

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## Véase también
- [Requisitos previos de ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Planeamiento de la capacidad de ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Configurar la recopilación de eventos](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Configurar el reenvío de eventos de Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


