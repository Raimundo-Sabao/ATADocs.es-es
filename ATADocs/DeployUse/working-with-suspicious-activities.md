---
# required metadata

title: Trabajar con actividades sospechosas | Microsoft Advanced Threat Analytics
description: Se describe cómo revisar las actividades sospechosas identificadas por ATA
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 44d7c899-816c-4f7f-91d3-84a09d291a24

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Trabajar con actividades sospechosas
En este tema se explican los conceptos básicos para trabajar con Advanced Threat Analytics.

## Revisar las actividades sospechosas en la escala de tiempo de ataque
Después de iniciar sesión la consola de ATA, verá automáticamente la **escala de tiempo de actividades sospechosas** abiertas. Las actividades sospechosas se muestran en orden cronológico, empezando por las más recientes al principio de la escala.
Cada actividad sospechosa va acompañada de la siguiente información:

-   Entidades involucradas (usuarios, equipos, servidores, controladores de dominio y recursos).

-   Horas y período de tiempo de las actividades sospechosas.

-   Gravedad de la actividad sospechosa (alta, media o baja).

-   Estado (abierta, resuelta o descartada).

-   Posibilidad de hacer lo siguiente:

    -   Compartir la actividad sospechosa por correo electrónico con otras personas de la organización.

    -   Exportar la actividad sospechosa a Excel.

    -   Agregar una nota a la actividad sospechosa.

    -   Proporcionar información sobre la actividad sospechosa.

-   Recomendaciones sobre cómo actuar frente a la actividad sospechosa.

> [!NOTE]
> -   Si mueve el puntero del mouse sobre un usuario o un equipo, verá un miniperfil de entidad con más información sobre esa entidad y el número de actividades sospechosas relacionadas con ella.
> -   Si hace clic en una entidad, se le llevará al perfil de entidad del usuario o del equipo.

![Imagen de escala de tiempo de actividades sospechosas de ATA](media/ATA-Suspicious-Activity-Timeline.JPG)

## Filtrar la lista de actividades sospechosas
Para filtrar la lista de actividades sospechosas:

1.  En el panel **Filtrar por** situado a la izquierda de la pantalla, seleccione una de las siguientes opciones: **Todas**, **Abiertas**, **Resueltas** o **Descartadas**.

2.  Para filtrar la lista aún más, seleccione **Alta**, **Media** o **Baja**.

**Gravedad de la actividad sospechosa**

-   **Bajo**

    Señala las actividades sospechosas que pueden desembocar en ataques diseñados para que un usuario o software malintencionado tenga acceso a los datos de la organización.

-   **Mediana**

    Señala las actividades sospechosas que pueden poner a determinadas identidades en riesgo de sufrir ataques más graves que culminen en un robo de identidad o en una escalación de privilegios.

-   **Alto**

    Señala las actividades sospechosas que pueden derivar en un robo de identidad, una escalación de privilegios u otros ataques de gran impacto.

**Estado de la actividad sospechosa**

-   **Abrir**

    En esta lista figuran todas las actividades sospechosas nuevas.

-   **Resuelto**

    Sirve para llevar un seguimiento de las actividades sospechosas detectadas, investigadas y corregidas.

    > [!NOTE]
    > ATA puede volver a abrir una actividad resuelta si esa misma actividad se detecta de nuevo en un breve período de tiempo.

-   **Descartadas**

    Son actividades que se descartan manualmente. Si ATA detecta una actividad sospechosa similar, se creará una detección.

## Proporcionar información sobre una actividad sospechosa
Para que ATA obtenga información sobre la red a través de sus usuarios, algunas actividades sospechosas (reconocimiento de DNS, pass-the-ticket, enumeración de sesiones SMB, comportamientos anómalos y ejecución remota) requieren que dichos usuarios especifiquen información. De este modo, las futuras detecciones de actividades sospechosas serán mejores.

1.  En las actividades sospechosas que permiten aportar información, la pregunta de entrada se abre automáticamente. Se le pedirá que responda preguntas sobre las actividades de la red y si deben considerarse o no sospechosas. En el siguiente ejemplo, se pregunta si se pueden ejecutar herramientas de exploración en un equipo concreto.

    ![Imagen de entrada de información de actividades sospechosas en ATA](media/ATA-Input.JPG)

2.  Si la respuesta es no, esta actividad se considerará sospechosa y cada vez que ATA la detecte en este equipo, recibirá una alerta.

3.  Sin embargo, si la respuesta es sí, la actividad sospechosa se puede descartar, de modo que las actividades futuras de este tipo que se produzcan en este equipo no generarán una actividad sospechosa o generarán una actividad que se descarta automáticamente.

4.  Si no lo tiene claro, puede hacer clic en **Cancelar**.

## Cambiar el estado de una actividad sospechosa
Para cambiar el estado de una actividad sospechosa, haga clic en el estado actual de la actividad sospechosa y seleccione **Abierta**, **Resuelta** o **Descartada**.

## Véase también
- [¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Trabajar con la configuración de detección de ATA](working-with-detection-settings.md)
- [Modifying ATA configuration (Cambiar la configuración de ATA)](modifying-ata-configuration.md)


<!--HONumber=May16_HO1-->


