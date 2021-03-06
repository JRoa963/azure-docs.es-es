---
title: ¿Qué son las notificaciones de mantenimiento del servicio de Azure?
description: Las notificaciones de mantenimiento del servicio permiten ver los mensajes de mantenimiento del servicio que publica Microsoft Azure.
author: dkamstra
services: monitoring
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 4/12/2018
ms.author: dukek
ms.subservice: logs
ms.openlocfilehash: ab4aa2f37d5a883c83b8ee09b5de6551ebf13d2e
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "60883649"
---
# <a name="view-service-health-notifications-by-using-the-azure-portal"></a>Visualización de las notificaciones de mantenimiento del servicio mediante Azure Portal

Azure publica las notificaciones de mantenimiento del servicio, que contienen información acerca de los recursos en la suscripción. Estas notificaciones son una subclase de los eventos del registro de actividad y también se pueden encontrar en el registro de actividad. En función de la clase, las notificaciones de mantenimiento del servicio pueden ser meramente informativas o pueden requerir acciones.

Hay varias clases de las notificaciones de mantenimiento del servicio:  

- **Acción requerida:** Azure puede haber observado algo inusual en su cuenta y le ayuda a remediarlo. Azure le envía una notificación en la que se detallan las acciones que debe realizar o se proporciona información sobre cómo ponerse en contacto con los equipos de ingeniería o soporte técnico de Azure.  
- **Recuperación asistida:** se ha producido un evento y los ingenieros han confirmado que todavía le afecta. El equipo de ingeniería de Azure necesitará trabajar con usted directamente para restaurar completamente los servicios.  
- **Incidente:** un evento que tiene repercusiones en el servicio está afectando a uno o varios recursos de la suscripción.  
- **Mantenimiento:** una actividad de mantenimiento planeado que puede afectar a uno o varios de los recursos de la suscripción.  
- **Información:** posibles optimizaciones que puedan ayudarle a mejorar el uso de los recursos. 
- **Seguridad:** información urgente relacionada con la seguridad de las soluciones que se ejecutan en Azure.

Cada notificación del estado de un servicio incluye datos acerca del ámbito y el impacto en los recursos. Los detalles incluyen:

Nombre de propiedad | DESCRIPCIÓN
-------- | -----------
canales nueva | Uno de los valores siguientes: **Administrador** u **Operación**.
correlationId | Normalmente, un GUID en formato de cadena. Los eventos que pertenecen a la misma acción generalmente suelen compartir el mismo valor de correlationId.
eventDataId | Identificador único de un evento.
eventName | Título del evento.
level | Nivel de un evento
resourceProviderName | Nombre del proveedor de recursos del recurso afectado.
resourceType| Tipo del recurso afectado.
subStatus | Normalmente el código de estado HTTP de la llamada REST correspondiente, pero también puede incluir otras cadenas que describen un subestado. Por ejemplo:  Correcto (código de estado HTTP: 200), Creado (código de estado HTTP: 201), Aceptado (código de estado HTTP: 202), Sin contenido (código de estado HTTP: 204), Solicitud incorrecta (código de estado HTTP: 400), No encontrado (código de estado HTTP): 404), Conflicto (código de estado HTTP: 409), Error interno del servidor (código de estado HTTP: 500), Servicio no disponible (código de estado HTTP: 503), Tiempo de espera agotado para la puerta de enlace (código de estado HTTP: 504).
eventTimestamp | Marca de tiempo de cuándo generó el evento el servicio de Azure que procesó la solicitud correspondiente al evento.
submissionTimestamp | Marca de tiempo de cuándo el evento empezó a estar disponible para las consultas.
subscriptionId | Suscripción de Azure en la que se registró este evento.
status | Cadena que describe el estado de la operación. Entre los valores habituales, se incluyen: **Started**, **In Progress**, **Succeeded**, **Failed**, **Active** y **Resolved**.
operationName | Nombre de la operación.
category | Esta propiedad es siempre **ServiceHealth**.
resourceId | Identificador de recurso del recurso afectado.
Properties.title | El título localizado de esta comunicación. El valor predeterminado es inglés.
Properties.communication | Los detalles localizados de la comunicación con el formato HTML. El valor predeterminado es inglés.
Properties.incidentType | Uno de los valores siguientes: **ActionRequired**, **Informational**, **Incident**, **Maintenance** o **Security**.
Properties.trackingId | El incidente al que está asociado este evento. Se utiliza para correlacionar los eventos relacionados con un incidente.
Properties.impactedServices | Un blob JSON con caracteres de escape que describe los servicios y regiones a los que afecta el incidente. Una lista de servicios, cada uno de los cuales tiene un valor de **ServiceName** y una lista de regiones afectadas, cada una de los cuales tiene un valor de **RegionName**.
Properties.defaultLanguageTitle | La comunicación en inglés.
Properties.defaultLanguageContent | La comunicación en inglés en formato HTML o como texto sin formato.
Properties.stage | Los valores posibles de **Incident** y **Security** son **Active**, **Resolved** o **RCA**. Para **ActionRequired** o **Informational**, el único valor posible es **Active**. En el caso de **Maintenance** son: **Active**, **Planned**, **InProgress**, **Canceled**, **Rescheduled**, **Resolved** o **Complete**.
Properties.communicationId | La comunicación con la cual está asociado este evento.

