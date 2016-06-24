---
# required metadata

title: Novedades de ATA versión 1.6 | Microsoft Advanced Threat Analytics
description: Se enumeran las novedades de ATA versión 1.6 junto con los problemas conocidos
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: a0d64aff-ca9e-4300-b3f8-eb3c8b8ae045

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Novedades de ATA versión 1.6
En estas notas de la versión encontrará información sobre los problemas conocidos de esta versión de Advanced Threat Analytics.

## ¿Cuáles son las novedades de la actualización de ATA 1.6?
La actualización a ATA 1.6 ofrece mejoras en las siguientes áreas:

-   Nuevas detecciones

-   Mejoras en las detecciones existentes

-   La puerta de enlace ligera de ATA

-   Actualizaciones automáticas

-   Rendimiento mejorado del centro ATA

-   Requisitos de almacenamiento inferiores

-   Compatibilidad con IBM QRadar

### Nuevas detecciones


- **Solicitud malintencionada de información privada de protección de datos** La API de protección de datos (DPAPI) es un servicio de protección de datos basado en contraseña. Hay varias aplicaciones que almacenan secretos del usuario, como contraseñas de sitios web y credenciales de recurso compartido de archivos, que usan este servicio de protección. Para admitir escenarios de pérdida de contraseña, los usuarios pueden descifrar los datos protegidos con una clave de recuperación que no implique su contraseña. En un entorno de dominio, los atacantes pueden robar la clave de recuperación de forma remota y usarla para descifrar los datos protegidos en todos los equipos unidos al dominio.


- **Enumeración de sesiones de red** El reconocimiento es una fase clave de la cadena de destrucción de ataques avanzados. Los controladores de dominio actúan como servidores de archivos para la distribución del objeto de directiva de grupo mediante el protocolo de bloque de mensajes del servidor (SMB). Como parte de la fase de reconocimiento, los atacantes pueden consultar al controlador de dominio para ver todas las sesiones activas de SMB en el servidor, lo que les permite obtener acceso a todos los usuarios y las direcciones IP asociados a esas sesiones de SMB. Los atacantes pueden usar la enumeración de sesiones de SMB para dirigirse a cuentas importantes, lo que les ayuda a moverse lateralmente por la red.


- **Solicitudes malintencionadas de replicación** En entornos de Active Directory, la replicación entre controladores de dominio se produce con regularidad. Un atacante puede suplantar la identidad de la solicitud de replicación de Active Directory (a veces suplantando como un controlador de dominio), lo que le permite recuperar los datos almacenados en Active Directory, incluidos los hash de contraseña, sin usar técnicas más intrusivas, como las instantáneas de volumen.


- **Detección de vulnerabilidad de seguridad MS11-013** Hay una vulnerabilidad de elevación de privilegios en Kerberos que permite que se falsifiquen ciertos aspectos de un vale de servicio Kerberos. Un usuario o un atacante malintencionado que aprovechara esta vulnerabilidad correctamente podría obtener un token con privilegios elevados en el controlador de dominio.


- **Implementación de protocolos inusual** Las solicitudes de autenticación (Kerberos o NTLM) normalmente se realizan mediante un conjunto estándar de métodos y protocolos. Sin embargo, para autenticar correctamente, la solicitud solo tiene que cumplir un conjunto específico de requisitos. Los atacantes podrían implementar estos protocolos con pequeñas desviaciones de la implementación estándar en el entorno. Estas desviaciones podrían indicar la presencia de un atacante que intentara ejecutar ataques como pass-the-hash, fuerza bruta y otros.


### Mejoras en las detecciones existentes
ATA 1.6 incluye una lógica de detección mejorada que reduce los escenarios de falsos positivos y falsos negativos en detecciones existentes como golden ticket, Honey Token, fuerza bruta y ejecución remota.

