---
title: 'Script de Azure PowerShell: eliminación de un contenedor en una cuenta de Azure Cosmos'
description: 'Ejemplo de script de Azure PowerShell: eliminación de un contenedor en una cuenta de Azure Cosmos'
author: markjbrown
ms.service: cosmos-db
ms.topic: samples
ms.date: 05/06/2019
ms.author: mjbrown
ms.openlocfilehash: 9f9e349f6bca0694ce22efd36e36e4ba2ab51d1c
ms.sourcegitcommit: 0ae3139c7e2f9d27e8200ae02e6eed6f52aca476
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/06/2019
ms.locfileid: "65078226"
---
# <a name="delete-a-container-in-an-azure-cosmos-account-using-powershell"></a>Eliminar un contenedor en una cuenta de Azure Cosmos mediante PowerShell

[!INCLUDE [updated-for-az](../../../../../includes/updated-for-az.md)]

[!INCLUDE [sample-powershell-install](../../../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a>Script de ejemplo

[!code-powershell[main](../../../../../powershell_scripts/cosmosdb/sql/ps-container-delete.ps1 "Delete a container in an Azure Cosmos account")]

## <a name="clean-up-deployment"></a>Limpieza de la implementación

Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos y todos los recursos asociados.

```powershell
Remove-AzResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a>Explicación del script

Este script usa los siguientes comandos. Cada comando de la tabla crea un vínculo a documentación específica del comando.

| Get-Help | Notas |
|---|---|
|**Recursos de Azure**| |
| [Remove-AzResource](https://docs.microsoft.com/powershell/module/az.resources/remove-azresource) | Elimina un recurso. |
|**Grupos de recursos de Azure**| |
| [Remove-AzResourceGroup](https://docs.microsoft.com/powershell/module/az.resources/remove-azresourcegroup) | Elimina un grupo de recursos, incluidos todos los recursos anidados. |
|||

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre Azure PowerShell, consulte la [documentación de Azure PowerShell](https://docs.microsoft.com/powershell/).

Encontrará más ejemplos de scripts de PowerShell de Azure Cosmos DB en los [scripts de PowerShell de Azure Cosmos DB](../../../powershell-samples.md).