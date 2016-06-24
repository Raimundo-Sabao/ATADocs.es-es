---
# required metadata

title: Requisitos previos de ATA | Microsoft Advanced Threat Analytics
description: Se describen los requisitos para implementar ATA correctamente en el entorno
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: a5f90544-1c70-4aff-8bf3-c59dd7abd687

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Requisitos previos de ATA
En este artículo se describen los requisitos para implementar ATA correctamente en el entorno.

>[!NOTE] Para obtener más información sobre cómo planear la capacidad y los recursos, vea [Planeación de la capacidad de ATA](ata-capacity-planning.md).


ATA está formado por el Centro ATA, la puerta de enlace de ATA o la puerta de enlace ligera de ATA. Para obtener más información sobre los componentes de ATA, vea [Arquitectura de ATA](ata-architecture.md).


[Antes de empezar:](#before-you-start) en esta sección se indica la información que debe reunir y las cuentas y entidades de red que deben existir antes de iniciar la instalación de ATA.

[Centro ATA:](#ata-center-requirements) en esta sección se especifica el hardware, el software y los requisitos del Centro ATA, además de la configuración que es necesario definir en el servidor del Centro ATA.

[Puerta de enlace de ATA:](#ata-gateway-requirements) en esta sección se especifica el hardware, el software y los requisitos de la puerta de enlace de ATA, además de la configuración que es necesario definir en los servidores de la puerta de enlace de ATA.

[Puerta de enlace ligera de ATA](#ata-lightweight-gateway-requirements): esta sección enumera los requisitos de software y hardware de la puerta de enlace ligera de ATA.

[Consola de ATA:](#ata-console) en esta sección se enumeran los requisitos de explorador para ejecutar la consola de ATA.

![Diagrama de arquitectura de ATA](media/ATA-architecture-topology.jpg)

## Antes de empezar
En esta sección se indica la información que debe reunir y las cuentas y entidades de red que deben existir antes de iniciar la instalación de ATA.


-   Cuenta de usuario y contraseña con acceso de lectura a todos los objetos de los dominios que se van a supervisar.

    > [!NOTE] Si tiene configuradas ACL personalizadas en varias unidades organizativas del dominio, procure que el usuario seleccionado tenga permisos de lectura a esas unidades organizativas.

-   Tenga una lista de todas las subredes que se usan en la red para VPN y Wi-Fi, que reasignan direcciones IP entre dispositivos en un breve intervalo de tiempo (segundos o minutos).  Conviene identificar estas subredes de concesión a corto plazo para que ATA pueda reducir su duración de caché y, de este modo, dar cabida a las reasignaciones rápidas entre dispositivos. Vea [Instalación de ATA](/advanced-threat-analytics/deploy-use/install-ata) para ver la configuración de subredes de concesión a corto plazo.
-   Asegúrese de que el Analizador de mensajes y Wireshark no están instalados en la puerta de enlace de ATA ni el centro ATA.
-    Opcional: se recomienda que el usuario tenga permiso de solo lectura en el contenedor de objetos eliminados, ya que esto permitirá a ATA detectar la eliminación masiva de objetos en el dominio. Para más información sobre cómo configurar permisos de solo lectura en el contenedor de objetos eliminados, consulte la sección **Cambiar permisos en un contenedor de objetos eliminados** del tema [Ver o establecer permisos en un objeto de directorio](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx).

-   Opcional: una cuenta de usuario de un usuario que no tenga actividades de red. Esta cuenta se configurará como el usuario de honeytoken de ATA. Para configurar el usuario de honeytoken, necesitará el SID de la cuenta de usuario, no el nombre de usuario.

-   Opcional: además de recopilar y analizar el tráfico de red hacia y desde los controladores de dominio, ATA puede usar el evento 4776 de Windows para mejorar aún más la detección de ataques pass-the-hash. Dicho evento puede recibirse mediante SIEM o mediante el establecimiento del reenvío de eventos de Windows desde el controlador de dominio. Los eventos recopilados proporcionan a ATA información adicional que no está disponible a través del tráfico de red del controlador de dominio.


## Requisitos del Centro ATA
En esta sección se enumeran los requisitos del Centro ATA.
### General
El Centro ATA se puede instalar en un servidor que ejecute Windows Server 2012 R2. El Centro ATA se puede instalar en un servidor que sea miembro de un dominio o un grupo de trabajo.

El Centro ATA se puede instalar como una máquina virtual. 

Si ejecuta el Centro ATA como una máquina virtual, apague el servidor antes de crear un punto de control para evitar posibles daños en la base de datos.
### Especificaciones del servidor
La base de datos de ATA requiere que se **deshabilite** el acceso a memoria no uniforme (NUMA) en el BIOS. El sistema puede hacer referencia a NUMA como una intercalación de nodos, en cuyo caso tendrá que **habilitar** la intercalación de nodos para deshabilitar NUMA. Consulte la documentación del BIOS para más información.<br>
Para disfrutar del mejor rendimiento posible, establezca la **Opción de energía** del Centro ATA en **Alto rendimiento**.<br>
Las especificaciones del servidor dependerán del número de controladores de dominio que vaya a supervisar y de la carga de cada uno de los controladores de dominio. Vea [Planeación de la capacidad de ATA](ata-capacity-planning.md) para obtener más información.

### Sincronización de hora
El servidor del Centro ATA, los servidores de la puerta de enlace de ATA y los controladores de dominio deben estar sincronizados a intervalos de 5 minutos entre sí.


### Adaptadores de red
Debe disponer de lo siguiente:
-   Como mínimo un adaptador de red

-   Dos direcciones IP (recomendado pero no obligatorio)

La comunicación entre el Centro ATA y la puerta de enlace de ATA se cifra mediante SSL en el puerto 443. Además, la consola de ATA se ejecuta en IIS y se protege con SSL en el puerto 443. Se recomienda disponer de **dos direcciones IP**. El servicio del Centro ATA enlazará el puerto 443 a la primera dirección IP, mientras que IIS enlazará el puerto 443 a la segunda.

> [!NOTE] Se podría usar una única dirección IP con dos puertos diferentes, pero se recomienda usar dos direcciones IP.

### Puertos
En la siguiente tabla se enumeran los puertos mínimos que han de estar abiertos para que el Centro ATA funcione correctamente.

En esta tabla, la dirección IP 1 se enlaza al servicio del Centro ATA y la dirección IP 2, al servicio de IIS de la consola de ATA:

|Protocol|Transporte|Puerto|Hacia/Desde|Direction|Dirección IP|
|------------|-------------|--------|-----------|-------------|--------------|
|**SSL** (comunicaciones de ATA)|TCP|443 o configurable|Puerta de enlace de ATA|Entrante|Dirección IP 1|
|**HTTP**|TCP|80|Red de la empresa|Entrante|Dirección IP 2|
|**HTTPS**|TCP|443|Red de la empresa y puerta de enlace de ATA|Entrante|Dirección IP 2|
|**SMTP** (opcional)|TCP|25|Servidor SMTP|Saliente|Dirección IP 2|
|**SMTPS** (opcional)|TCP|465|Servidor SMTP|Saliente|Dirección IP 2|
|**Syslog** (opcional)|TCP|514|Servidor de Syslog|Saliente|Dirección IP 2|

### Certificados
Asegúrese de que el Centro ATA tiene acceso al punto de distribución CRL. Si las puertas de enlace de ATA carecen de acceso a Internet, realice [el procedimiento para importar una CRL manualmente](https://technet.microsoft.com/en-us/library/aa996972%28v=exchg.65%29.aspx), asegurándose de instalar todos los puntos de distribución CRL de toda la cadena.

Para facilitar la instalación del Centro ATA, durante este proceso puede instalar certificados autofirmados. Tras la implementación, puede reemplazar el certificado autofirmado por un certificado de una entidad de certificación interna para que lo use la puerta de enlace de ATA.<br>
> [!NOTE] El tipo de proveedor del certificado debe ser proveedor de servicios criptográficos (CSP).


El Centro ATA requiere certificados para los siguientes servicios:

-   Internet Information Services (IIS): certificado de servidor web

-   Servicio del Centro ATA: certificado de autenticación de servidor

> [!NOTE] Si va a tener acceso a la consola de ATA desde otros equipos, asegúrese de que esos equipos confían en el certificado que IIS usa; de lo contrario, se abrirá una página de advertencia que informa de que hay un problema con el certificado de seguridad del sitio web antes de llegar a la página de inicio de sesión.

## Requisitos de la puerta de enlace de ATA
En esta sección se enumeran los requisitos de la puerta de enlace de ATA.
### General
La puerta de enlace de ATA se puede instalar en un servidor que ejecute Windows Server 2012 R2.
La puerta de enlace de ATA se puede instalar en un servidor que sea miembro de un dominio o un grupo de trabajo.

Antes de instalar la puerta de enlace de ATA, confirme que se ha instalado la siguiente actualización: [KB2919355](https://support.microsoft.com/en-us/kb/2919355/).

Lo puede comprobar ejecutando el siguiente cmdlet de Windows PowerShell: `[Get-HotFix -Id kb2919355]`.

Para obtener más información sobre cómo usar máquinas virtuales con la puerta de enlace de ATA, vea [Configure port mirroring](/advanced-threat-analytics/deploy-use/configure-port-mirroring) (Configurar la creación de reflejo del puerto).

### Especificaciones del servidor
Para disfrutar del mejor rendimiento posible, establezca la **opción de energía** de la puerta de enlace de ATA en **alto rendimiento**.<br>
Una puerta de enlace de ATA permite supervisar varios controladores de dominio, según la cantidad de tráfico de red hacia y desde los controladores de dominio.


### Sincronización de hora
El servidor del Centro ATA, los servidores de la puerta de enlace de ATA y los controladores de dominio deben estar sincronizados a intervalos de 5 minutos entre sí.

### Adaptadores de red
La puerta de enlace de ATA necesita como mínimo un adaptador de administración y de un adaptador de captura:

-   **Adaptador de administración:** se usará en las comunicaciones de la red corporativa. Este adaptador debe configurarse con los siguientes elementos:

    -   Dirección IP estática que incluya la puerta de enlace predeterminada

    -   Servidores DNS preferido y alternativo

    -   El **Sufijo DNS para esta conexión** debe ser el nombre DNS del dominio de cada dominio que se esté supervisando.

        ![Configurar el sufijo DNS en Configuración avanzada de TCP/IP](media/ATA-DNS-Suffix.png)

        > [!NOTE] Si la puerta de enlace de ATA es un miembro del dominio, esto se configurará automáticamente.

-   **Adaptador de captura:** se usará para capturar el tráfico hacia y desde los controladores de dominio.

    > [!IMPORTANT]
    > -   Configure la creación de reflejo del puerto del adaptador de captura como destino del tráfico de red del controlador de dominio. Para obtener más información, vea [Configure port mirroring](/advanced-threat-analytics/deploy-use/configure-port-mirroring) (Configurar la creación de reflejo del puerto). Normalmente, para configurar la creación de reflejo del puerto tendrá que colaborar con el equipo de virtualización o de redes.
    > -   Configure una dirección IP no enrutable estática en el entorno sin una puerta de enlace predeterminada y sin direcciones de servidor DNS. Por ejemplo, 1.1.1.1/32. Esto hará que el adaptador de red de captura pueda capturar la máxima cantidad de tráfico posible y que el adaptador de red de administración se use para enviar y recibir el tráfico de red necesario.

### Puertos
En la siguiente tabla se enumeran los puertos mínimos que la puerta de enlace de ATA necesita que estén configurados en el adaptador de administración:

|Protocol|Transporte|Puerto|Hacia/Desde|Direction|
|------------|-------------|--------|-----------|-------------|
|LDAP|TCP y UDP|389|Controladores de dominios|Saliente|
|LDAP seguro (LDAPS)|TCP|636|Controladores de dominios|Saliente|
|LDAP para Catálogo global|TCP|3268|Controladores de dominios|Saliente|
|LDAPS para Catálogo global|TCP|3269|Controladores de dominios|Saliente|
|Kerberos|TCP y UDP|88|Controladores de dominios|Saliente|
|Netlogon|TCP y UDP|445|Controladores de dominios|Saliente|
|Hora de Windows|UDP|123|Controladores de dominios|Saliente|
|DNS|TCP y UDP|53|Servidores DNS|Saliente|
|NTLM sobre RPC|TCP|135|Todos los dispositivos de la red|Saliente|
|NetBIOS|UDP|137|Todos los dispositivos de la red|Saliente|
|SSL|TCP|443 o según esté configurado en el servicio del Centro|Centro ATA:<br /><br />- Dirección IP de servicio del Centro<br />- Dirección IP de IIS|Saliente|
|Syslog (opcional)|UDP|514|Servidor SIEM|Entrante|

> [!NOTE] Como parte del proceso de resolución realizado por la puerta de enlace de ATA, hay que abrir los siguientes puertos entrantes en los dispositivos de la red desde las puertas de enlace de ATA.
>
> -   NTLM sobre RPC
> -   NetBIOS

### Certificados
Asegúrese de que el Centro ATA tiene acceso al punto de distribución CRL. Si las puertas de enlace de ATA carecen de acceso a Internet, realice el procedimiento para importar una CRL manualmente, asegurándose de instalar todos los puntos de distribución CRL de toda la cadena.<br>
Para facilitar la instalación del Centro ATA, durante este proceso puede instalar certificados autofirmados. Tras la implementación, puede reemplazar el certificado autofirmado por un certificado de una entidad de certificación interna para que lo use la puerta de enlace de ATA.

> [!NOTE]
El tipo de proveedor del certificado debe ser proveedor de servicios criptográficos (CSP).<br>

Debe haber un certificado de **autenticación de servidor** instalado en el almacén del equipo de la puerta de enlace de ATA en el almacén del equipo local. Dicho certificado debe ser de confianza para el Centro ATA.

## Requisitos de la puerta de enlace ligera de ATA
En esta sección se enumeran los requisitos de la puerta de enlace ligera de ATA.
### General
La puerta de enlace ligera de ATA admite la instalación en un controlador de dominio que ejecute Windows Server 2008 R2, Windows Server 2012 o Windows Server 2012 R2.

El controlador de dominio puede ser un controlador de dominio de solo lectura (RODC).

El controlador de dominio no puede ser Server Core.

### Especificaciones del servidor

La puerta de enlace ligera de ATA requiere un mínimo de 2 núcleos y 6 GB de RAM instalados en el controlador de dominio.
Para disfrutar del mejor rendimiento posible, establezca la **Opción de energía** de la puerta de enlace ligera de ATA en **Alto rendimiento**.
La puerta de enlace ligera de ATA puede implementarse en controladores de dominio de varias cargas y tamaños, según la cantidad de tráfico de red hacia y desde los controladores de dominio y la cantidad de recursos instalados en ese controlador de dominio.

### Sincronización de hora
El servidor del Centro ATA, los servidores de la puerta de enlace ligera de ATA y los controladores de dominio deben estar sincronizados a intervalos de 5 minutos entre sí.
### Adaptadores de red
La puerta de enlace ligera de ATA supervisa el tráfico local en todos los adaptadores de red del controlador de dominio. <br>
Después de la implementación, puede usar la consola de ATA si quiere modificar qué adaptadores de red se supervisan.

### Puertos
En la siguiente tabla se enumeran los puertos mínimos que la puerta de enlace ligera de ATA necesita:

|Protocol|Transporte|Puerto|Hacia/Desde|Direction|
|------------|-------------|--------|-----------|-------------|
|DNS|TCP y UDP|53|Servidores DNS|Saliente|
|NTLM sobre RPC|TCP|135|Todos los dispositivos de la red|Saliente|
|NetBIOS|UDP|137|Todos los dispositivos de la red|Saliente|
|SSL|TCP|443 o según esté configurado en el servicio del Centro|Centro ATA:<br /><br />- Dirección IP de servicio del Centro<br />- Dirección IP de IIS|Saliente|
|Syslog (opcional)|UDP|514|Servidor SIEM|Entrante|

> [!NOTE] Como parte del proceso de resolución realizado por la puerta de enlace ligera de ATA, hay que abrir los siguientes puertos entrantes en los dispositivos de la red desde las puertas de enlace ligeras de ATA.
>
> -   NTLM sobre RPC
> -   NetBIOS

### Certificados
Asegúrese de que el Centro ATA tiene acceso al punto de distribución CRL. Si las puertas de enlace ligeras de ATA carecen de acceso a Internet, realice el procedimiento para importar una CRL manualmente, y asegúrese de instalar todos los puntos de distribución CRL de toda la cadena.
Para facilitar la instalación del Centro ATA, durante este proceso puede instalar certificados autofirmados. Tras la implementación, puede reemplazar el certificado autofirmado por un certificado de una entidad de certificación interna para que lo use la puerta de enlace ligera de ATA.
> [!NOTE]
El tipo de proveedor del certificado debe ser proveedor de servicios criptográficos (CSP).

Debe haber un certificado de autenticación de servidor instalado en el almacén del equipo de la puerta de enlace ligera de ATA en el almacén del equipo local. Dicho certificado debe ser de confianza para el Centro ATA.

## Consola de ATA
El acceso a la consola de ATA se efectúa a través de un explorador. Se admiten los siguientes:

-   Internet Explorer 10 y versiones posteriores

-   Google Chrome 40 y versiones posteriores

-   Resolución de ancho de pantalla mínima de 1700 píxeles

## Véase también

- [Arquitectura de ATA](ata-architecture.md)
- [Instalación de ATA](/advanced-threat-analytics/deploy-use/install-ata)
- [¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)



<!--HONumber=May16_HO4-->


