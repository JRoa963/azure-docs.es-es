---
title: Crear un recurso compartido de archivos de Azure de premium
description: En este artículo, aprenderá a crear un recurso compartido de archivos de Azure de premium.
services: storage
author: roygara
ms.service: storage
ms.topic: conceptual
ms.date: 05/05/2019
ms.author: rogarana
ms.subservice: files
ms.openlocfilehash: 265a1cf0a8a5e1e099a4ec7a9f0d674e0c474dd4
ms.sourcegitcommit: 0568c7aefd67185fd8e1400aed84c5af4f1597f9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/06/2019
ms.locfileid: "65190093"
---
# <a name="how-to-create-an-premium-azure-file-share"></a>Cómo crear un recurso compartido de archivos de Azure de premium
Recursos compartidos de archivos de Premium (versión preliminar) se ofrecen en los medios de almacenamiento de discos de estado sólido (SSD) y son útiles para cargas de trabajo intensivas de E/S, incluido el hospedaje de bases de datos y de informática de alto rendimiento (HPC). Recursos compartidos de archivos Premium se hospedan en un tipo de cuenta de almacenamiento de propósito especial denominado FileStorage cuenta. Recursos compartidos de archivos Premium están diseñados para aplicaciones a escala empresarial, que proporciona recursos compartidos de alto rendimiento, IOPS alta y baja latencia coherente y de alto rendimiento.

