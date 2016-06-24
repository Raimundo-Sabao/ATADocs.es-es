---
# required metadata

title: Planeación de la implementación de ATA | Microsoft Advanced Threat Analytics
description: Le ayuda a planear la implementación y a decidir cuántos servidores de ATA van a ser necesarios en su red
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 279d79f2-962c-4c6f-9702-29744a5d50e2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Planeamiento de la capacidad de ATA
Este tema le ayudará a determinar cuántos servidores de ATA se necesitarán en su red, incluidas la comprensión de cuántas puertas de enlace de ATA y puertas de enlace ligeras de ATA necesita y la capacidad del servidor para el Centro ATA y las puertas de enlace de ATA.

## Evaluación del tamaño del centro ATA
El centro ATA requiere un mínimo de 30 días de acumulación de datos para poder analizar el comportamiento de los usuarios. Aquí se especifica el espacio en disco necesario para la base de datos de ATA por cada controlador de dominio. Si tiene varios controladores de dominio, sume el espacio en disco requerido por cada controlador de dominio para calcular la cantidad total de espacio necesario para la base de datos de ATA.

|Paquetes por segundo&#42;|CPU (núcleos&#42;&#42;)|Memoria (GB)|Almacenamiento de base de datos por día (GB)|Almacenamiento de base de datos por mes (GB)|E/S por segundo& #42; & #42; & #42;|
|---------------------------|-------------------------|-------------------|---------------------------------|-----------------------------------|-----------------------------------|
|1.000|2|32|0,3|9|30 (100)
|10,000|4|48|3|90|200 (300)
|40,000|8|64|12|360|500 (1,000)
|100,000|12|96|30|900|1,000 (1,500)
|400.000|40|128|120|1,800|2,000 (2,500)
& #42;Número medio diario total de paquetes por segundo de todos los controladores de dominio supervisados por todas las puertas de enlace de ATA.

& #42; & #42;Esto incluye los núcleos físicos, no los núcleos con Hyper-Threading.

& #42; & #42; & #42;Promedios (Cantidades máximas)
> [!NOTE]
> -   El Centro ATA puede controlar un máximo agregado de 400 000 fotogramas por segundo (FPS) de todos los controladores de dominio supervisados.
> -   Las cantidades de almacenamiento aquí indicadas son valores netos. Tenga siempre en cuenta el crecimiento futuro y procure que el disco en el que reside la base de datos tenga al menos un 20 % de espacio libre.
> -   Si el espacio libre alcanza un mínimo del 20 % o 100 GB, se eliminará la colección de datos más antigua. Esto seguirá ocurriendo hasta que solo haya dos días de datos o un 5 % o 50 GB de espacio libre, momento en el que la recopilación de datos se detendrá.
> -  La latencia del almacenamiento de las actividades de lectura y escritura debe ser inferior a 10 ms.
> -  La proporción entre las actividades de lectura y escritura es de aproximadamente 1:3 por debajo de los 100 000 paquetes por segundo y de 1:6 por encima de los 100 000 paquetes por segundo.

