---
# required metadata

title: Arquitectura de ATA | Microsoft Advanced Threat Analytics
description: Se describe la arquitectura de Microsoft Advanced Threat Analytics (ATA)
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 892b16d2-58a6-49f9-8693-1e5f69d8299c

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Arquitectura de ATA
En este diagrama se ilustra la arquitectura de Advanced Threat Analytics:

![Diagrama de topología de arquitectura de ATA](media/ATA-architecture-topology.jpg)

ATA supervisa el tráfico de red de los controladores de dominio mediante el uso de la creación de reflejo de puerto a una puerta de enlace de ATA con conmutadores físicos o virtuales, o implementando la puerta de enlace ligera de ATA directamente en los controladores de dominio, lo que elimina la necesidad de crear un reflejo del puerto. Además, ATA puede sacar provecho de los eventos de Windows (reenviados directamente desde los controladores de dominio o desde un servidor SIEM) y analizar los datos en busca de amenazas y ataques.
Esta sección describe el flujo de red y la captura de eventos y explora en profundidad para describir la funcionalidad de los componentes principales de ATA: la puerta de enlace de ATA, la puerta de enlace ligera de ATA (que tiene la misma funcionalidad principal que la puerta de enlace de ATA) y el Centro ATA.


![Diagrama de flujo de tráfico de ATA](media/ATA-traffic-flow.jpg)

## Componentes de ATA
ATA consta de lo siguiente:

-   **Centro ATA** <br>
El Centro ATA recibe datos de cualquier puerta de enlace de ATA o puerta de enlace ligera de ATA que implemente.
-   **Puerta de enlace de ATA**<br>
La puerta de enlace de ATA se instala en un servidor dedicado que supervisa el tráfico de los controladores de dominio mediante la creación de reflejo del puerto o un TAP de red.
-   **Puerta de enlace ligera de ATA**<br>
La puerta de enlace ligera de ATA se instala directamente en los controladores de dominio y supervisa el tráfico directamente, sin necesidad de un servidor dedicado ni de una configuración de creación de reflejo del puerto. Es una alternativa a la puerta de enlace de ATA.

Una implementación de ATA puede constar de un solo Centro ATA conectado a todas las puertas de enlace de ATA, todas las puertas de enlace ligeras de ATA o una combinación de las puertas de enlace de ATA y las puertas de enlace ligeras de ATA.


## Opciones de implementación
Puede implementar ATA mediante la siguiente combinación de puertas de enlace:

-   **Usar solo puertas de enlace de ATA** <br>
Si la implementación de ATA contiene solo puertas de enlace de ATA, sin ninguna puerta de enlace ligera de ATA, todos los controladores de dominio deben estar configurados para habilitar la creación de reflejo del puerto a una puerta de enlace de ATA o debe disponer de los TAP de red.
-   **Usar solo puertas de enlace ligeras de ATA**<br>
Si la implementación de ATA contiene solo puertas de enlace ligeras de ATA, las puertas de enlace ligeras de ATA se implementan en cada controlador de dominio y no se necesitan servidores adicionales ni configurar la creación de reflejo del puerto.
-   **Usar puertas de enlace de ATA y puertas de enlace ligeras de ATA**<br>
Si la implementación de ATA incluye tanto puertas de enlace de ATA como puertas de enlace ligeras de ATA, donde la puerta de enlace ligera de ATA está instalada en algunos de los controladores de dominio (por ejemplo, todos los controladores de dominio en las sucursales) mientras que otros controladores de dominio los supervisan las puertas de enlace de ATA (por ejemplo, los controladores de dominio más grandes en los centros de datos principales).

En los 3 escenarios, todas las puertas de enlace envían los datos al Centro ATA.




## Centro ATA
El **centro ATA** se encarga de lo siguiente:

-   Administra la configuración de las puertas de enlace de ATA y de las puertas de enlace ligeras de ATA

-   Recibe datos de las puertas de enlace de ATA y de las puertas de enlace ligeras de ATA 

-   Detecta las actividades sospechosas

-   Ejecuta algoritmos de aprendizaje automático de comportamiento de ATA para detectar un comportamiento anómalo

-   Ejecuta varios algoritmos deterministas para detectar ataques avanzados según la cadena de destrucción de ataques

-   Ejecuta la consola de ATA

-   Opcional: el centro ATA se puede configurar para enviar correos electrónicos y eventos cuando se detecte una actividad sospechosa.

El Centro ATA recibe el tráfico analizado por la puerta de enlace de ATA y la puerta de enlace ligera de ATA, genera perfiles, lleva a cabo una detección determinista y ejecuta el aprendizaje automático y algoritmos de comportamiento para obtener información sobre la red con el propósito de habilitar la detección de anomalías y avisarle de las actividades sospechosas.

