---
# required metadata

title: Solución de problemas del registro de errores de ATA | Microsoft Advanced Threat Analytics
description: Se explica cómo solucionar los errores comunes de ATA 
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Solución de problemas del registro de errores de ATA
En esta sección se detallan los posibles errores en las implementaciones de ATA y los pasos necesarios para solucionarlos.
## Errores de la puerta de enlace de ATA
|Error de :|Descripción|Solución|
|-------------|----------|---------|
|System.DirectoryServices.Protocols.LdapException: Error local|La puerta de enlace de ATA no pudo autenticarse en el controlador de dominio.|1. Confirme que el registro DNS del controlador de dominio está configurado correctamente en el servidor DNS. <br>2. Compruebe que la hora de la puerta de enlace de ATA está sincronizada con la del controlador de dominio.|
|System.IdentityModel.Tokens.SecurityTokenValidationException: No se pudo validar la cadena de certificados|La puerta de enlace de ATA no pudo validar el certificado del centro ATA.|1. Compruebe que el certificado de CA raíz está instalado en el almacén de certificados de la entidad de certificación de confianza en la puerta de enlace de ATA. <br>2. Compruebe que la lista de revocación de certificados (CRL) está disponible y que se puede realizar la validación de la revocación de certificados.|
|Microsoft.Common.ExtendedException: No se pudo redistribuir el tiempo generado|La puerta de enlace de ATA no pudo analizar mensajes de Syslog reenviados desde SIEM.|Compruebe que SIEM está configurado para reenviar los mensajes en uno de los formatos compatibles con ATA.|
|System.ServiceModel.FaultException: Error al comprobar la seguridad del mensaje.|La puerta de enlace de ATA no pudo autenticarse en el centro ATA.|Compruebe que la hora de la puerta de enlace de ATA está sincronizada con la del centro ATA.|
|System.ServiceModel.EndpointNotFoundException: No se pudo conectar con net.tcp://center.ip.addr:443/IEntityReceiver|La puerta de enlace de ATA no pudo establecer conexión con el centro ATA.|Asegúrese de que la configuración de red es correcta y de que la conexión de red entre la puerta de enlace de ATA y el centro ATA está activa.|
|System.DirectoryServices.Protocols.LdapException: El servidor LDAP no está disponible.|La puerta de enlace de ATA no pudo consultar al controlador de dominio con el protocolo LDAP.|1. Compruebe que la cuenta de usuario usada por ATA para conectarse al dominio de Active Directory tiene acceso de lectura a todos los objetos del árbol de Active Directory. <br>2. Asegúrese de que el controlador de dominio no está protegido para evitar consultas LDAP de la cuenta de usuario usada por ATA.|
|Microsoft.Tri.Infrastructure.ContractException: Excepción de contrato|La puerta de enlace de ATA no pudo sincronizar la configuración del centro ATA.|Realice la configuración de la puerta de enlace de ATA en la consola de ATA.|
|System.Reflection.ReflectionTypeLoadException: No se pueden cargar uno o varios tipos requeridos. Recupere la propiedad LoaderExceptions para obtener más información.|El Analizador de mensajes está instalado en la puerta de enlace de ATA.| Desinstale el Analizador de mensajes.|
|Error [Diseño] System.OutOfMemoryException: Se produjo una excepción de tipo 'System.OutOfMemoryException'.|La puerta de enlace de ATA no tiene suficiente memoria.|Aumente la cantidad de memoria en el controlador de dominio.|
|Error al iniciar el consumidor activo ---> Microsoft.Opn.Runtime.Monitoring.MessageSessionException: El proveedor de eventos de PEFNDIS no está listo|PEF (Analizador de mensajes) no se instaló correctamente.|Póngase en contacto con soporte técnico para encontrar una solución.|
|Error de instalación: 0x80070652|Hay otras instalaciones pendientes en el equipo.|Espere a que las demás instalaciones finalicen y, si es necesario, reinicie el equipo.|

## Errores de la consola de ATA
|Error de :|Descripción|Solución|
|-------------|----------|---------|
|Error HTTP 500.19: Error interno del servidor|El módulo URL Rewrite para IIS no se pudo instalar correctamente.|Desinstale y vuelva a instalar el módulo URL Rewrite para IIS.<br>[Descargue el módulo URL Rewrite para IIS](http://go.microsoft.com/fwlink/?LinkID=615137)|

## Errores de implementación
|Error de :|Descripción|Solución|
|-------------|----------|---------|
|Se produce un error en la instalación de .Net Framework 4.6.1 con identificador 0x800713ec|Los requisitos previos para .Net Framework 4.6.1 no están instalados en el servidor. |Antes de instalar ATA, compruebe que las actualizaciones de Windows [KB2919442](https://www.microsoft.com/en-us/download/details.aspx?id=42135) y [KB2919355](https://support.microsoft.com/en-us/kb/2919355) están instaladas en el servidor.|

![Imagen de error de instalación de .NET de ATA](media/netinstallerror.png)


## Véase también
- [Requisitos previos de ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Planeamiento de la capacidad de ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Configurar la recopilación de eventos](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Configurar el reenvío de eventos de Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#ATA_event_WEF)
- [¡Visite el foro de ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO4-->