## Elegir el tipo de puerta de enlace correcto para la implementación
Se recomienda que use una puerta de enlace ligera de ATA en lugar de una puerta de enlace de ATA siempre que sea posible, siempre y cuando los controladores de dominio cumplan con la tabla de tamaños que se enumera a continuación.
La mayoría de los controladores de dominio pueden y deben estar cubiertos por la puerta de enlace ligera de ATA a menos que los controladores de dominio no se ajusten a los requisitos de la [tabla de tamaños de la puerta de enlace ligera de ATA](#ata-lightweight-gateway-sizing).
A continuación, se exponen ejemplos de escenarios en los que las puertas de enlace ligeras de ATA deberían cubrir todos los controladores de dominio:

-   Sucursales
-   Controladores de dominio virtuales de cualquier proveedor de IaaS


## Tamaño de la puerta de enlace ligera de ATA
Se recomienda que use una puerta de enlace ligera de ATA en lugar de una puerta de enlace de ATA siempre que sea posible, siempre y cuando los controladores de dominio cumplan con la tabla de tamaños que se enumera aquí.

Una puerta de enlace ligera de ATA puede admitir la supervisión de un controlador de dominio según la cantidad de tráfico de red que genera el controlador de dominio. 

|Paquetes por segundo&#42;|CPU (núcleos&#42;&#42;)|Memoria (GB)&#42;&#42;&#42;|
|---------------------------|-------------------------|---------------|
|1.000|2|6|
|5 000|6|16|
    |10,000|10|24|

&#42;Número total de paquetes por segundo en el controlador de dominio supervisados por la puerta de enlace ligera de ATA específica.

&#42;&#42;Cantidad total de núcleos que no funcionen con Hyper Threading que tiene instalada el controlador de dominio.<br>Aunque Hyper Threading es aceptable para la puerta de enlace ligera de ATA, al planear la capacidad, debe contar núcleos reales y no núcleos que funcionan con Hyper Threading.

&#42;&#42;&#42;Cantidad total de memoria que tiene instalada el controlador de dominio.
> [!NOTE]   Si el controlador de dominio no tiene la cantidad necesaria de recursos que requiere la puerta de enlace ligera de ATA, no se verá afectado el rendimiento del controlador de dominio, pero la puerta de enlace ligera de ATA podría no funcionar según lo esperado.


## Evaluación del tamaño de la puerta de enlace de ATA

Tenga en cuenta lo siguiente al decidir cuántas puertas de enlace de ATA necesita implementar.

La mayoría de los controladores de dominio pueden estar cubiertos por una puerta de enlace ligera de ATA, que debe planearse según la tabla de tamaños de puerta de enlace ligera de ATA anterior.

Si las puertas de enlace de ATA siguen siendo necesarias, estas son las consideraciones sobre cuántas puertas de enlace de ATA se necesitan:<br>

-   **Bosques y dominios de Active Directory**<br>
    ATA puede supervisar el tráfico de varios dominios de un único bosque de Active Directory. Para supervisar varios bosques de Active Directory se necesitan implementaciones de ATA independientes. No se recomienda configurar una única implementación de ATA para supervisar el tráfico de red de controladores de dominio de diferentes bosques.

-   **Duplicación de puertos**<br>
Consideraciones sobre la creación de reflejo del puerto pueden requerir que implemente varias puertas de enlace de ATA por centro de datos o sucursal.

-   **Capacidad**<br>
    Una puerta de enlace de ATA permite supervisar varios controladores de dominio, según la cantidad de tráfico de red hacia y desde los controladores de dominio bajo supervisión. 
<br>

|Paquetes por segundo&#42;|CPU (núcleos&#42;&#42;)|Memoria (GB)|
|---------------------------|-------------------------|---------------|
|1.000|1|6|
|5 000|2|10|
|10,000|3|12|
|20,000|6|24|
|50.000|16|48|
&#42;Número medio total de paquetes por segundo de todos los controladores de dominio supervisados por la puerta de enlace de ATA específica durante la hora del día más ocupada.

& #42; La cantidad total del tráfico con puerto reflejado del controlador de dominio no puede superar la capacidad de la NIC de captura en la puerta de enlace de ATA.

& #42; & #42;Hyper-Threading debe estar deshabilitado.



## Estimación del tráfico del controlador de dominio
Hay varias herramientas que puede usar para detectar el promedio de paquetes por segundo de los controladores de dominio. Si no dispone de herramientas que lleven un seguimiento de este contador, puede usar el Monitor de rendimiento para recopilar la información necesaria.

Para averiguar el número de paquetes por segundo, haga lo siguiente en cada controlador de dominio:

1.  Abra el Monitor de rendimiento.

    ![Imagen del Monitor de rendimiento](media/ATA-traffic-estimation-1.png)

2.  Expanda **Conjuntos de recopiladores de datos**.

    ![Imagen de Conjuntos de recopiladores de datos](media/ATA-traffic-estimation-2.png)

3.  Haga clic con el botón derecho en **Definido por el usuario** y seleccione **Nuevo** &gt; **Conjunto de recopiladores de datos**.

    ![Imagen de nuevo conjunto de recopiladores de datos](media/ATA-traffic-estimation-3.png)

4.  Escriba un nombre para el conjunto de recopiladores y seleccione **Crear manualmente (avanzado)**.

5.  En **¿Qué tipo de datos desea incluir?**, seleccione **Crear registros de datos - Contador de rendimiento**.

    ![Imagen de tipo de datos del nuevo conjunto de recopiladores de datos](media/ATA-traffic-estimation-5.png)

6.  En **¿Qué contadores de rendimiento desea registrar?**, haga clic en **Agregar**.

7.  Expanda **Adaptador de red**, seleccione **Paquetes/s** y seleccione la instancia adecuada. Si no está seguro, puede seleccionar **&lt;Todas las instancias&gt;** y hacer clic en **Agregar** y **Aceptar**.

    > [!NOTE] Para ello, en una línea de comandos, ejecute `ipconfig /all` para ver el nombre del adaptador y la configuración.

    ![Imagen de adición de contadores de rendimiento](media/ATA-traffic-estimation-7.png)

8.  Cambie el **Intervalo de muestra** a **1 segundo**.

9. Indique la ubicación en la que quiera guardar los datos.

10. En **¿Desea crear el conjunto de recopiladores de datos?**, seleccione **Iniciar ahora este conjunto de recopiladores de datos** y haga clic en **Finalizar**.

    De este modo, ahora debería ver el conjunto de recopiladores de datos que acaba de crear con un triángulo verde, señal de que funciona.

11. Transcurridas 24 horas, detenga el conjunto de recopiladores de datos; para ello, haga clic con el botón derecho en él y seleccione **Detener**.

    ![Imagen de detención del conjunto de recopiladores de datos](media/ATA-traffic-estimation-12.png)

12. En el Explorador de archivos, vaya a la carpeta donde guardó el archivo .blg y haga doble clic en él para abrirlo en el Monitor de rendimiento.

13. Seleccione el contador Paquetes/s y registre los valores promedio y máximo.

    ![Imagen del contador Paquetes/s](media/ATA-traffic-estimation-14.png)

## Véase también
- [Requisitos previos de ATA](ata-prerequisites.md)
- [Arquitectura de ATA](ata-architecture.md)
- [¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


