---
title: Seleccionar un dominio de Internet de empresa a un nombre de dominio de Azure Traffic Manager
description: Este artículo le ayudará a que el nombre de dominio de la empresa indique un nombre de dominio del Administrador de tráfico.
services: traffic-manager
author: kumudd
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: kumud
ms.openlocfilehash: 77a5fbab6ecda910750ab2b8bae987e77607223a
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "60329707"
---
# <a name="point-a-company-internet-domain-to-an-azure-traffic-manager-domain"></a>Hacer que un dominio de Internet de la compañía indique un dominio de Azure Traffic Manager

Cuando se crea un perfil de Traffic Manager, Azure asigna automáticamente un nombre DNS para ese perfil. Para usar un nombre de la zona DNS, cree un registro DNS CNAME que se asigne al nombre de dominio de su perfil de Traffic Manager. Puede encontrar el nombre de dominio de Traffic Manager en la sección **General** de la página Configuración del perfil de Traffic Manager.

Por ejemplo, para señalar el nombre `www.contoso.com` al nombre DNS de Traffic Manager `contoso.trafficmanager.net`, cree el registro de recursos DNS siguiente:

    www.contoso.com IN CNAME contoso.trafficmanager.net

Todo el tráfico de las solicitudes a *www\.contoso.com* dirigidos a *contoso.trafficmanager.net*.

> [!IMPORTANT]
> No puede hacer que un dominio de segundo nivel como por ejemplo *contoso.com*, indique el dominio del Administrador de tráfico. Los estándares de protocolo DNS no permiten registros CNAME para nombres de dominio de segundo nivel.

## <a name="next-steps"></a>Pasos siguientes

* [Métodos de enrutamiento del Administrador de tráfico](traffic-manager-routing-methods.md)
* [Administrador de tráfico: deshabilitación, habilitación o eliminación de un perfil](disable-enable-or-delete-a-profile.md)
* [Administrador de tráfico: deshabilitación o habilitación de un extremo](disable-or-enable-an-endpoint.md)
