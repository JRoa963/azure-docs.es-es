---
title: Administrar los datos de usuario encontrados en una investigación de Azure Security Center | Microsoft Docs
description: " Obtenga información sobre la administración de los datos de usuario localizados mediante la característica de investigación de Azure Security Center. "
services: operations-management-suite
documentationcenter: na
author: rkarlin
manager: barbkess
editor: ''
ms.assetid: 411d7bae-c9d4-4e83-be63-9f2f2312b075
ms.service: operations-management-suite
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/20/2018
ms.author: rkarlin
ms.openlocfilehash: bec9be627937913c268d65bb6cdadcf68c7a3fb4
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "60909220"
---
# <a name="manage-user-data-found-in-an-azure-security-center-investigation"></a>Administrar los datos de usuario encontrados en una investigación de Azure Security Center
En este artículo se proporciona información sobre cómo administrar los datos de usuario que se encuentran en la característica de investigación de Azure Security Center. Datos de investigación se almacenan en [registros de Azure Monitor](../log-analytics/log-analytics-overview.md) y expone en el centro de seguridad. La administración de los datos de usuario incluye la capacidad de eliminar o exportar datos.

[!INCLUDE [gdpr-intro-sentence.md](../../includes/gdpr-intro-sentence.md)]

## <a name="searching-for-and-identifying-personal-data"></a>Búsqueda e identificación de datos personales
En Azure Portal, puede usar la [característica de investigación](../security-center/security-center-investigation.md) de Security Center para buscar datos personales. La característica de investigación está disponible en **Alertas de seguridad**.

La característica de investigación muestra todas las entidades, la información de usuario y los datos en la pestaña **Entidades**.

## <a name="securing-and-controlling-access-to-personal-information"></a>Protección y control del acceso a la información personal
Un usuario de Security Center que tenga asignado el rol Lector, Propietario, Colaborador o Administrador de cuenta puede acceder a los datos del cliente dentro de la herramienta.

Vea [Roles integrados para el control de acceso basado en roles de Azure](../role-based-access-control/built-in-roles.md) para obtener más información sobre los roles Lector, Propietario y Colaborador. Vea [Administradores de la suscripción de Azure](../billing/billing-add-change-azure-subscription-administrator.md) para obtener más información sobre el rol Administrador de cuenta.

## <a name="deleting-personal-data"></a>Eliminación de datos personales
Un usuario de Security Center que tenga asignado el rol Propietario, Colaborador o Administrador de cuenta puede eliminar la información de investigación.

Para eliminar una investigación, puede enviar una solicitud `DELETE` a API de REST de Azure Resource Manager:

```HTTP
DELETE
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.OperationalInsights/workspaces/{workspaceName}/features/security/incidents/{incidentName}
```

Para encontrar la entrada `incidentName`, enumere todos los incidentes con una solicitud `GET`:

```HTTP
GET
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.OperationalInsights/workspaces/{workspaceName}/features/security/incidents
```

## <a name="exporting-personal-data"></a>Exportación de datos personales
Un usuario de Security Center que tenga asignado el rol Propietario, Colaborador o Administrador de cuenta puede exportar la información de investigación. Para exportar información de investigación, vaya a la pestaña **Entidades** para copiar y pegar la información pertinente.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre la administración de datos de usuario, vea [Administrar datos de usuario en Azure Security Center](security-center-privacy.md).
Para más información acerca de cómo eliminar datos privados en los registros de Azure Monitor, consulte [cómo exportar y eliminar datos privados](../azure-monitor/platform/personal-data-mgmt.md#how-to-export-and-delete-private-data).
