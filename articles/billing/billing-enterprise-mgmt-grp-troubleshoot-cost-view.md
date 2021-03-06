---
title: Solución de problemas de las vistas de costos empresariales de Azure | Microsoft Docs
description: Obtenga información para resolver los problemas que podría tener con vistas de costos de organización dentro de Azure Portal.
author: rthorn17
manager: adpick
editor: ''
ms.assetid: ''
ms.service: billing
ms.devlang: na
ms.topic: troubleshooting
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/22/2017
ms.author: banders
ms.custom: seodec18
ms.openlocfilehash: d35996b16d615a198b9a6039386f6b295172f388
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "60615765"
---
# <a name="troubleshoot-enterprise-cost-views"></a>Solución de problemas de vistas de costos empresariales

Dentro de las inscripciones empresariales, hay varias configuraciones que podrían provocar que los usuarios de la inscripción no pudieran ver los costos.  El administrador de inscripciones administra estas configuraciones. O bien, si la inscripción no se compró directamente a través de Microsoft, es el asociado quien administra las configuraciones.  Este artículo le ayuda a comprender cuáles son las configuraciones y de qué manera pueden afectar a la inscripción. Estas configuraciones son independientes de los roles de control de acceso basado en rol (RBAC) de Azure.

## <a name="enabling-access-to-costs"></a>Habilitación del acceso a los costos

¿Aparece un mensaje de acceso no autorizado o que dice que *las vistas de costos están deshabilitadas en su inscripción?* cuando busca información de costos?
![Captura de pantalla que muestra "no autorizado" en el campo de costo actual de la suscripción.](media/billing-enterprise-mgmt-groups/unauthorized.png)

El motivo podría ser uno de los siguientes:

1. Adquirió Azure a través de un asociado empresarial y el asociado no ha publicado aún los precios. Póngase en contacto con su asociado para que actualicen los precios en [Enterprise Portal](https://ea.azure.com).
2. Si usted es cliente directo de EA, hay un par de posibilidades:
    * Es el propietario de la cuenta y su administrador de inscripciones ha deshabilitado la opción para que el **propietario de la cuenta vea los cargos**.  
    * Es el administrador del departamento y su administrador de inscripciones ha deshabilitado la opción para que el **administrador del departamento vea los cargos**.
    * Póngase en contacto con el administrador de inscripciones para acceder. El administrador de inscripciones puede actualizar la configuración en [Enterprise Portal](https://ea.azure.com/manage/enrollment).

      ![Captura de pantalla que muestra la configuración de Enterprise Portal para ver los cargos.](media/billing-enterprise-mgmt-groups/ea-portal-settings.png)

## <a name="asset-is-unavailable"></a>Recurso no disponible

Si recibe el mensaje de error de que este recurso no está disponible al intentar acceder a una suscripción o un grupo de administración, significa que no tiene el rol correcto para ver este elemento.  

![Captura de pantalla que muestra el mensaje "recurso no disponible".](media/billing-enterprise-mgmt-groups/asset-not-found.png)

Pida acceso al administrador de suscripciones o al administrador del grupo de administración. Para saber más, vea [Administración del acceso mediante RBAC y Azure Portal](../role-based-access-control/role-assignments-portal.md).
