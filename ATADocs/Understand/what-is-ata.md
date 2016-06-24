---
# required metadata

title: ¿Qué es Microsoft Advanced Threat Analytics (ATA)? | Microsoft Advanced Threat Analytics
description: Se explica qué es Microsoft Advanced Threat Analytics (ATA) y qué tipos de actividades sospechosas puede detectar
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 283e7b4e-996a-4491-b7f6-ff06e73790d2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


## ¿Qué es ATA?
Microsoft Advanced Threat Analytics (ATA) es una solución líder en el sector del análisis del comportamiento de usuarios y entidades que ayuda a los profesionales de seguridad de TI a proteger sus organizaciones frente a ataques dirigidos avanzados y amenazas internas. Al analizar, aprender e identificar automáticamente el comportamiento normal y anómalo de las entidades (usuario, dispositivos y recursos) mediante la tecnología de aprendizaje automático, ATA ayuda a identificar técnicas y ataques malintencionados, problemas de seguridad y riesgos conocidos. Con la mejor información e inteligencia de investigadores de seguridad de primer orden, esta tecnología innovadora está diseñada para ayudar a las empresas a centrarse en detectar infracciones de seguridad antes de que causen daños.

## ¿Qué hace ATA?
ATA detecta lo siguiente:

  - Amenazas persistentes avanzadas al principio de la cadena del ataque, antes de que provoquen daños

  - Amenazas internas

ATA ayuda a separar las actividades sospechosas reales del ruido para centrarse en aquello que es crítico.

El motor de detección de ATA usa el aprendizaje automático, la inspección profunda de paquetes en el contexto de la entidad, el análisis de registros e información de Active Directory (AD) para analizar el comportamiento de los usuarios y las entidades.

ATA ejecuta un análisis en profundidad del tráfico de la organización y usa el aprendizaje automático para crear un mapa de actividades, tráfico y uso normales dentro de la organización. A partir de ahí, ATA vigilará y le avisará cuando algo anómalo ocurra. Esto se consigue mediante la ejecución de la tecnología de inspección profunda de paquetes de Microsoft, que habilita la inspección de paquetes en el contexto de la entidad para un mayor nivel de profundidad de análisis del tráfico de red, lo que permite a ATA analizar todos los niveles del tráfico de red.

ATA también recopila los eventos significativos de los sistemas SIEM y de los controladores de dominio. Después del análisis, ATA genera una vista dinámica que se actualiza constantemente de todos los usuarios, dispositivos y recursos de una organización. Con esta visión global, ATA es capaz de detectar ataques malintencionados conocidos como pass-the-hash, pass-the-ticket, ataques de reconocimiento, etc., así como de buscar cualquier anomalía en el comportamiento de las entidades de la red.

Una vez que detecta una actividad sospechosa, ATA genera una alerta y reduce al mínimo el número de falsos positivos que recibe mediante algoritmos avanzados de agregación y verificación de contexto.



## ¿Qué amenazas busca ATA?

Entre otras muchas, ATA detecta las siguientes fases de un ataque avanzado: reconocimiento, credenciales en peligro, movimiento lateral, escalación de privilegios, dominación de dominio, etc. Estas detecciones van dirigidas a detectar ataques avanzados y amenazas internas antes de que causen cualquier daño en la organización.

La detección de cada fase se traduce en varias actividades sospechosas relevantes para la fase en cuestión, donde cada actividad sospechosa guarda relación con distintos tipos de ataques posibles.

### Reconocimiento
ATA proporciona varias detecciones de reconocimiento. Estas detecciones incluyen:

-   **Reconocimiento mediante enumeración de cuentas**<br>Detecta los intentos de los atacantes de usar el protocolo Kerberos para saber si existe un usuario, aun cuando la actividad no se haya registrado como un evento en el controlador de dominio.
-   **Enumeración de sesiones de red**<br>
Como parte de la fase de reconocimiento, los atacantes pueden consultar al controlador de dominio para ver todas las sesiones activas de SMB en el servidor, lo que les permite obtener acceso a todos los usuarios y las direcciones IP asociados a esas sesiones de SMB. Los atacantes pueden usar la enumeración de sesiones de SMB para dirigirse a cuentas importantes, lo que les ayuda a moverse lateralmente por la red.
-   **Reconocimiento con DNS**<br>
La información de DNS de la red de destino suele ser información de reconocimiento muy útil. Contiene una lista de todos los servidores y, con frecuencia, todos los clientes y la asignación a sus direcciones IP. Ver la información de DNS puede proporcionar a los atacantes una vista detallada de estas entidades en el entorno que les permite centrar sus esfuerzos en las entidades relevantes para la campaña.