### <a name="details-on-service-health-level-information"></a>Detalles sobre la información de estado del servicio

**Action Required** (properties.incidentType == ActionRequired)
- Información: Se necesita una acción del administrador para evitar que los servicios existentes se vean afectados
    
**Maintenance** (properties.incidentType == Maintenance)
- Advertencia: mantenimiento de emergencia
- Información: mantenimiento planeado estándar

**Information** (properties.incidentType == Information)
- Información: Se necesita que el administrador para evite que los servicios existentes se vean afectados

**Security** (properties.incidentType == Security)
- Error: Problemas generalizados de acceso a varios servicios en distintas regiones que afectan a numerosos grupos de clientes.
- Advertencia: Problemas de acceso a servicios concretos o en regiones concretas que afectan a un subgrupo de clientes.
- Información: Problemas que afectan a las operaciones de administración o de latencia, sin afectar a la disponibilidad del servicio.

**Service Issues** (properties.incidentType == Incident)
- Error: Problemas generalizados de acceso a varios servicios en distintas regiones que afectan a numerosos grupos de clientes.
- Advertencia: Problemas de acceso a servicios concretos o en regiones concretas que afectan a un subgrupo de clientes.
- Información: Problemas que afectan a las operaciones de administración o de latencia, sin afectar a la disponibilidad del servicio.


## <a name="view-your-service-health-notifications-in-the-azure-portal"></a>Visualización de las notificaciones de mantenimiento del servicio en Azure Portal
1.  En [Azure Portal](https://portal.azure.com), seleccione **Supervisión**.

    ![Captura de pantalla del menú de Azure Portal, con el Monitor seleccionado](./media/service-notifications/home-monitor.png)

    Azure Monitor se abre junto con toda la configuración de supervisión y los datos en una sola vista consolidada. Primero se abre la sección **Registro de actividades** .

3.  Seleccione **Alertas**.

    ![Captura de pantalla del registro de actividad del Monitor, con Alertas seleccionado](./media/service-notifications/service-health-summary.png)
4. Seleccione **+Agregar alerta del registro de actividad** y configure una alerta para asegurarse de que recibe las futuras notificaciones del servicio. Para más información, consulte [Creación de alertas del registro de actividad en notificaciones del servicio](../../azure-monitor/platform/alerts-activity-log-service-notifications.md).

## <a name="next-steps"></a>Pasos siguientes
Reciba [notificaciones de alertas con cada notificación de mantenimiento del servicio](../../azure-monitor/platform/alerts-activity-log-service-notifications.md).  
Más información sobre las [alertas del registro de actividad](../../azure-monitor/platform/activity-log-alerts.md).