Este artículo muestra cómo crear este nuevo tipo de cuenta con [portal Azure](https://portal.azure.com/), Azure PowerShell y CLI de Azure.

## <a name="prerequisites"></a>Requisitos previos

Para obtener acceso a recursos de Azure como recursos compartidos de archivos de Azure premium, necesitará una suscripción de Azure. Si todavía no tiene una suscripción, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.

## <a name="create-a-premium-file-share-using-the-azure-portal"></a>Crear un recurso compartido de archivos de premium mediante el portal de Azure

### <a name="sign-in-to-azure"></a>Inicio de sesión en Azure

Inicie sesión en el [Azure Portal](https://portal.azure.com/).

### <a name="create-a-filestorage-preview-storage-account"></a>Crear una cuenta de almacenamiento filestorage (versión preliminar)

Ahora está listo para crear la cuenta de almacenamiento.

Cada cuenta de almacenamiento debe pertenecer a un grupo de recursos de Azure. Un grupo de recursos es un contenedor lógico para agrupar servicios de Azure. Al crear una cuenta de almacenamiento, puede elegir entre crear un grupo de recursos o usar uno existente. En este artículo se muestra cómo crear un nuevo grupo de recursos.

1. En el portal de Azure, seleccione **cuentas de almacenamiento** en el menú izquierdo.

    ![Página principal de Azure portal seleccione la cuenta de almacenamiento](media/storage-how-to-create-premium-fileshare/azure-portal-storage-accounts.png)

1. En la ventana **Cuentas de almacenamiento** que aparece, elija **Agregar**.
1. Seleccione la suscripción en la que se va a crear la cuenta de almacenamiento.
1. En el campo **Grupo de recursos**, haga clic en **Crear nuevo**. Escriba un nombre para el nuevo grupo de recursos, como se muestra en la siguiente imagen.

1. Después, escriba un nombre para la cuenta de almacenamiento. El nombre que elija debe ser único en Azure. El nombre debe tener también una longitud de entre 3 y 24 caracteres y solo puede contener números y letras minúsculas.
1. Seleccione una ubicación para la cuenta de almacenamiento o utilice la ubicación predeterminada.
1. Para **rendimiento** seleccione **Premium**.
1. Seleccione **tipo de cuenta** y elija **FileStorage (versión preliminar)**.
1. Deje **replicación** establecido en su valor predeterminado de **almacenamiento con redundancia local (LRS)**.

    ![Cómo crear una cuenta de almacenamiento para un recurso compartido de archivos de premium](media/storage-how-to-create-premium-fileshare/premium-files-storage-account.png)

1. Seleccione **Revisar y crear** para revisar la configuración de la cuenta de almacenamiento y crear la cuenta.
1. Seleccione **Crear**.

Una vez creado el recurso de la cuenta de almacenamiento, vaya a él.

### <a name="create-a-premium-file-share"></a>Creación de un recurso compartido de archivos premium

1. En el menú izquierdo de la cuenta de almacenamiento, desplácese a la **del servicio de archivos** sección y, después, seleccione **Files (versión preliminar)**.
1. Seleccione **+ recurso compartido de archivos** para crear un recurso compartido de archivos de premium.
1. Escriba un nombre y una cuota deseada para el recurso compartido de archivo y luego seleccione **crear**.

> [!NOTE]
> Tamaños de recurso compartido aprovisionado está especificado por la cuota del recurso compartido, se facturan los recursos compartidos de archivos del tamaño aprovisionado, consulte el [página de precios](https://azure.microsoft.com/pricing/details/storage/files/) para obtener más detalles.

   ![Creación de un recurso compartido de archivos premium](media/storage-how-to-create-premium-fileshare/create-premium-file-share.png)

### <a name="clean-up-resources"></a>Limpieza de recursos

Si desea limpiar los recursos creados en este artículo, simplemente puede eliminar el grupo de recursos. Eliminando el grupo de recursos, también elimina la cuenta de almacenamiento asociada, así como otros recursos asociados con el grupo de recursos.

## <a name="create-a-premium-file-share-using-powershell"></a>Crear un recurso compartido de archivos de premium con PowerShell

### <a name="create-an-account-using-powershell"></a>Creación de una cuenta con PowerShell

En primer lugar, instale la versión más reciente del módulo [PowerShellGet](https://docs.microsoft.com/powershell/gallery/installing-psget).

A continuación, actualice el módulo de PowerShell, inicie sesión en la suscripción de Azure, cree un grupo de recursos y, luego, una cuenta de almacenamiento.

### <a name="upgrade-your-powershell-module"></a>Actualizar el módulo de PowerShell

Para interactuar con un recurso compartido de premium desde con PowerShell, deberá instalar el módulo Az.Storage más reciente.

Para empezar, abra una sesión de PowerShell con permisos elevados.

Instalar el módulo Az.Storage:

```powershell
Install-Module Az.Storage -Repository PSGallery -AllowPrerelease -AllowClobber -Force
```

### <a name="sign-in-to-your-azure-subscription"></a>Inicio de sesión en la suscripción de Azure

Use el comando `Connect-AzAccount` y siga las instrucciones en pantalla para realizar la autenticación.

```powershell
Connect-AzAccount
```

### <a name="create-a-resource-group"></a>Crear un grupo de recursos

Para crear un grupo de recursos con PowerShell, use el comando [New-AzResourceGroup](/powershell/module/az.resources/new-azresourcegroup):

```powershell
# put resource group in a variable so you can use the same group name going forward,
# without hardcoding it repeatedly
$resourceGroup = "storage-how-to-resource-group"
$location = "westus2"
New-AzResourceGroup -Name $resourceGroup -Location $location
```

### <a name="create-a-filestorage-preview-storage-account"></a>Crear una cuenta de almacenamiento FileStorage (versión preliminar)

Para crear una cuenta de almacenamiento filestorage (versión preliminar) de PowerShell, use el [New AzStorageAccount](/powershell/module/az.storage/New-azStorageAccount) comando:

```powershell
$storageAcct = New-AzStorageAccount -ResourceGroupName $resourceGroup -Name "fileshowto" -SkuName "Premium_LRS" -Location "westus2" -Kind "FileStorage"
```

### <a name="create-a-premium-file-share"></a>Creación de un recurso compartido de archivos premium

Ahora que tiene una cuenta FileStorage, puede crear un recurso compartido de archivos de premium. Use la [New AzStorageShare](/powershell/module/az.storage/New-AzStorageShare) para crear uno.

> [!NOTE]
> Tamaños de recurso compartido aprovisionado está especificado por la cuota del recurso compartido, se facturan los recursos compartidos de archivos del tamaño aprovisionado, consulte el [página de precios](https://azure.microsoft.com/pricing/details/storage/files/) para obtener más detalles.

```powershell
New-AzStorageShare `
   -Name myshare `
   -Context $storageAcct.Context
```

### <a name="clean-up-resources"></a>Limpieza de recursos

Para quitar el grupo de recursos y sus recursos asociados, incluida la nueva cuenta de almacenamiento, use el comando [Remove-AzResourceGroup](/powershell/module/az.resources/remove-azresourcegroup): 

```powershell
Remove-AzResourceGroup -Name $resourceGroup
```

## <a name="create-a-premium-file-share-using-azure-cli"></a>Crear un recurso compartido de archivos de premium mediante la CLI de Azure

Para iniciar Azure Cloud Shell, inicie sesión en [Azure Portal](https://portal.azure.com).

Si quiere iniciar sesión en la instalación local de la CLI, ejecute el comando de inicio de sesión:

```cli
az login
```

### <a name="add-the-preview-storage-cli-extension"></a>Agregar la extensión de la CLI de almacenamiento de versión preliminar

Debido a recursos compartidos de archivos premium son una característica de vista previa, tendrá que agregar la extensión de vista previa para el shell. Para ello, mediante Cloud Shell o un shell local, escriba el siguiente comando: `az extension add --name storage-preview`

### <a name="create-a-resource-group"></a>Crear un grupo de recursos

Para crear un grupo de recursos con la CLI de Azure, use el comando [az group create](/cli/azure/group).

```azurecli-interactive
az group create `
    --name files-howto-resource-group `
    --location westus2
```

### <a name="create-a-filestorage-storage-account"></a>Crear una cuenta de almacenamiento FileStorage

Para crear una cuenta de almacenamiento FileStorage desde la CLI de Azure, use el [crear cuenta de almacenamiento de az](/cli/azure/storage/account) comando.

```azurecli-interactive
az storage account create `
    --name fileshowto `
    --resource-group files-howto-resource-group `
    --location westus `
    --sku Premium_LRS `
    --kind FileStorage
```

### <a name="get-the-storage-account-key"></a>Obtención de la clave de la cuenta de almacenamiento

Las claves de cuenta de almacenamiento controlan el acceso a los recursos en una cuenta de almacenamiento, en este artículo, usamos la clave con el fin de crear un recurso compartido de archivos de premium. Las claves se crean automáticamente al crear una cuenta de almacenamiento. Puede obtener las claves de cuenta de almacenamiento con el comando [az storage account keys list](/cli/azure/storage/account/keys):

```azurecli-interactive 
STORAGEKEY=$(az storage account keys list \
    --resource-group "myResourceGroup" \
    --account-name $STORAGEACCT \
    --query "[0].value" | tr -d '"')
```

### <a name="create-a-premium-file-share"></a>Creación de un recurso compartido de archivos premium

Ahora que tiene una cuenta filestorage, puede crear un recurso compartido de archivos de premium. Use la [crear recurso compartido de almacenamiento de az](/cli/azure/storage/share) comando para crear uno.

> [!NOTE]
> Tamaños de recurso compartido aprovisionado está especificado por la cuota del recurso compartido, se facturan los recursos compartidos de archivos del tamaño aprovisionado, consulte el [página de precios](https://azure.microsoft.com/pricing/details/storage/files/) para obtener más detalles.

```azurecli-interactive
az storage share create \
    --account-name $STORAGEACCT \
    --account-key $STORAGEKEY \
    --name "myshare" 
```

### <a name="clean-up-resources"></a>Limpieza de recursos

Para quitar el grupo de recursos y sus recursos asociados, incluida la nueva cuenta de almacenamiento, use el comando [az group delete](/cli/azure/group).

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Pasos siguientes

En este artículo, ha creado un recurso compartido de archivos de premium. Para obtener información sobre el rendimiento que ofrece esta cuenta, continúe a la sección de nivel de rendimiento de la Guía de planeación.

> [!div class="nextstepaction"]
> [Niveles de rendimiento de recurso compartido de archivos](storage-files-planning.md#file-share-performance-tiers)