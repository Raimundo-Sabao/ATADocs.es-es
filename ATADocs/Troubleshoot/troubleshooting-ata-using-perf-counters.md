---
# required metadata

title: Solución de problemas de ATA con contadores de rendimiento | Microsoft Advanced Threat Analytics
description: Se explica cómo usar contadores de rendimiento para solucionar problemas de ATA
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: df162a62-f273-4465-9887-94271f5000d2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Solución de problemas de ATA con contadores de rendimiento
Los contadores de rendimiento de ATA ofrecen información sobre el rendimiento de cada componente de ATA. Los componentes de ATA procesan los datos de forma secuencial, de modo que, cuando hay un problema, provoca una reacción en cadena que se traduce en tráfico descartado. Para solucionar el problema, tendrá que averiguar qué componente falla y solucionar el problema al principio de la cadena.
Consulte [ATA architecture (Arquitectura de ATA)](/advanced-threat-analytics/plan-design/ata-architecture) para comprender el flujo de los componentes internos de ATA.

**Proceso de componente de ATA**:

1.  Cuando un componente alcanza su tamaño máximo, impide que el componente anterior pueda enviarle más entidades.

2.  Esto hará que el componente anterior acabe por aumentar **su** propio tamaño hasta impedir que su componente anterior correspondiente le envíe más entidades.

3.  Esto sucederá hasta llegar al componente NetworkListener inicial, que eliminará tráfico cuando ya no pueda reenviar entidades.

4. Use los datos encontrados en los contadores de rendimiento para entender cómo funciona cada componente.

## Contadores de rendimiento de puerta de enlace de ATA

En esta sección, todas las referencias a la puerta de enlace de ATA se refieren también a la puerta de enlace ligera de ATA.

Si quiere observar el estado del rendimiento en tiempo real de la puerta de enlace de ATA, agregue los contadores de rendimiento de la puerta de enlace del ATA.
Para ello, abra el "Monitor de rendimiento" y agregue todos los contadores de la puerta de enlace de ATA. El nombre del objeto de contador de rendimiento es "Microsoft ATA Gateway".

![Imagen de adición de contadores de rendimiento](media/ATA-performance-counters.png)

Esta es una lista de los principales contadores de puerta de enlace de ATA a los que hay que prestar atención:

|Contador|Descripción|Threshold|Solucionar problemas|
|-----------|---------------|-------------|-------------------|
|Mensajes de analizador PEF de NetworkListener/s|Cantidad de tráfico que la puerta de enlace de ATA procesa cada segundo.|Sin umbral|Ayuda a conocer la cantidad de tráfico que redistribuye la puerta de enlace de ATA.|
|Eventos quitados PEF de NetworkListener/s|Cantidad de tráfico que la puerta de enlace de ATA elimina cada segundo.|Este número debe ser cero todo el tiempo (se admiten ciertas ráfagas breves de eliminaciones).|Compruebe si alguno de los componentes ha alcanzado su tamaño máximo y está bloqueando todos los componentes anteriores hasta NetworkListener. Consulte el **proceso de componente de ATA** anterior.<br /><br />Compruebe que no hay ningún problema de CPU ni de memoria.|
|Eventos quitados ETW de NetworkListener/s|Cantidad de tráfico que la puerta de enlace de ATA elimina cada segundo.|Este número debe ser cero todo el tiempo (se admiten ciertas ráfagas breves de eliminaciones).|Compruebe si alguno de los componentes ha alcanzado su tamaño máximo y está bloqueando todos los componentes anteriores, hasta NetworkListener. Consulte el **proceso de componente de ATA** anterior.<br /><br />Compruebe que no hay ningún problema de CPU ni de memoria.|
|Tamaño de bloqueo de n.º de datos de mensaje de NetworkActivityTranslator|Cantidad de tráfico en cola para su traducción en actividades de red (NA).|Debe ser menor que el máximo -1 (valor máximo predeterminado: 100 000).|Compruebe si alguno de los componentes ha alcanzado su tamaño máximo y está bloqueando todos los componentes anteriores, hasta NetworkListener. Consulte el **proceso de componente de ATA** anterior.<br /><br />Compruebe que no hay ningún problema de CPU ni de memoria.|
|Tamaño de bloqueo de actividades de EntityResolver|Cantidad de actividades de red (NA) en cola para su resolución.|Debe ser menor que el máximo -1 (valor máximo predeterminado: 10 000).|Compruebe si alguno de los componentes ha alcanzado su tamaño máximo y está bloqueando todos los componentes anteriores, hasta NetworkListener. Consulte el **proceso de componente de ATA** anterior.<br /><br />Compruebe que no hay ningún problema de CPU ni de memoria.|
|Tamaño de bloqueo de lote de entidades de EntitySender|Cantidad de actividades de red (NA) en cola para su envío al centro ATA.|Debe ser menor que el máximo -1 (valor máximo predeterminado: 1 000 000).|Compruebe si alguno de los componentes ha alcanzado su tamaño máximo y está bloqueando todos los componentes anteriores, hasta NetworkListener. Consulte el **proceso de componente de ATA** anterior.<br /><br />Compruebe que no hay ningún problema de CPU ni de memoria.|
|Tiempo de envío de lote de EntitySender|Cantidad de tiempo que tardó en enviarse el último lote.|La mayoría de las veces, debe ser inferior a 1000 milisegundos.|Compruebe si hay algún problema de red entre la puerta de enlace de ATA y el centro ATA.|

