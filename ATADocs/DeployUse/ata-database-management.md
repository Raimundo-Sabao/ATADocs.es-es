---
# required metadata

title: Administración de la base de datos de ATA | Microsoft Advanced Threat Analytics
description: Procedimientos para mover o restaurar la base de datos ATA o hacer una copia de seguridad de esta.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Administración de la base de datos de ATA
Si necesita mover o restaurar la base de datos de ATA, o bien hacer una copia de seguridad de esta, use los siguientes procedimientos para trabajar con MongoDB.

## Copia de seguridad de la base de datos de ATA
Vea la [documentación de MongoDB pertinente](http://docs.mongodb.org/manual/administration/backup/)..

## Restaurar la base de datos de ATA
Vea la [documentación de MongoDB pertinente](http://docs.mongodb.org/manual/administration/backup/)..

## Mover la base de datos de ATA a otra unidad

1.  Detenga el servicio **Microsoft Advanced Threat Analytics Center**.

2.  Detenga el servicio **MongoDB**.

3.  Abra el archivo de configuración de Mongo, que se encuentra de forma predeterminada en C:\Archivos de programa\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongod.cfg.

    Buscar el parámetro `storage: dbPath`

4.  Mueva la carpeta que aparece en el parámetro `dbPath` a la nueva ubicación.

5.  Cambie el parámetro `dbPath` del archivo de configuración de Mongo por la nueva ruta de acceso de carpeta. Después, guarde y cierre el archivo.

    ![Imagen de modificación de la configuración de MongoDB](media/ATA-mongoDB-moveDB.png)

6.  Inicie el servicio **MongoDB**.

7.  Abra un símbolo del sistema y ejecute el shell de Mongo; para ello, ejecute `mongo.exe ATA` .

    El archivo mongo.exe se encuentra de forma predeterminada en C:\Archivos de programa\Microsoft Advanced Threat Analytics\Center\MongoDB\bin.

8.  Ejecute el siguiente comando: `db.SystemProfiles.update( {_t: "CenterSystemProfile"} , {$set:{"Configuration.CenterDatabaseClientConfiguration.DataPath" : "<New DB Location>"}}) Instead of <New DB Location>` donde &lt;New DB Location&gt; es la nueva ruta de acceso de carpeta.

9.  Actualice HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Center\DatabaseDataPath a la nueva ruta de acceso de carpeta.

9. Inicie el servicio **Microsoft Advanced Threat Analytics Center**.

## Véase también
- [Arquitectura de ATA](/advanced-threat-analytics/plan-design/ata-architecture)
- [Requisitos previos de ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)



<!--HONumber=May16_HO1-->