|||
|-|-|
|Receptor de entidades|Recibe lotes de entidades procedentes de todas las puertas de enlace de ATA y puertas de enlace ligeras de ATA.|
|Procesador de actividades de red|Procesa todas las actividades de red de cada lote recibido. Por ejemplo, coteja los distintos pasos de Kerberos realizados desde equipos potencialmente distintos.|
|Generador de perfiles de entidades|Genera perfiles de todas las entidades únicas según el tráfico y los eventos. Por ejemplo, aquí es donde ATA actualiza la lista de equipos conectados de cada perfil de usuario.|
|Base de datos central|Administra el proceso de escritura de los eventos y actividades de red en la base de datos. |
|Capa|ATA usa MongoDB para almacenar todos los datos en el sistema:<br /><br />- Actividades de red<br />- Actividades de evento<br />- Entidades únicas<br />- Actividades sospechosas<br />- Configuración de ATA|
|Detectores|Los detectores usan algoritmos de aprendizaje automático y reglas deterministas para buscar actividades sospechosas y comportamientos de usuario anómalos en la red.|
|Consola de ATA|La consola de ATA sirve para configurar ATA y supervisar las actividades sospechosas detectadas por ATA en la red. La consola de ATA no depende del servicio del centro ATA y se ejecutará incluso cuando dicho servicio esté detenido, siempre que pueda comunicarse con la base de datos.|
Tenga en cuenta lo siguiente al decidir cuántos centros ATA necesita implementar en la red:

-   Un centro ATA puede supervisar un solo bosque de Active Directory. Si tiene más de un bosque de Active Directory, necesitará como mínimo un centro ATA por cada bosque de Active Directory.

-    En una implementación de Active Directory muy grande, es posible que un solo Centro ATA no sea capaz de administrar el tráfico de todos los controladores de dominio. En este caso, se necesitarán varios Centros ATA. El número de Centros ATA debe determinarse según el [Planeación de la capacidad de ATA](ata-capacity-planning.md).

## Puerta de enlace de ATA y puerta de enlace ligera de ATA

### Funcionalidad principal de la puerta de enlace
La **puerta de enlace de ATA** y la **puerta de enlace ligera de ATA** tienen la misma funcionalidad principal:

-   Capturar e inspeccionar el tráfico de red de los controladores de dominio (tráfico reflejado en el puerto en el caso de una puerta de enlace de ATA y tráfico local del controlador de dominio en el caso de una puerta de enlace ligera de ATA) 

-   Recibir eventos de Windows procedentes de servidores SIEM o Syslog, o de controladores de dominio mediante el reenvío de eventos de Windows

-   Recuperar datos sobre usuarios y equipos del dominio de Active Directory

-   Realizar tareas de resolución de entidades de red (usuarios, grupos y equipos)

-   Transferir datos relevantes al Centro ATA

-   Supervisar varios controladores de dominio de una sola puerta de enlace de ATA o supervisar un controlador de dominio para una puerta de enlace ligera de ATA.

La puerta de enlace de ATA recibe el tráfico de red y eventos de Windows de la red y los procesa en los siguientes componentes principales:

|||
|-|-|
|Escucha de red|La escucha de red se encarga de capturar el tráfico de red y de analizarlo. Se trata de una tarea que hace un uso intensivo de la CPU, por lo que es especialmente importante comprobar los [requisitos previos de ATA](ata-prerequisites.md) al planear la puerta de enlace de ATA o la puerta de enlace ligera de ATA.|
|Escucha de eventos|La escucha de eventos se encarga de capturar y analizar los eventos de Windows reenviados desde un servidor SIEM en la red.|
|Lector de registros de eventos de Windows|El lector de registros de eventos de Windows se encarga de leer y analizar eventos de Windows reenviados al registro de eventos de Windows de la puerta de enlace de ATA desde los controladores de dominio.|
|Traductor de actividades de red | Convierte el tráfico analizado en una representación lógica del tráfico que usa ATA (actividad de red).
|Resolución de entidades|La resolución de entidades toma los datos analizados (tráfico de red y eventos) y resuelve los datos con Active Directory para buscar información de cuenta y de identidad. Después, se comparan con las direcciones IP que constan en los datos analizados. La resolución de entidades inspecciona los encabezados de paquete de forma eficaz, para permitir analizar los paquetes de autenticación de nombres de equipo, propiedades e identidades. La resolución de entidad combina los paquetes de autenticación analizados con los datos en el paquete real.|
|Remitente de entidades|El remitente de entidades se encarga de enviar los datos analizados y cotejados al centro ATA.|

## Características de la puerta de enlace ligera de ATA

Las siguientes características funcionan de manera diferente dependiendo de si ejecuta una puerta de enlace de ATA o una puerta de enlace ligera de ATA.

