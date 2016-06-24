---
# required metadata

title: Preguntas más frecuentes sobre ATA | Microsoft Advanced Threat Analytics
description: Se proporciona una lista de preguntas más frecuentes sobre ATA y las correspondientes respuestas
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: a7d378ec-68ed-4a7b-a0db-f5e439c3e852

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Preguntas más frecuentes sobre ATA
En este artículo se proporciona una lista de preguntas más frecuentes sobre ATA y las correspondientes respuestas e información necesaria.


## ¿Cómo se puede obtener una licencia de ATA?
Para obtener información sobre licencias, vea [Cómo comprar Advanced Threat Analytics](https://www.microsoft.com/en-us/server-cloud/products/advanced-threat-analytics/Purchasing.aspx)


## ¿Qué debo hacer si la puerta de enlace de ATA no se inicia?
Busque el error más reciente en el registro de errores actual (carpeta "Logs" (registros) del directorio donde ATA esté instalado).
## ¿Cómo puedo probar ATA?
Puede simular actividades sospechosas, que es una prueba completa. Para ello, haga lo siguiente:

1.  Reconocimiento de DNS mediante Nslookup.exe
2.  Ejecución remota mediante psexec.exe


Esto hay que ejecutarlo de forma remota en el controlador de dominio que se está supervisando, no desde la puerta de enlace de ATA.

## ¿Cómo se puede comprobar el reenvío de eventos de Windows?
Puede ejecutar lo siguiente desde un símbolo del sistema en el directorio **\Archivos de programa\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**:

        mongo ATA --eval "printjson(db.getCollectionNames())" | find /C "NtlmEvents"`
## ¿Funciona ATA con el tráfico cifrado?
El tráfico cifrado no se analizará (por ejemplo: LDAPS, IPSEC ESP).
## ¿Funciona ATA con la protección de Kerberos?
ATA permite habilitar la protección de Kerberos, también conocida como túnel seguro de autenticación flexible (FAST), salvo para detectar ataques de overpass-the-hash, donde no funcionará.
## ¿Cuántas puertas de enlace de ATA son necesarias?

En primer lugar, se recomienda que use puertas de enlace ligeras de ATA en cualquier controlador de dominio que las pueda acomodar, vea [Tamaño de puerta de enlace ligera de ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning#ATA-Lightweight-Gateway-Sizing). 

Si las puertas de enlace ligeras de ATA pueden cubrir todos los controladores de dominio, no se necesitan puertas de enlace de ATA.

Para los controladores de dominio que no pueda cubrir la puerta de enlace ligera de ATA, tenga en cuenta lo siguiente al decidir cuántas puertas de enlace de ATA necesita:

 - La cantidad total de tráfico que generan los controladores de dominio, así como la arquitectura de red (para configurar el reflejo del puerto). Para obtener más información sobre cómo saber cuánto tráfico generan los controladores de dominio, vea [Estimación del tráfico del controlador de dominio](/advanced-threat-analytics/plan-design/ata-capacity-planning#Domain-controller-traffic-estimation).
 - Las limitaciones operativas de creación de reflejo del puerto también determinan el número de puertas de enlace de ATA que necesita para dar cabida a los controladores de dominio (por ejemplo, por conmutador, por centro de datos, por región, etc.). Cada entorno tendrá sus propias consideraciones. 

## ¿Cuánto almacenamiento es necesario para ATA?
Por cada día completo con un promedio de 1000 paquetes por segundo, deberá disponer de 0,3 GB de almacenamiento.<br /><br />Para obtener más información sobre el tamaño del Centro ATA, vea [Planeación de la capacidad de ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning).


## ¿Por qué algunas cuentas se consideran confidenciales?
Esto ocurre cuando una cuenta es miembro de determinados grupos designados como confidenciales (por ejemplo: "Administradores del dominio").

Si quiere entender por qué una cuenta es confidencial, puede revisar su pertenencia a grupos para saber a qué grupos confidenciales pertenece (el grupo al que pertenece también puede ser confidencial debido a otro grupo, por lo que este mismo proceso deberá realizarse hasta encontrar el grupo confidencial de nivel más alto).

## ¿Cómo se supervisa un controlador de dominio virtual con ATA?
La mayoría de los controladores de dominio virtuales los puede cubrir la puerta de enlace ligera de ATA. Para determinar si la puerta de enlace ligera de ATA es adecuada para su entorno, vea [Planeación de la capacidad de ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning).

Si hay un controlador de dominio virtual que no puede cubrir la puerta de enlace ligera de ATA, puede tener una puerta de enlace de ATA física o virtual, tal y como se describe en [Configure port mirroring](/advanced-threat-analytics/deploy-use/configure-port-mirroring) (Configurar la creación de reflejo del puerto).  <br />La manera más fácil es tener una puerta de enlace de ATA virtual en cada host donde haya un controlador de dominio virtual.<br />Si los controladores de dominio virtuales se mueven entre hosts, debe realizar una de las siguientes tareas:

-   Cuando el controlador de dominio virtual se mueva a otro host, preconfigure la puerta de enlace de ATA en ese host para recibir el tráfico del controlador de dominio virtual recién desplazado.
-   Asegúrese de afiliar la puerta de enlace de ATA virtual al controlador de dominio virtual para que, si se mueve, la puerta de enlace de ATA lo haga junto con él.
-   Hay algunos conmutadores virtuales que pueden enviar tráfico entre hosts.

## ¿Cómo puedo hacer una copia de seguridad de ATA?
Se puede hacer una copia de seguridad de dos elementos:

-   El tráfico y los eventos almacenados por ATA. Se puede hacer una copia de seguridad de estos elementos usando cualquiera de los procedimientos de copia de seguridad de base de datos compatibles. Para obtener más información, vea [Administración de la base de datos de ATA](/advanced-threat-analytics/deploy-use/ata-database-management). 
-   La configuración de ATA, que se almacena en la base de datos y de la que se hace una copia de seguridad automática cada hora. 

## ¿Qué detecta ATA?
ATA detecta ataques y técnicas malintencionadas, problemas de seguridad y riesgos conocidos.
Para ver una lista completa de las detecciones de ATA, vea [¿Qué es Microsoft Advanced Threat Analytics?](what-is-ata.md).

## ¿Qué tipo de almacenamiento es necesario para ATA?
Se recomienda el almacenamiento rápido (no se recomiendan discos de 7200 RPM) con acceso a disco de baja latencia (menos de 10 ms). La configuración de la RAID debe admitir la carga de mucha escritura (no se recomiendan RAID-5/6 ni sus derivados).

## ¿Cuántas NIC necesita la puerta de enlace de ATA?
La puerta de enlace de ATA necesita un mínimo de dos adaptadores de red:<br>1. Una NIC para conectarse a la red interna y el centro ATA<br>2. Una NIC que se usará para capturar el tráfico de red de los controladores de dominio a través de la creación de reflejo del puerto.<br>* Esto no se aplica a la puerta de enlace ligera de ATA, que usa de forma nativa todos los adaptadores de red que usa el controlador de dominio.

## ¿Qué tipo de integración tiene ATA con los SIEM?
ATA presenta la siguiente integración bidireccional con los SIEM:

1. ATA se puede configurar para enviar una alerta de Syslog en caso de producirse una actividad sospechosa en cualquier servidor SIEM con el formato CEF.
2. ATA se puede configurar para recibir mensajes de Syslog por cada evento de Windows con el id. 4776 desde [estos SIEM](/advanced-threat-analytics/deploy-use/configure-event-collection#SIEM-support).

## ¿Puede ATA supervisar controladores de dominio que se visualizan en la solución de IaaS?

Sí, puede usar la puerta de enlace ligera de ATA para supervisar controladores de dominio que se encuentren en cualquier solución de IaaS.

## ¿Se trata de una oferta local o en la nube?
Microsoft Advanced Threat Analytics es un producto local.

## ¿Va a formar parte de Azure Active Directory o de Active Directory local?
Actualmente, esta solución es una oferta independiente; no forma parte de Azure Active Directory ni de Active Directory local.

## ¿Tengo que escribir mis propias reglas y crear un umbral o línea base?
Con Microsoft Advanced Threat Analytics, no hay ninguna necesidad de crear reglas, umbrales o líneas base ni de ajustar nada. ATA analiza los comportamientos entre usuarios, dispositivos y recursos, así como la relación entre ellos, y es capaz de detectar cualquier actividad sospechosa o ataque conocido con rapidez. ATA comenzará a detectar actividades con un comportamiento sospechoso tres semanas después de su implementación. Pero ATA comenzará a detectar ataques malintencionados y problemas de seguridad conocidos inmediatamente después de haberse implementado.

## Si el ataque ya se ha producido, ¿podrá Microsoft Advanced Threat Analytics identificar el comportamiento anómalo?
Sí, aunque ATA se haya instalado después de la infracción de seguridad, será capaz de detectar actividades sospechosas de hackers. ATA no solo se fija en el comportamiento del usuario, sino también en el de otros usuarios del mapa de seguridad de la organización. Durante el transcurso del primer análisis, si el comportamiento del atacante es anómalo, ATA lo identificará como un "valor atípico" y llevará un seguimiento informativo de ese comportamiento anómalo. Además, ATA puede detectar la actividad sospechosa de un hacker que intente robar las credenciales de otro usuario (como pass-the-ticket) o que trate de realizar una ejecución remota en uno de los controladores de dominio.

## ¿Esto solo es válido en el tráfico de Active Directory?
Aparte de analizar el tráfico de Active Directory mediante una tecnología de inspección profunda de paquetes, ATA también puede recopilar eventos relevantes del sistema de administración de eventos e información de seguridad, así como crear perfiles de entidades basados en información de Servicios de dominio de Active Directory. También recopila eventos de los registros de eventos, en caso de que la organización tenga configurado el reenvío de registro de eventos de Windows.

## ¿Qué es la creación de reflejo del puerto?
La creación de reflejo del puerto, también conocida como SPAN (Switched Port Analyzer, analizador de puerto conmutado), es un método para supervisar el tráfico de red. Cuando la creación de reflejo del puerto está habilitada, el conmutador envía una copia de todos los paquetes de red detectados en un puerto (o una VLAN completa) a otro puerto, donde dichos paquetes se pueden analizar.

## ¿ATA solo supervisa los dispositivos unidos a un dominio?
No. ATA supervisa todos los dispositivos de la red que realicen solicitudes de autenticación y autorización en Active Directory, incluidos los dispositivos móviles y los que no son de Windows.

## ¿Supervisa ATA las cuentas de equipo y las de usuario?
Sí. Las cuentas de equipo (así como las de cualquier otra entidad) se pueden usar para realizar actividades malintencionadas, de ahí que ATA supervise el comportamiento de todas las cuentas de equipo y demás entidades en el entorno.

## ¿Admite ATA varios dominios y varios bosques?
En términos de disponibilidad general, Microsoft Advanced Threat Analytics admite varios dominios con el mismo límite de bosque. El bosque en sí es el "límite de seguridad" de facto, de modo que si se admiten múltiples dominios, nuestros clientes tendrán una cobertura del 100 % de los entornos con ATA.

## ¿Se puede ver el estado general de la implementación?
Sí. Se puede ver el estado general de la implementación, así como problemas específicos relacionados con la configuración, la conectividad, etc. Además, recibirá una alerta cuando se produzcan.


## Véase también
- [Requisitos previos de ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Planeamiento de la capacidad de ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Configurar la recopilación de eventos](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Configurar el reenvío de eventos de Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#Configuring-Windows-Event-Forwarding)
- [¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)



<!--HONumber=May16_HO3-->