### Credenciales en peligro

Para poder detectar las credenciales en peligro, ATA hace uso tanto de análisis de comportamiento basados en el Aprendizaje automático como de la detección de técnicas y ataques malintencionados conocidos.

Con los análisis de comportamiento y el aprendizaje automático, ATA es capaz de detectar actividades sospechosas como inicios de sesión anómalos, accesos irregulares a recursos y horas de trabajo no habituales que apuntarían a que las credenciales están en peligro.
Para protegerse frente a las credenciales en peligro, ATA detecta las siguientes técnicas y ataques malintencionados conocidos:
:

 - **Fuerza bruta** <br>En los ataques por fuerza bruta, los atacantes intentan adivinar las credenciales de usuario al emparejar varios nombres de usuario con diversos intentos de contraseña. Muchas veces, los atacantes usan diccionarios o algoritmos de gran complejidad para probar con cuantos valores el sistema les permita.

- **Cuenta confidencial expuesta en la autenticación de texto sin formato**<br>
Si las credenciales de una cuenta con privilegios elevados se envían en texto sin formato, ATA le avisa para que pueda actualizar la configuración del equipo.

- **Servicio que expone cuentas en la autenticación de texto sin formato** <br>
Si un servicio de un equipo envía varias credenciales de cuenta en texto sin formato, ATA le avisa para que pueda actualizar la configuración del servicio.

- **Actividades sospechosas de cuentas de Honey Token**<br>
Las cuentas de Honey Token son cuentas ficticias configuradas para interceptar e identificar actividades malintencionadas que intentan usar esas cuentas ficticias y realizar un seguimiento de ellas. ATA le avisa de cualquier actividad en estas cuentas de Honey Token.
-   **Implementación de protocolos inusual**<br>
Las solicitudes de autenticación (Kerberos o NTLM) normalmente se realizan mediante un conjunto normal de métodos y protocolos. Sin embargo, para autenticar correctamente, la solicitud solo tiene que cumplir un conjunto específico de requisitos. Los atacantes pueden implementar estos protocolos con pequeñas desviaciones de la implementación normal en el entorno. Estas desviaciones pueden indicar la presencia de un atacante que intenta aprovechar o que aprovecha correctamente las credenciales en peligro.
-   **Solicitud malintencionada de información privada de protección de datos**<br>
La API de protección de datos (DPAPI) es un servicio de protección de datos basado en contraseña. Hay varias aplicaciones que almacenan secretos del usuario, como contraseñas de sitios web y credenciales de recurso compartido de archivos, que usan este servicio de protección. Para admitir escenarios de pérdida de contraseña, los usuarios pueden descifrar los datos protegidos con una clave de recuperación que no implique su contraseña. En un entorno de dominio, los atacantes pueden robar la clave de recuperación de forma remota y usarla para descifrar los datos protegidos en todos los equipos unidos al dominio.
-   **Comportamiento anómalo**<br>
A menudo, en los casos de amenazas internas, así como de ataques avanzados, las credenciales de cuenta pueden ponerse un riesgo mediante métodos de ingeniería social o métodos y técnicas nuevos y aún desconocidos. ATA es capaz de detectar estos tipos de peligros al analizar el comportamiento de la entidad y detectar las anomalías de las operaciones realizadas por la entidad y alertar de ellas.

### Movimiento lateral
Para proporcionar detección de movimiento lateral, cuando los usuarios usan credenciales que proporcionan acceso a algunos recursos para obtener acceso a recursos a los que no deberían acceder, ATA aprovecha el análisis de comportamientos basado en el aprendizaje automático y los ataques malintencionados conocidos y la detección técnica.

Con el análisis de comportamientos y el aprendizaje automático, ATA detecta los accesos irregulares a recursos, los dispositivos anómalos usados y otros indicadores que revelan la existencia de un movimiento lateral.

Además, ATA es capaz de detectar el movimiento lateral identificando las técnicas usadas por los atacantes para llevar a cabo ese movimiento lateral, como por ejemplo:

