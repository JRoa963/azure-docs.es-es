---
title: Instalación silenciosa de Azure Backup Server v2
description: Use un script de PowerShell para realizar una instalación silenciosa de Azure Backup Server v2. Este tipo de instalación también se denomina instalación desatendida.
services: backup
author: lingliw
manager: digimobile
ms.service: backup
ms.topic: conceptual
origin.date: 11/13/2018
ms.date: 11/26/2018
ms.author: v-lingwu
ms.openlocfilehash: 66ed5765a91b607bc5b765926c5df87d13ff6a24
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "60253852"
---
# <a name="run-an-unattended-installation-of-azure-backup-server"></a>Ejecución de una instalación desatendida de Azure Backup Server

Obtenga información sobre cómo ejecutar una instalación desatendida de Azure Backup Server.

Estos pasos no se aplican si va a instalar Azure Backup Server v1.

## <a name="install-backup-server"></a>Instalación de Backup Server v2

1. En el servidor que hospeda Azure Backup Server v2 o posterior, cree un archivo de texto. (Puede crear el archivo en el Bloc de notas o en otro editor de texto). Guarde el archivo como MABSSetup.ini.

2. Pegue el código siguiente en el archivo MABSSetup.ini. Reemplace el texto entre corchetes (\< \>) por los valores de su entorno. A continuación se muestra un texto de ejemplo:

   ```
   [OPTIONS]
   UserName=administrator
   CompanyName=<Microsoft Corporation>
   SQLMachineName=localhost
   SQLInstanceName=<SQL instance name>
   SQLMachineUserName=administrator
   SQLMachinePassword=<admin password>
   SQLMachineDomainName=<machine domain>
   ReportingMachineName=localhost
   ReportingInstanceName=<reporting instance name>
   SqlAccountPassword=<admin password>
   ReportingMachineUserName=<username>
   ReportingMachinePassword=<reporting admin password>
   ReportingMachineDomainName=<domain>
   VaultCredentialFilePath=<vault credential full path and complete name>
   SecurityPassphrase=<passphrase>
   PassphraseSaveLocation=<passphrase save location>
   UseExistingSQL=<1/0 use or do not use existing SQL>
   ```

3. Guarde el archivo. Después, en un símbolo del sistema con privilegios elevados en el servidor de instalación, escriba este comando:

   ```
   start /wait <cdlayout path>/Setup.exe /i  /f <.ini file path>/setup.ini /L <log path>/setup.log
   ```

Puede usar estas marcas para la instalación:</br>
**/f**: ruta de acceso del archivo .ini</br>
**/l**: Ruta de acceso al registro</br>
**/i**: Ruta de acceso de instalación</br>
**/x**: Ruta de acceso de desinstalación</br>

## <a name="next-steps"></a>Pasos siguientes
Después de instalar Backup Server, sepa cómo preparar el servidor o empezar a proteger la carga de trabajo.

- [Preparar cargas de trabajo de Backup Server](backup-azure-microsoft-azure-backup.md)
- [Usar Backup Server para hacer una copia de seguridad de un servidor de VMware](backup-azure-backup-server-vmware.md)
- [Usar Backup Server para hacer una copia de seguridad de SQL Server](backup-azure-sql-mabs.md)
- [Agregar Modern Backup Storage a Backup Server](backup-mabs-add-storage.md)

<!-- Update_Description: link update -->