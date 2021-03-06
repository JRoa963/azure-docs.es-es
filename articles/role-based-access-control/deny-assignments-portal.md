---
title: Visualización de las asignaciones de denegación de recursos de Azure mediante Azure Portal | Microsoft Docs
description: Aprenda cómo ver a usuarios, grupos, entidades de servicio e identidades administradas a los que se les ha denegado el acceso a acciones específicas en recursos de Azure en un ámbito determinado mediante Azure Portal.
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
ms.assetid: 8078f366-a2c4-4fbb-a44b-fc39fd89df81
ms.service: role-based-access-control
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/13/2019
ms.author: rolyon
ms.reviewer: bagovind
ms.openlocfilehash: 2dcbcbec9054b31312043ef6642f59fa64728b30
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "60194366"
---
# <a name="view-deny-assignments-for-azure-resources-using-the-azure-portal"></a>Visualización de las asignaciones de denegación de recursos de Azure mediante Azure Portal

Las [asignaciones de denegación](deny-assignments.md) impiden que los usuarios realicen acciones concretas en recursos de Azure, aunque una asignación de roles les conceda acceso. En este artículo se describe cómo usar Azure Portal para ver las asignaciones de denegación.

> [!NOTE]
> En este momento, la única manera de agregar sus propias asignaciones de denegación es usar Azure Blueprints. Para más información, consulte [Protect new resources with Azure Blueprints resource locks](../governance/blueprints/tutorials/protect-new-resources.md) (Protección de los nuevos recursos con bloqueos de recursos de Azure Blueprints).

## <a name="prerequisites"></a>Requisitos previos

Para obtener información sobre una asignación de denegar, debe tener:

- `Microsoft.Authorization/denyAssignments/read` permiso que se incluye en la mayoría [roles integrados para los recursos de Azure](built-in-roles.md).

## <a name="view-deny-assignments"></a>Visualización de asignaciones de denegación

Siga estos pasos para ver las asignaciones de denegación en el ámbito de la suscripción o del grupo de administración.

1. En Azure Portal, haga clic en **Todos los servicios** y, después, en **Grupos de administración** o **Suscripciones**.

1. Haga clic en el grupo de administración o suscripción que desee ver.

1. Haga clic en **Control de acceso (IAM)**.

1. Haga clic en la pestaña **Asignaciones de denegación** (o haga clic en el botón **Ver** en el icono Ver asignaciones de denegación).

    Si hay alguna asignación denegada en este ámbito o heredada de este ámbito, se enumerarán.

    ![Control de acceso: pestaña Asignaciones de denegación](./media/deny-assignments-portal/access-control-deny-assignments.png)

1. Para mostrar las columnas adicionales, haga clic en **Editar columnas**.

    ![Asignaciones de denegación: columnas](./media/deny-assignments-portal/deny-assignments-columns.png)

    |  |  |
    | --- | --- |
    | **Nombre** | Nombre de la asignación de denegación. |
    | **Tipo de entidad de seguridad** | Usuario, grupo, grupo definido por el sistema o entidad de servicio. |
    | **Se deniega**  | Nombre de la entidad de seguridad que se incluye en la asignación de denegación. |
    | **Id** | Identificador único para la asignación de denegación. |
    | **Entidades de seguridad excluidas** | Si hay entidades de seguridad que se excluyen de la asignación de denegación. |
    | **No se aplica a los elementos secundarios** | Si la asignación de denegación se hereda en los ámbitos secundarios. |
    | **Protegida por el sistema** | Si Azure administra la asignación de denegación. Actualmente, siempre es sí. |
    | **Ámbito** | Grupo de administración, suscripción, grupo de recursos o identificador de recurso. |

1. Agregue una marca de verificación a cualquiera de los elementos habilitados y, a continuación, haga clic en **Aceptar** para mostrar las columnas seleccionadas.

## <a name="view-details-about-a-deny-assignment"></a>Visualización de detalles sobre una asignación de denegación

Siga estos pasos para ver detalles adicionales sobre una asignación de denegación.

1. Abra el panel **Asignaciones de denegación**, tal como se describe en la sección anterior.

1. Haga clic en el nombre de asignación de denegación para abrir la hoja **Usuarios**.

    ![Asignación de denegación: Usuarios](./media/deny-assignments-portal/deny-assignment-users.png)

    La hoja **Usuarios** incluye las dos secciones siguientes.

    |  |  |
    | --- | --- |
    | **La asignación de denegación se aplica a**  | Entidades de seguridad a las que se aplica la asignación de denegación. |
    | **La asignación de denegación excluye** | Entidades de seguridad que se excluyen de la asignación de denegación. |

    **La entidad de seguridad definida por el sistema** representa a todos los usuarios, grupos, entidades de servicio e identidades administradas de un directorio de Azure AD.

1. Para ver una lista de los permisos que se deniegan, haga clic en **Permisos denegados**.

    ![Asignación de denegación: Permisos denegados](./media/deny-assignments-portal/deny-assignment-denied-permissions.png)

    | Tipo de acción | DESCRIPCIÓN |
    | --- | --- |
    | **Acciones**  | Operaciones de administración denegadas. |
    | **NotActions** | Operaciones de administración que se excluyen de la operación de administración denegada. |
    | **DataActions**  | Operaciones de datos denegadas. |
    | **NotDataActions** | Operaciones de datos que se excluyen de la operación de datos denegada. |

    Para el ejemplo mostrado en la captura de pantalla anterior, los siguientes son los permisos efectivos:

    - Se deniegan todas las operaciones de almacenamiento en el plano de datos, excepto las operaciones de proceso.

1. Para ver las propiedades de una asignación de denegación, haga clic en **Propiedades**.

    ![Asignación de denegación: Propiedades](./media/deny-assignments-portal/deny-assignment-properties.png)

    En la hoja **Propiedades**, puede ver el nombre, el identificador, la descripción y el ámbito de la asignación de denegación. El modificador **No se aplica a los elementos secundarios** indica si la asignación de denegación se hereda a los ámbitos secundarios. El modificador **Protegida por el sistema** indica si Azure administra esta asignación de denegación. Actualmente, es **Sí** en todos los casos.

## <a name="next-steps"></a>Pasos siguientes

* [Descripción de las asignaciones de denegación para recursos de Azure](deny-assignments.md)
* [Enumeración de las asignaciones de denegación para recursos de Azure mediante la API de REST](deny-assignments-rest.md)
