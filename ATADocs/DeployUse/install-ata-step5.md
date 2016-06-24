---
# required metadata

title: "Instalación de ATA: paso 5 | Microsoft Advanced Threat Analytics"
description: El paso cinco de la instalación de ATA le ayuda a configurar la puerta de enlace de ATA.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 2a5b6652-2aef-464c-ac17-c7e5f12f920f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Instalación de ATA: paso 5

>[!div class="step-by-step"] [« Paso 4](install-ata-step4.md)
[Paso 6 »](install-ata-step6.md)


## Paso 5. Configurar las opciones de puerta de enlace de ATA
Después de instalar la puerta de enlace de ATA, realice los pasos siguientes para configurar la puerta de enlace de ATA.

1.  En la consola de ATA, haga clic en **Configuración** y seleccione la página **Puertas de enlace de ATA**.

2.  Escriba la información siguiente:

  - **Descripción**: <br>Escriba una descripción de la puerta de enlace de ATA (opcional).
  - **Controladores de dominio reflejados en puerto (FQDN)** (obligatorio para la puerta de enlace de ATA, no se puede establecer para la puerta de enlace ligera de ATA): <br>Escriba el FQDN completo del controlador de dominio y haga clic en el signo más para agregarlo a la lista. Por ejemplo, **dc01.contoso.com**.<br /><br />![Imagen del FQDN de ejemplo](media/ATAGWDomainController.png)

La siguiente información se aplica a todos los servidores especificados en la lista **Controladores de dominio**: -  todos los controladores de dominio cuyo tráfico esté supervisado por la puerta de enlace de ATA mediante el reflejo de puerto deben estar incluidos en la lista **Controladores de dominio**. Si un controlador de dominio no aparece en la lista **Controladores de dominio**, la detección de actividades sospechosas podría no funcionar según lo esperado.
-   Al menos un controlador de dominio de la lista ha de ser un servidor de catálogo global. Esto permitirá que ATA resuelva los objetos de usuario y de equipo en otros dominios del bosque.

 - **Capturar adaptadores de red** (obligatorio):<br>
     - En el caso de una puerta de enlace de ATA en un servidor dedicado, seleccione los adaptadores de red que estén configurados como puerto de reflejo de destino. Estos recibirán el tráfico reflejado del controlador de dominio.
     - En el caso de una puerta de enlace ligera de ATA, deberían ser todos los adaptadores de red que se usan para la comunicación con otros equipos de la organización.

![Imagen de la configuración de las opciones de puerta de enlace](media/ATA-Config-GW-Settings.jpg)

 - **Candidato de sincronizador de dominio**<br>
Ninguna puerta de enlace de ATA establecida para ser un candidato de sincronizador de dominio puede ser responsable de la sincronización entre ATA y el dominio de Active Directory. Según el tamaño del dominio, la sincronización inicial puede tardar algún tiempo y consume muchos recursos. De forma predeterminada, solo las puertas de enlace de ATA se establecen como candidatos de sincronizador de dominio. <br>Se recomienda deshabilitar las puertas de enlace de ATA de sitio remoto como candidatas de sincronizador de dominio.<br>Si el controlador de dominio es de solo lectura, no lo establezca como candidato de sincronizador de dominio. Para obtener más información, consulte [ATA architecture (Arquitectura de ATA)](/advanced-threat-analytics/plan-design/ata-architecture#ata-lightweight-gateway-features)

> [!NOTE] El servicio de puerta de enlace de ATA tardará unos minutos en iniciarse por primera vez, ya que crea la memoria caché de los analizadores de captura de red.<br>
Los cambios de configuración se aplicarán a la puerta de enlace de ATA en la próxima sincronización programada entre la puerta de enlace de ATA y el Centro ATA.



    

3. Opcionalmente, puede establecer la [recopilación de escucha de Syslog y de reenvío de eventos de Windows](configure-event-collection.md). 
4. Habilite **Actualizar la puerta de enlace de ATA automáticamente** para que en próximas versiones, cuando actualice el centro ATA, esta puerta de enlace de ATA se actualice automáticamente.
3.  Haga clic en **Guardar**.


## Validar instalaciones
Para validar que la puerta de enlace de ATA se ha implementado correctamente, compruebe lo siguiente:

1.  Compruebe que el servicio denominado **Microsoft Advanced Threat Analytics Gateway** se esté ejecutando. Después de guardar la configuración de la puerta de enlace de ATA, el servicio podría tardar unos minutos en iniciarse.

2.  Si el servicio no se inicia, revise el archivo "Microsoft.Tri.Gateway-Errors.log" que se encuentra en la carpeta predeterminada "%Archivos de programa%\Microsoft Advanced Threat Analytics\Gateway\Logs".

3.  Consulte [ATA Troubleshooting (Solución de problemas de ATA)](/advanced-threat-analytics/troubleshoot/troubleshooting-ata-known-errors) para obtener ayuda.

4.  Si se trata de la primera puerta de enlace de ATA que se instala, deje que pasen unos minutos, inicie sesión en la consola de ATA y abra el panel de notificación deslizando el lado derecho de la pantalla. Debería ver una lista de **Entidades descubiertas recientemente** en la barra de notificación en el lado derecho de la consola.

5.  En el escritorio, haga clic en el acceso directo **Microsoft Advanced Threat Analytics** para conectarse a la consola de ATA. Inicie sesión con las mismas credenciales de usuario que usó para instalar el Centro ATA.
6.  En la consola, busque algo en la barra de búsqueda, como un usuario o un grupo del dominio.
7.  Abra el Monitor de rendimiento. En el árbol de rendimiento, haga clic en **Monitor de rendimiento** y luego haga clic en el icono del signo más para **Agregar un contador**. Expanda **Puerta de enlace de Microsoft ATA**, desplácese hacia abajo hasta **Mensajes capturados PEF de NetworkListener/s** y agréguelo. A continuación, asegúrese de que ve actividad en el gráfico.

    ![Imagen de adición de contadores de rendimiento](media/ATA-performance-monitoring-add-counters.png)


>[!div class="step-by-step"] [« Paso 4](install-ata-step4.md)
[Paso 6 »](install-ata-step6.md)

## Véase también

- [¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Configurar la recopilación de eventos](configure-event-collection.md)
- [Requisitos previos de ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=May16_HO3-->