### La puerta de enlace ligera de ATA
Esta versión de ATA presenta una nueva opción de implementación para la puerta de enlace de ATA que permite instalar una puerta de enlace de ATA directamente en el controlador de dominio. Esta opción de implementación elimina la funcionalidad no crítica de la puerta de enlace de ATA y presenta la administración dinámica de recursos basada en los recursos disponibles en el controlador de dominio, lo que garantiza que las operaciones existentes del controlador de dominio no se vean afectadas. La puerta de enlace ligera de ATA reduce el costo de implementación de ATA. Al mismo tiempo facilita la implementación en sucursales en donde la capacidad de recursos de hardware es limitada o no hay posibilidad de configurar la compatibilidad con la creación de reflejo del puerto.
Para obtener más información sobre la puerta de enlace ligera de ATA, consulte [ATA Architecture (Arquitectura de ATA)](/advanced-threat-analytics/plan-design/ata-architecture#ata-gateway-and-ata-lightweight-gateway)

Para obtener más información sobre las consideraciones de implementación y la elección del tipo correcto de puerta de enlace, consulte [ATA capacity planning (Planeación de la capacidad de ATA)](/advanced-threat-analytics/plan-design/ata-capacity-planning#choosing-the-right-gateway-type-for-your-deployment)


### Actualizaciones automáticas
A partir de la versión 1.6, es posible actualizar el centro ATA con Microsoft Update. Además, las puertas de enlace de ATA ahora se pueden actualizar automáticamente mediante el canal de comunicación estándar con el centro ATA.
### Rendimiento mejorado del centro ATA
Con esta versión, una carga de base de datos más ligera y una forma más eficaz de ejecutar todas las detecciones permiten supervisar muchos más controladores de dominio con un solo centro ATA.

### Requisitos de almacenamiento inferiores
ATA 1.6 necesita mucho menos espacio de almacenamiento para ejecutar la base de datos de ATA, ya que ahora solo necesita el 20% del espacio de almacenamiento usado en versiones anteriores.

### Compatibilidad con IBM QRadar
ATA ahora puede recibir eventos de la solución SIEM QRadar de IBM, además de las soluciones SIEM admitidas con anterioridad.

## Problemas conocidos
Esta versión presenta los siguientes problemas conocidos.

### No se reconoce la nueva ruta de acceso en las bases de datos movidas de forma manual

En las implementaciones en que se mueve manualmente la ruta de acceso de la base de datos, la implementación de ATA no usa la nueva ruta de acceso de la base de datos para la actualización. Esto puede originar los problemas siguientes:


- ATA puede usar todo el espacio libre en la unidad de sistema del centro ATA, sin eliminar de forma circular las actividades de red antiguas.


- La actualización de ATA a la versión 1.6 puede producir un error en las comprobaciones de preparación previas a la actualización, como se muestra en la siguiente imagen.
    ![Error de comprobación de preparación](media/ata_failed_readinesschecks.png)
    >[!Important]
Antes de actualizar ATA a la versión 1.6, actualice la siguiente clave del Registro con la ruta de acceso correcta de la base de datos:  `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Center\DatabaseDataPath`

### Error de migración al actualizar desde ATA 1.5
Al actualizar a ATA 1.6, el proceso de actualización puede producir un error con el código siguiente:

![Error de actualización de ATA a 1.6](http://i.imgur.com/QrLSApr.png) Si aparece este error, revise el registro de implementación en: **C:\Users\<Usuario>\AppData\Local\Temp** y busque la siguiente excepción:

    System.Reflection.TargetInvocationException: Exception has been thrown by the target of an invocation. ---> MongoDB.Driver.MongoWriteException: A write operation resulted in an error. E11000 duplicate key error index: ATA.UniqueEntityProfile.$_id_ dup key: { : "<guid>" } ---> MongoDB.Driver.MongoBulkWriteException`1: A bulk write operation resulted in one or more errors.  E11000 duplicate key error index: ATA.UniqueEntityProfile.$_id_ dup key: { : " <guid> " }

También puede ver este error: System.ArgumentNullException: El valor no puede ser nulo.
    
Si ve alguno de estos errores, ejecute la siguiente solución.

**Solución alternativa**: 

1.  Mueva la carpeta "data_old" a una carpeta temporal (normalmente se encuentra en %Archivos de programa%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin).
2.  Desinstale el centro ATA v1.5 y elimine todos los datos de la base de datos.
![Desinstale ATA 1.5](http://i.imgur.com/x4nJycx.png)
3.  Vuelva a instalar el centro ATA v1.5. Asegúrese de usar la misma configuración que la instalación anterior de ATA 1.5 (certificados, direcciones IP, ruta de acceso de base de datos, etc.).
4.  Detenga estos servicios en el siguiente orden:
    1.  Centro Microsoft Advanced Threat Analytics
    2.  MongoDB
5.  Reemplace los archivos de base de datos de MongoDB por los archivos de la carpeta "data_old".
6.  Inicie estos servicios en el siguiente orden:
    1.  MongoDB
    2.  Centro Microsoft Advanced Threat Analytics
7.  Revise los registros para comprobar que el producto se ejecuta sin errores.
8.  [Descargue](http://aka.ms/ataremoveduplicateprofiles "Descargue") la herramienta "RemoveDuplicateProfiles.exe" y cópiela en la ruta de acceso de instalación principal (%Archivos de programa%\Microsoft Advanced Threat Analytics\Center)
9.  Desde un símbolo del sistema con privilegios elevados, ejecute "RemoveDuplicateProfiles.exe" y espere hasta que se complete correctamente.
10. Desde aquí: …\Microsoft Advanced Threat Analytics\Center\MongoDB\directorio bin: **Mongo ATA**, escriba el siguiente comando:

    db.SuspiciousActivities.remove({ "_t" : "RemoteExecutionSuspiciousActivity", "DetailsRecords" : { "$elemMatch" : { "ReturnCode" : null } } }, { "_id" : 1 });

![Solución de actualización](http://i.imgur.com/Nj99X2f.png)

Esto debe devolver un WriteResult({ "nRemoved" : XX }) donde "XX" es el número de actividades sospechosas que se han eliminado. Si el número es mayor que 0, cierre el símbolo del sistema y continúe con el proceso de actualización.


### NET Framework 4.6.1 exige reiniciar el servidor

En algunos casos, la instalación de .Net Framework 4.6.1 puede requerir que reinicie el servidor. Observe que, al hacer clic en Aceptar en el cuadro de diálogo **Configuración del centro Microsoft Advanced Threat Analytics**, el servidor se reinicia automáticamente. Esto es especialmente importante al instalar la puerta de enlace ligera de ATA en un controlador de dominio, ya que es posible que quiera planificar una ventana de mantenimiento antes de la instalación.
    ![Reinicio de .NET Framework](media/ata-net-framework-restart.png)

### Ya no se migran las actividades de red históricas
Esta versión de ATA ofrece un motor de detección mejorado que proporciona una detección más precisa y reduce muchos escenarios de falsos positivos, especialmente de pass-the-hash.
El nuevo motor de detección mejorado usa tecnología de detección integrada, lo que permite la detección sin acceder a la actividad de red histórica para aumentar considerablemente el rendimiento del centro ATA. Esto también significa que no es necesario migrar la actividad de red histórica durante el procedimiento de actualización.
El procedimiento de actualización de ATA exporta los datos, en caso de que los quiera para una investigación futura, a `<Center Installation Path>\Migration` como un archivo JSON.

## Véase también
[¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)

[Actualización de ATA a la versión 1.6 (guía de migración)](ata-update-1.6-migration-guide.md)

<!--HONumber=May16_HO4-->


