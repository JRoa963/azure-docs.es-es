---
title: Características de Azure Cloud Shell | Microsoft Docs
description: Introducción a las características de Bash en Azure Cloud Shell
services: Azure
documentationcenter: ''
author: maertendMSFT
manager: timlt
tags: azure-resource-manager
ms.assetid: ''
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/26/2019
ms.author: damaerte
ms.openlocfilehash: f873f20f97b822e1f4dee716cb69535b0522dc2c
ms.sourcegitcommit: e7d4881105ef17e6f10e8e11043a31262cfcf3b7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/29/2019
ms.locfileid: "64866503"
---
# <a name="features--tools-for-azure-cloud-shell"></a>Características y herramientas de Azure Cloud Shell

[!INCLUDE [features-introblock](../../includes/cloud-shell-features-introblock.md)]

Azure Cloud Shell se ejecuta en `Ubuntu 16.04 LTS`.

## <a name="features"></a>Características

### <a name="secure-automatic-authentication"></a>Protección de la autenticación automática

Cloud Shell autentica de forma segura y automática el acceso a la cuenta para la CLI de Azure y Azure PowerShell.

### <a name="home-persistence-across-sessions"></a>Persistencia de $HOME entre sesiones

Para conservar archivos entre sesiones, la primera vez que se inicia Cloud Shell se explica cómo conectar un recurso compartido de archivos de Azure.
Una vez finalizado, Cloud Shell conectará automáticamente su almacenamiento (montado como `$HOME\clouddrive`) para todas las sesiones futuras.
Además, el directorio `$HOME` se conserva como un archivo .img en el recurso compartido de archivos Azure.
Los archivos fuera de `$HOME` y el estado de la máquina no se conservan entre sesiones. Use los procedimientos recomendados al almacenar secretos, como las claves SSH. Los servicios como [Azure Key Vault tiene tutoriales de configuración](https://docs.microsoft.com/azure/key-vault/key-vault-manage-with-cli2#prerequisites).

[Más información sobre la persistencia de archivos en Cloud Shell](persisting-shell-storage.md).

### <a name="azure-drive-azure"></a>Unidad de Azure (Azure):

PowerShell en Cloud Shell se inicia en la unidad de Azure (`Azure:`).
La unidad de Azure permite detectar y navegar fácilmente por los recursos de Azure, como Compute, Network y Storage, etc., de manera similar a la navegación por el sistema de archivos.
Puede seguir usando los [cmdlets de Azure PowerShell](https://docs.microsoft.com/powershell/azure) que ya conoce para administrar estos recursos sin importar la unidad en la que se encuentre.
Cualquier cambio que se realice en los recursos de Azure, ya sea directamente en Azure Portal o mediante los cmdlets de Azure PowerShell, se reflejan en la unidad de Azure.  Puede ejecutar `dir -Force` para actualizar los recursos.

![](media/features-powershell/azure-drive.png)

### <a name="manage-exchange-online"></a>Manage Exchange Online

PowerShell en Cloud Shell contiene una compilación privada del módulo de Exchange Online.  Ejecute `Connect-EXOPSSession` para obtener los cmdlets de Exchange.

![](media/features-powershell/exchangeonline.png)

 Ejecute `Get-Command -Module tmp_*`
> [!NOTE]
> El nombre del módulo debe comenzar por `tmp_`, si ha instalado módulos con el mismo prefijo, también se expone sus cmdlets. 

![](media/features-powershell/exchangeonlinecmdlets.png)

### <a name="deep-integration-with-open-source-tooling"></a>Profunda integración con herramientas de código abierto

Cloud Shell incluye autenticación configurada previamente para herramientas de código abierto, como Terraform, Ansible y Chef InSpec. Pruébelo desde los tutoriales de ejemplo.

## <a name="tools"></a>Herramientas

|Category   |NOMBRE   |
|---|---|
|Herramientas de Linux            |Bash<br> zsh<br> sh<br> tmux<br> dig<br>               |
|Herramientas de Azure            |[CLI de Azure](https://github.com/Azure/azure-cli) y [CLI de Azure clásica](https://github.com/Azure/azure-xplat-cli)<br> [AzCopy](https://docs.microsoft.com/azure/storage/common/storage-use-azcopy-linux?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#writing-your-first-azcopy-command)<br> [CLI de Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-cli)<br> [Batch Shipyard](https://github.com/Azure/batch-shipyard)<br> [blobxfer](https://github.com/Azure/blobxfer)|
|Editores de texto           |código (editor de Cloud Shell)<br> vim<br> nano<br> emacs    |
|Control de código fuente         |git                    |
|Herramientas de compilación            |make<br> maven<br> npm<br> pip         |
|Contenedores             |[Máquina de Docker](https://github.com/docker/machine)<br> [Kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/)<br> [Helm](https://github.com/kubernetes/helm)<br> [CLI de DC/OS](https://github.com/dcos/dcos-cli)         |
|Bases de datos              |Cliente de MySQL<br> Cliente de PostgreSql<br> [Utilidad sqlcmd](https://docs.microsoft.com/sql/tools/sqlcmd-utility)<br> [mssql-scripter](https://github.com/Microsoft/sql-xplat-cli) |
|Otros                  |Cliente de iPython<br> [CLI de Cloud Foundry](https://github.com/cloudfoundry/cli)<br> [Terraform](https://www.terraform.io/docs/providers/azurerm/)<br> [Ansible](https://www.ansible.com/microsoft-azure)<br> [Chef InSpec](https://www.chef.io/inspec/)|

## <a name="language-support"></a>Compatibilidad con idiomas

|Idioma   |`Version`   |
|---|---|
|.NET Core  |2.0.0       |
|Go         |1.9        |
|Java       |1.8        |
|Node.js    |8.9.4      |
|PowerShell |[6.2.0](https://github.com/PowerShell/powershell/releases)       |
|Python     |2.7 y 3.5 (predeterminadas)|

## <a name="next-steps"></a>Pasos siguientes
[Guía de inicio rápido de Bash en Cloud Shell](quickstart.md) <br>
[Guía de inicio rápido de PowerShell en Cloud Shell](quickstart-powershell.md) <br>
[Más información acerca de la CLI de Azure](https://docs.microsoft.com/cli/azure/) <br>
[Información acerca de Azure PowerShell](https://docs.microsoft.com/powershell/azure/) <br>