-   **Candidato de sincronizador de dominio**<br>
La puerta de enlace del sincronizador de dominio es responsable de sincronizar todas las entidades de un dominio de Active Directory específico de forma proactiva (similar al mecanismo que usan los propios controladores de dominio para la replicación). Se elige una puerta de enlace de forma aleatoria, de la lista de candidatos, para que actúe como el sincronizador de dominio. <br><br>
Si el sincronizador está sin conexión durante más de 30 minutos, se elige otro candidato en su lugar. Si no hay ningún sincronizador de dominio disponible para un dominio específico, ATA no podrá sincronizar proactivamente las entidades y sus cambios, pero ATA recuperará reactivamente nuevas entidades, ya que se detectan en el tráfico supervisado. 
<br>Si no hay ningún sincronizador de dominio disponible y busca una entidad que no tenía ningún tráfico relacionado, no se mostrarán resultados de la búsqueda.<br><br>
De manera predeterminada, todas las puertas de enlace de ATA son candidatas de sincronizador.<br><br>
Ya que es más probable que todas las puertas de enlace ligeras de ATA se implementen en sucursales y en controladores de dominio pequeños, no son candidatas de sincronizador de manera predeterminada.


-   **Limitaciones de los recursos**<br>
La puerta de enlace ligera de ATA incluye un componente de supervisión que evalúa la capacidad de proceso y memoria disponibles en el controlador de dominio en el que se está ejecutando. El proceso de supervisión se ejecuta cada 10 segundos y actualiza dinámicamente la cuota de uso de CPU y memoria en el proceso de puerta de enlace ligera de ATA para asegurarse de que, en cualquier momento determinado, el controlador de dominio tiene al menos el 15 % de recursos de proceso y de memoria libres.<br><br>
Independientemente de lo que ocurra en el controlador de dominio, este proceso libera siempre recursos para asegurarse de que no se ve afectada la funcionalidad principal del controlador de dominio.<br><br>
Si esto hace que la puerta de enlace ligera de ATA se quede sin recursos, se supervisa únicamente el tráfico parcial y aparecerá la alerta de supervisión "Se quitó el tráfico de red reflejado en puerto" en la página de estado.

En la siguiente tabla se proporciona un ejemplo de un controlador de dominio con suficientes recursos de proceso disponibles para permitir una cuota mayor de la que se necesita actualmente, por lo que se supervisa todo el tráfico:

||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|Puerta de enlace ligera de ATA (Microsoft.Tri.Gateway.exe)|Varios (otros procesos) |Cuota de la puerta de enlace ligera de ATA|La puerta de enlace quita|
|30 %|20 %|10 %|45 %|No|

Si Active Directory necesita más procesos, se reduce la cuota que necesita la puerta de enlace ligera de ATA. En el siguiente ejemplo, la puerta de enlace ligera de ATA necesita más cuota que la asignada y quita algún tráfico (supervisa solo el tráfico parcial):

||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|Puerta de enlace ligera de ATA (Microsoft.Tri.Gateway.exe)|Varios (otros procesos) |Cuota de la puerta de enlace ligera de ATA|La puerta de enlace está quitando|
|60 %|15 %|10 %|15 %|Sí|



## Los componentes de red
Para trabajar con ATA, tenga en cuenta lo siguiente:

### Creación de reflejo del puerto
Si usa puertas de enlace de ATA, tendrá que configurar la creación de reflejo del puerto para los controladores de dominio que se supervisarán y establecer la puerta de enlace de ATA como destino mediante los conmutadores físicos o virtuales. Otra opción es usar los TAP de red. ATA funcionará si solo algunos controladores de dominio (no todos) están supervisados, pero las detecciones serán menos efectivas.

La creación de reflejo del puerto hace que se refleje todo el tráfico de red del controlador de dominio en la puerta de enlace de ATA, pero solo un porcentaje muy pequeño de ese tráfico se comprime y envía al Centro ATA para analizarlo.

Los controladores de dominio y las puertas de enlace de ATA pueden ser físicos o virtuales. Para obtener más información, vea [Configure port mirroring](/advanced-threat-analytics/deploy-use/configure-port-mirroring) (Configurar la creación de reflejo del puerto).


### Eventos
Para mejorar la detección de ATA de ataques pass-the-hash, por fuerza bruta y de Honey Token, ATA necesita el id. 4776 del registro de eventos de Windows. Esto se puede reenviar a la puerta de enlace de ATA de dos maneras diferentes: configurando la puerta de enlace de ATA para que escuche eventos de SIEM o mediante el reenvío de eventos de Windows.

-   Configurar la puerta de enlace de ATA para que escuche eventos de SIEM <br>Configure el SIEM para que reenvíe eventos de Windows específicos a ATA. ATA admite diversos proveedores de SIEM. Para obtener más información, vea [Configurar la recopilación de eventos](/advanced-threat-analytics/deploy-use/configure-event-collection).

-   Configurar el reenvío de eventos de Windows<br>Otra forma de que ATA obtenga eventos consiste en configurar los controladores de dominio de manera que reenvíen el evento de Windows 4776 a la puerta de enlace de ATA. Esto es especialmente útil si no hay un SIEM o si el SIEM no es compatible actualmente con ATA. Para obtener más información sobre el reenvío de eventos de Windows en ATA, vea [Configurar el reenvío de eventos de Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding).

## Véase también
- [Requisitos previos de ATA](ata-prerequisites.md)
- [Planeamiento de la capacidad de ATA](ata-capacity-planning.md)
- [Configurar la recopilación de eventos](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Configurar el reenvío de eventos de Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)



<!--HONumber=May16_HO2-->


