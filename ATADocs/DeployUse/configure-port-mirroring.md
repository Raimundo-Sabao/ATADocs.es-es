---
# required metadata

title: Configurar la creación de reflejo del puerto | Microsoft Advanced Threat Analytics
description: Describe las opciones de creación de reflejo del puerto y cómo configurarlas para ATA
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: cdaddca3-e26e-4137-b553-8ed3f389c460

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Configurar la creación de reflejo del puerto
> [!NOTE] Este artículo solo es relevante si implementa puertas de enlace de ATA en lugar de puertas de enlace ligeras de ATA. Para determinar si tiene que usar puertas de enlace de ATA, consulte [Choosing the right gateways for your deployment (Elección de las puertas de enlace adecuadas para la implementación)](/advanced-threat-analytics/plan-design/ata-capacity-planning#Choosing-the-right-gateway-type-for-your-deployment)
 
El origen de datos principal que usa ATA es la inspección profunda de paquetes del tráfico de red hacia y desde los controladores de dominio. Para que ATA vea el tráfico de red, debe configurar la creación de reflejo del puerto o usar un TAP de red.

En el caso de la creación de reflejo del puerto, configure la **creación de reflejo del puerto** para cada controlador de dominio que quiera supervisar como **origen** del tráfico de red. Normalmente, para configurar la creación de reflejo del puerto tendrá que colaborar con el equipo de virtualización o de redes.
Para más información, consulte la documentación del proveedor.

Los controladores de dominio y las puertas de enlace de ATA pueden ser físicos o virtuales. A continuación se indican los métodos comunes para la creación de reflejo del puerto y algunas consideraciones. Consulte la documentación del servidor de virtualización o del conmutador para obtener más información. El fabricante del conmutador podría usar una terminología diferente.

**Analizador de puerto conmutado (SPAN)**: copia el tráfico de red de uno o más puertos de conmutador a otro puerto de conmutador en el mismo conmutador. Tanto la puerta de enlace de ATA como los controladores de dominio deben estar conectados al mismo conmutador físico.

**Analizador de puerto conmutado remoto (RSPAN)**: permite supervisar el tráfico de red de puertos de origen distribuidos entre varios conmutadores físicos. RSPAN copia el tráfico de origen en una VLAN especial configurada para RSPAN. Esta VLAN debe ser troncal a los demás modificadores pertinentes. RSPAN funciona en el nivel 2.

**Analizador de puerto conmutado remoto encapsulado (ERSPAN)**: se trata de una tecnología de Cisco que funciona en el nivel 3. ERSPAN permite supervisar el tráfico en los conmutadores sin necesidad de troncos de VLAN. ERSPAN usa la encapsulación de enrutamiento genérico (GRE) para copiar el tráfico de red supervisado. En la actualidad ATA no puede recibir tráfico ERSPAN directamente. Para que ATA funcione con tráfico ERSPAN, es necesario que un conmutador o enrutador que pueda desencapsular el tráfico se configure como destino de ERSPAN donde se desencapsulará el tráfico. Después habrá que configurar el conmutador o enrutador para que lo reenvíe a la puerta de enlace de ATA con SPAN o RSPAN.

> [!NOTE]
> Si el controlador de dominio de cuyo puerto se va a crear un reflejo está conectado mediante un vínculo WAN, asegúrese de que dicho vínculo puede controlar la carga adicional de tráfico ERSPAN.

## Opciones de creación de reflejo del puerto admitidas

|Puerta de enlace de ATA|Controlador de dominio|Consideraciones|
|---------------|---------------------|------------------|
|Las máquinas|Virtual en el mismo host|El conmutador virtual debe admitir la creación de reflejo del puerto.<br /><br />Si se mueve una de las máquinas virtuales a otro host, podría dañarse la creación de reflejo del puerto.|
|Las máquinas|Virtual en hosts diferentes|Asegúrese de que el conmutador virtual admite este escenario.|
|Las máquinas|virtuales físicas|Requiere un adaptador de red dedicado. En caso contrario, ATA verá todo el tráfico que entra y sale del host, incluido el tráfico que envía al Centro ATA.|
|virtuales físicas|Las máquinas|Asegúrese de que el conmutador virtual admite este escenario y la configuración de la creación de reflejo del puerto en los conmutadores físicos en función del escenario:<br /><br />Si el host virtual está en el mismo conmutador físico, debe configurar un intervalo de nivel de conmutador.<br /><br />Si el host virtual está en un conmutador diferente, debe configurar RSPAN o ERSPAN&#42;.|
|virtuales físicas|Físico en el mismo conmutador|El conmutador físico debe admitir SPAN/la creación de reflejo del puerto.|
|virtuales físicas|Físico en un conmutador diferente|Requiere conmutadores físicos para admitir RSPAN o ERSPAN&#42;.|
&#42; ERSPAN solo se admite cuando la desencapsulación se realiza antes de que ATA analice el tráfico.

> [!NOTE]
> Asegúrese de que los controladores de dominio y las puertas de enlace de ATA a los que se conectan estén sincronizados a intervalos de 5 minutos entre sí.

**Si trabaja con clústeres de virtualización:**

-   Para cada controlador de dominio que se ejecute en el clúster de virtualización en una máquina virtual con la puerta de enlace de ATA, configure la afinidad entre el controlador de dominio y la puerta de enlace de ATA. De este modo, cuando el controlador de dominio se mueva a otro host del clúster, la puerta de enlace de ATA lo seguirá. Esto funciona bien cuando hay pocos controladores de dominio.
> [!NOTE]
> Si el entorno admite máquina virtual a máquina virtual en hosts diferentes (RSPAN) no es necesario preocuparse por la afinidad.
> 
-   Para asegurarse de que las puertas de enlace de ATA tienen el tamaño adecuado para controlar por sí mismas la supervisión de todos los controladores de dominio, pruebe esta opción: instale una máquina virtual en cada host de virtualización e instale una puerta de enlace de ATA en cada host. Configure cada puerta de enlace de ATA para que supervise todos los controladores de dominio que se ejecutan en el clúster. De este modo, se supervisarán todos los hosts en los que se ejecutan los controladores de dominio.

Después de configurar la creación de reflejo del puerto, valide que funciona antes de instalar la puerta de enlace de ATA.

## Véase también
- [Validar la creación de reflejo del puerto](validate-port-mirroring.md)
- [Instalación de ATA](install-ata.md)
- [¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