> [!NOTE]
> -   Los contadores de tiempo se expresan en milisegundos.
> -   A veces resulta más cómodo supervisar la lista completa de contadores mediante el tipo de gráfico "Informe" (ejemplo: supervisión en tiempo real de todos los contadores).

## Contadores de rendimiento del centro ATA
Si quiere observar el estado del rendimiento en tiempo real del centro ATA, agregue los contadores de rendimiento del centro ATA.

Para ello, abra el "Monitor de rendimiento" y agregue todos los contadores del centro ATA. El nombre del objeto de contador de rendimiento es "Microsoft ATA Center".

![Adición de contadores de rendimiento del centro ATA](media/ATA-Gateway-perf-counters.png)

Esta es una lista de los principales contadores del centro ATA a los que hay que prestar atención:

|Contador|Descripción|Threshold|Solucionar problemas|
|-----------|---------------|-------------|-------------------|
|Tamaño de bloqueo de lote de entidades de EntityReceiver|Número de lotes de entidad puestos en cola por el centro ATA.|Debe ser menor que el máximo -1 (valor máximo predeterminado: 10 000).|Compruebe si alguno de los componentes ha alcanzado su tamaño máximo y está bloqueando todos los componentes anteriores, hasta NetworkListener.  Consulte el **proceso de componente de ATA** anterior.<br /><br />Compruebe que no hay ningún problema de CPU ni de memoria.|
|Tamaño de bloqueo de actividades de red de NetworkActivityProcessor|Número de actividades de red (NA) en cola para su procesamiento.|Debe ser menor que el máximo -1 (valor máximo predeterminado: 50 000).|Compruebe si alguno de los componentes ha alcanzado su tamaño máximo y está bloqueando todos los componentes anteriores, hasta NetworkListener. Consulte el **proceso de componente de ATA** anterior.<br /><br />Compruebe que no hay ningún problema de CPU ni de memoria.|
|Tamaño de bloqueo de actividades de red de EntityProfiler|Número de actividades de red (NA) en cola para la creación de perfiles.|Debe ser menor que el máximo -1 (valor máximo predeterminado: 10 000).|Compruebe si alguno de los componentes ha alcanzado su tamaño máximo y está bloqueando todos los componentes anteriores, hasta NetworkListener. Consulte el **proceso de componente de ATA** anterior.<br /><br />Compruebe que no hay ningún problema de CPU ni de memoria.|
|CenterDatabase &#42; Tamaño de bloque|Número de actividades de red, de un tipo específico, en cola para escribirse en la base de datos.|Debe ser menor que el máximo -1 (valor máximo predeterminado: 50 000).|Compruebe si alguno de los componentes ha alcanzado su tamaño máximo y está bloqueando todos los componentes anteriores, hasta NetworkListener. Consulte el **proceso de componente de ATA** anterior.<br /><br />Compruebe que no hay ningún problema de CPU ni de memoria.|


> [!NOTE]
> -   Los contadores de tiempo se expresan en milisegundos.
> -   A veces resulta más cómodo supervisar la lista completa de contadores mediante el tipo de gráfico "Informe" (ejemplo: supervisión en tiempo real de todos los contadores).

## Contadores del sistema operativo
Esta es una lista de los principales contadores del sistema operativo a los que hay que prestar atención:

|Contador|Descripción|Threshold|Solucionar problemas|
|-----------|---------------|-------------|-------------------|
|Procesador(_Total)\% Tiempo del procesador|Porcentaje de tiempo transcurrido que el procesador invierte en ejecutar un subproceso activo.|Menos del 80 % de media.|Compruebe si hay un proceso específico que esté tardando mucho más tiempo de procesador de lo que debería.<br /><br />Agregue más procesadores.<br /><br />Reduzca la cantidad de tráfico por servidor.<br /><br />El contador "Procesador(_Total)\% Tiempo del procesador" puede ser menos preciso en los servidores virtuales, en cuyo caso es preferible usar el contador "Sistema\Longitud de cola del procesador" para medir de forma más precisa la falta de energía de procesador.|
|Sistema\Cambios de contexto/s|Velocidad combinada a la que todos los procesadores cambian de un subproceso a otro.|Menos de 5000&#42; núcleos (núcleos físicos).|Compruebe si hay un proceso específico que esté tardando mucho más tiempo de procesador de lo que debería.<br /><br />Agregue más procesadores.<br /><br />Reduzca la cantidad de tráfico por servidor.<br /><br />El contador "Procesador(_Total)\% Tiempo del procesador" puede ser menos preciso en los servidores virtuales, en cuyo caso es preferible usar el contador "Sistema\Longitud de cola del procesador" para medir de forma más precisa la falta de energía de procesador.|
|Sistema\Longitud de la cola del procesador|Número de subprocesos listos para ejecutarse y en espera de ser programados.|Menos de 5&#42; núcleos (núcleos físicos).|Compruebe si hay un proceso específico que esté tardando mucho más tiempo de procesador de lo que debería.<br /><br />Agregue más procesadores.<br /><br />Reduzca la cantidad de tráfico por servidor.<br /><br />El contador "Procesador(_Total)\% Tiempo del procesador" puede ser menos preciso en los servidores virtuales, en cuyo caso es preferible usar el contador "Sistema\Longitud de cola del procesador" para medir de forma más precisa la falta de energía de procesador.|
|Memoria\MBytes disponibles|Cantidad de memoria física (RAM) disponible para asignar.|Debe ser superior a 512.|Compruebe si hay un proceso específico que esté consumiendo mucha más memoria física de lo que debería.<br /><br />Aumente la cantidad de memoria física.<br /><br />Reduzca la cantidad de tráfico por servidor.|
|LogicalDisk(&#42;)\Promedio de lecturas de disco/seg.|Latencia media para leer datos desde el disco (se recomienda seleccionar la unidad de base de datos como instancia).|Debe ser menor que 10 milisegundos.|Compruebe si hay un proceso específico que está usando la unidad de base de datos más de lo que debería.<br /><br />Consulte a su proveedor o equipo de almacenamiento si esta unidad puede enviar la carga de trabajo actual con menos de 10 ms de latencia. La carga de trabajo actual se puede determinar usando contadores de uso de disco.|
|LogicalDisk(&#42;)\Promedio de Escritura de disco/seg.|Latencia media para escribir datos en el disco (se recomienda seleccionar la unidad de base de datos como instancia).|Debe ser menor que 10 milisegundos.|Compruebe si hay un proceso específico que está usando la unidad de base de datos más de lo que debería.<br /><br />Consulte a su proveedor o equipo de almacenamiento si esta unidad puede enviar la carga de trabajo actual con menos de 10 ms de latencia. La carga de trabajo actual se puede determinar usando contadores de uso de disco.|
|\LogicalDisk(&#42;)\Lecturas de disco/s|Frecuencia de las operaciones de lectura en el disco.|Sin umbral|Los contadores de uso de disco pueden aportar más información a la hora de solucionar problemas de latencia de almacenamiento.|
|\LogicalDisk(&#42;)\Bytes de lectura de disco/s|Número de bytes por segundo que se leen desde el disco.|Sin umbral|Los contadores de uso de disco pueden aportar más información a la hora de solucionar problemas de latencia de almacenamiento.|
|\LogicalDisk(&#42;)\Escrituras de disco/s|Frecuencia de las operaciones de escritura en el disco.|Sin umbral|Los contadores de uso de disco pueden aportar más información a la hora de solucionar problemas de latencia de almacenamiento.|
|\LogicalDisk(&#42;)\Bytes de escritura de disco/s|Número de bytes por segundo que se escriben en el disco.|Sin umbral|Los contadores de uso de disco pueden aportar más información a la hora de solucionar problemas de latencia de almacenamiento.|

## Véase también
- [Requisitos previos de ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Planeamiento de la capacidad de ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Configurar la recopilación de eventos](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Configurar el reenvío de eventos de Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


