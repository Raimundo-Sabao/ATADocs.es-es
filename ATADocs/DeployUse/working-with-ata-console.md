---
# required metadata

title: Trabajar con la consola de ATA | Microsoft Advanced Threat Analytics
description: Se explica cómo iniciar sesión en la consola de ATA y en los componentes de la consola
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 1bf264d9-9697-44b5-9533-e1c498da4f07

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Trabajar con la consola de ATA

Use la consola de ATA para supervisar las actividades sospechosas detectadas por ATA y actuar en consecuencia.

## Permitir el acceso a la consola de ATA
Cualquier usuario que sea miembro del grupo de administradores locales en el servidor del centro ATA tiene permiso para iniciar sesión en la consola de ATA y administrar la configuración de ATA.
Para que un usuario que no es administrador local pueda iniciar sesión en la consola de ATA, agréguelo al grupo local de **administradores de Microsoft Advanced Threat Analytics**.

## Iniciar sesión en la consola de ATA

1. En el servidor del centro ATA, haga clic en el icono de la **consola de Microsoft ATA** en el escritorio o abra una ventana del explorador y vaya a la consola de ATA.

    ![Icono de servidor de ATA](media/ata-server-icon.png)

    > [!NOTE] Además puede abrir una ventana del explorador desde el centro ATA o desde la puerta de enlace de ATA e ir a la dirección IP configurada en la instalación del centro ATA para la consola de ATA.    

2.  Escriba su nombre de usuario y contraseña y haga clic en **Iniciar sesión**.

![Imagen de pantalla de inicio de sesión en ATA](media/ATA-log-in-screen.jpg)

    > [!NOTE]
    > You have to log in with a user who is a member of the local administrator group OR of the Microsoft Advanced Threat Analytics Administrators group.

## La consola de ATA

La consola de ATA proporciona una vista rápida de todas las actividades sospechosas en orden cronológico. Le permite profundizar en los detalles de cualquier actividad y realizar acciones basadas en esas actividades. La consola también muestra alertas y notificaciones para resaltar los problemas existentes en la red de ATA o nuevas actividades que se consideren sospechosas.

Estos son los elementos principales de la consola de ATA.


### Escala de tiempo de ataque

Es la página de destino predeterminada que verá cuando inicie sesión en la consola de ATA. Todas las actividades sospechosas abiertas se muestran de forma predeterminada en la escala de tiempo de ataque. Esta escala de tiempo de ataque se puede filtrar para mostrar todas las actividades sospechosas o solo las que estén abiertas, descartadas o resueltas. También podrá consultar la gravedad asignada a cada actividad.

![Imagen de escala de tiempo de ataque de ATA](media/attack-timeline.png)

Para obtener más información, consulte [Working with suspicious activities (Trabajar con actividades sospechosas)](/advanced-threat-analytics/deploy-use/working-with-suspicious-activities).

### Barra de notificación

Cuando se detecte una nueva actividad sospechosa, se abrirá automáticamente la barra de notificación a la derecha. Si hay nuevas actividades sospechosas desde la última vez que inició sesión, la barra de notificación se abrirá después de haber iniciado sesión correctamente. Para acceder a ella, haga clic en la flecha situada a la derecha en cualquier momento.

![Imagen de barra de notificación de ATA](media/notification-bar.png)

### Panel de filtrado

Puede filtrar las actividades sospechosas que quiera que aparezcan en la escala de tiempo de ataque o en la pestaña de actividades sospechosas de perfil de entidad según el estado y la gravedad.

### Barra de búsqueda

En el menú superior verá una barra de búsqueda. Puede buscar un usuario, un equipo o un grupo específico en ATA. Escriba algo para hacer una prueba.

![Imagen de búsqueda en la consola de ATA](media/ATA-console-search.png)

### Centro de mantenimiento

El centro de mantenimiento muestra alertas cuando algo no funciona correctamente en la implementación de ATA.

![Imagen del centro de mantenimiento de ATA](media/health-center.png)

Cada vez que el sistema detecte un problema (como un error de conectividad o una puerta de enlace de ATA desconectada), lo sabrá porque el icono del centro de mantenimiento muestra un punto rojo. ![Imagen de punto rojo del centro de mantenimiento de ATA](media/ATA-Health-Center-Alert-red-dot.png)

Las alertas del centro de mantenimiento se pueden descartar o resolver, así como clasificarse como alta, media o baja según su gravedad. Si resuelve una alerta que el servicio de ATA aún muestra como activa, se trasladará automáticamente a la lista de alertas abiertas. Si el sistema detecta que ya no hay motivo para mostrar una alerta (la situación se ha corregido), se trasladará automáticamente a la lista de alertas resueltas.

### Perfiles de usuario y de equipo

ATA genera un perfil por cada usuario y equipo de la red. En el perfil de usuario, ATA muestra información general, como la pertenencia a grupos, los últimos inicios de sesión y los recursos a los que ha tenido acceso recientemente.

![Perfil de usuario](media/user-profile.png)

En el perfil de equipo, ATA muestra información general, como los últimos inicios de sesión y los recursos a los que se ha tenido acceso recientemente.

![Perfil de equipo](media/computer-profile.png)

ATA proporciona más información sobre las entidades (equipos, dispositivos, usuarios) en las siguientes páginas: Resumen, Actividades y Actividades sospechosas.

Los perfiles que ATA no haya podido resolver completamente se identificarán con un icono de círculo relleno hasta la mitad.


![Imagen de perfil sin resolver de ATA](media/ATA-Unresolved-Profile.jpg)

### Miniperfil

En cualquier parte de la consola donde haya una sola entidad (como un usuario o un equipo) si coloca el mouse sobre dicha entidad, se abrirá un miniperfil automáticamente con la siguiente información:

![Imagen de miniperfil de ATA](media/ATA-mini-profile.jpg)

-   Nombre

-   Imagen

-   Correo electrónico

-   Teléfono

-   Número de actividades sospechosas por gravedad



## Véase también
[¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