- **Pass-the-ticket** <br>
En los ataques pass-the-ticket, los atacantes roban un vale Kerberos de un equipo y lo usan para tener acceso a otro equipo suplantando una entidad en la red.
- **Pass-the-hash** <br>
En los ataques pass-the-hash, los atacantes roban el hash NTLM de una entidad y lo usan para autenticarse con NTLM, suplantar la entidad y obtener acceso a los recursos de la red.
- **Over-pass-the-hash**<br>
Los ataques over-pass-the-hash son aquellos en los que el atacante usa un hash NTLM robado para autenticarse con Kerberos y obtener un vale TGT de Kerberos válido que, seguidamente, usa para autenticarse como un usuario válido y tener acceso a los recursos de la red.
-   **Comportamiento anómalo**<br>
El movimiento lateral es una técnica que suelen usar los atacantes para moverse entre dispositivos y áreas de la red de la víctima y acceder a credenciales con privilegios o información confidencial de interés para ellos. ATA es capaz de detectar el movimiento lateral al analizar el comportamiento de los usuarios, los dispositivos y sus relaciones dentro de la red corporativa, así como de detectar cualquier patrón de acceso anómalo que pueda indicar un movimiento lateral realizado por un atacante.

### Escalación de privilegios
ATA detecta los ataques de escalación de privilegios correctos y los intentos en los que los atacantes intentan aumentar los privilegios existentes y usarlos varias veces para terminar controlando todo el entorno de la víctima. 

ATA habilita la detección de escalación de privilegios al combinar el análisis de comportamientos para detectar comportamientos anómalos de cuentas con privilegios y la detección de ataques y técnicas conocidos y malintencionados que se suelen usar para escalar privilegios, como:

- **Vulnerabilidad de seguridad MS14-068 (PAC falsificado)**<br>
Los ataques de PAC falsificado son aquellos en los que el atacante inserta datos de autorización en el vale TGT válido en forma de encabezado de autorización falsificado que le concede permisos adicionales que la organización no le había concedido. En este escenario el atacante aprovecha credenciales puestas en peligro anteriormente o credenciales recopiladas en operaciones de movimiento lateral.
- **Vulnerabilidad de seguridad MS11-013 (Silver PAC)**<br>
Los ataques de vulnerabilidad de seguridad MS11-013 son una vulnerabilidad de elevación de privilegios en Kerberos que permite que se falsifiquen ciertos aspectos de un vale de servicio Kerberos. Un usuario o un atacante malintencionado que aprovechara esta vulnerabilidad correctamente podría obtener un token con privilegios elevados en el controlador de dominio. En este escenario el atacante aprovecha credenciales puestas en peligro anteriormente o credenciales recopiladas en operaciones de movimiento lateral.

### Dominación de dominio
ATA detecta a los atacantes que consiguen correctamente la dominación y el control total sobre el entorno de la víctima o lo intentan al realizar una detección de técnicas conocidas usadas por los atacantes, como:

- **Malware Skeleton Key**<br>
En los ataques de Skeleton Key, se instala un malware en el controlador de dominio que permite a los atacantes autenticarse como cualquier usuario, sin impedir que los usuarios legítimos puedan seguir haciéndolo.
- **Golden ticket**<br>
En los ataques de golden ticket, un atacante roba las credenciales del KBTGT (golden ticket de Kerberos). Con ese vale, el atacante puede crear un vale TGT sin conexión, que se usará para tener acceso a los recursos de la red.
- **Ejecución remota**<br>
Los atacantes pueden tratar de controlar la red ejecutando código de forma remota en el controlador de dominio.
-   **Solicitudes malintencionadas de replicación**
En entornos de Active Directory (AD), la replicación entre controladores de dominio se produce con regularidad. Un atacante puede suplantar la identidad de la solicitud de replicación de AD (a veces suplantando como un controlador de dominio), lo que le permite recuperar los datos almacenados en Active Directory, incluidos los hash de contraseña, sin usar técnicas más intrusivas, como las instantáneas de volumen.

## ¿Qué viene a continuación?

-   Para obtener más información sobre el modo en que ATA se adapta a la red: [ATA architecture (Arquitectura de ATA)](/advanced-threat-analytics/plan-design/ata-architecture)

-   Para ver una introducción sobre cómo implementar ATA: [Install ATA (Instalación de ATA)](/advanced-threat-analytics/deploy-use/install-ata)

## Véase también
[¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


