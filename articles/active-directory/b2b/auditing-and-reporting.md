---
title: 'Informes de auditoría y un usuario de colaboración B2B: Azure Active Directory | Microsoft Docs'
description: Las propiedades de un usuario invitado son configurables en la colaboración B2B de Azure Active Directory.
services: active-directory
ms.service: active-directory
ms.subservice: B2B
ms.topic: conceptual
ms.date: 12/14/2018
ms.author: mimart
author: msmimart
manager: daveba
ms.reviewer: mal
ms.custom: it-pro, seo-update-azuread-jan
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5763a7e5f122702ddaf86246fbfbd18326878146
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "60357195"
---
# <a name="auditing-and-reporting-a-b2b-collaboration-user"></a>Auditoría y generación de informes para usuarios de colaboración 2B
Con usuarios invitados, cuenta con funcionalidades de auditoría similares a las que tiene con los usuarios miembros. 

## <a name="access-reviews"></a>Revisiones de acceso
Puede utilizar revisiones de acceso para comprobar periódicamente si los usuarios invitados necesitan todavía acceso a los recursos. La característica **Revisiones de acceso** está disponible en **Azure Active Directory** en **Administrar** > **Relaciones de organización**. (También puede buscar "revisiones de acceso" en **Todos los servicios** en Azure Portal). Para aprender a usar las revisiones de acceso, consulte [Administración del acceso de los invitados con las revisiones de acceso de Azure AD](../governance/manage-guest-access-with-access-reviews.md).

## <a name="audit-logs"></a>Registros de auditoría

Los registros de auditoría de Azure AD proporcionan registros de las actividades del sistema y de los usuarios, incluidas las actividades iniciadas por los usuarios invitados. Para acceder a los registros de auditoría, en **Azure Active Directory**, en **Supervisión**, seleccione **Registros de auditoría**. A continuación, se muestra un ejemplo del historial de canje e invitación de los usuario Sam Oogle al que se acaba de invitar:

![Salida de registro que muestra la captura de pantalla y un ejemplo de auditoría](./media/auditing-and-reporting/audit-log.png)

Puede profundizar en cada uno de estos eventos para obtener los detalles. Por ejemplo, echemos un vistazo a los detalles de aceptación.

![Ejemplo de salida de los detalles de actividad y que muestra la captura de pantalla](./media/auditing-and-reporting/activity-details.png)

También puede exportar estos registros de Azure AD y utilizar la herramienta de informes que prefiera para obtener informes personalizados.

### <a name="next-steps"></a>Pasos siguientes

- [Propiedades de usuario de la colaboración B2B](user-properties.md)

