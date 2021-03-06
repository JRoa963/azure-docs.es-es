---
title: Reinicio de una máquina virtual en un laboratorio de Azure DevTest Labs | Microsoft Docs
description: Obtenga información sobre cómo reiniciar una máquina virtual en Azure DevTest Labs.
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
editor: ''
ms.assetid: 8460f09e-482f-48ba-a57a-c95fe8afa001
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2018
ms.author: spelluru
ms.openlocfilehash: 34c08a79abf6acb5ae8582ecd0743a890d850fc8
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "60864428"
---
# <a name="restart-a-vm-in-a-lab-in-azure-devtest-labs"></a>Reinicio de una máquina virtual en un laboratorio de Azure DevTest Labs
Puede reiniciar una máquina virtual de forma rápida y sencilla en DevTest Labs mediante los pasos descritos en este artículo. Tenga en cuenta lo siguiente antes de reiniciar una máquina virtual:

- La máquina virtual debe estar ejecutándose para que la característica de reinicio se pueda habilitar.
- Si un usuario está conectado a una máquina virtual en ejecución cuando lleva a cabo un reinicio, debe volver a conectarse a la máquina virtual después de que se inicie la copia de seguridad.
- Si se está aplicando un artefacto cuando se reinicia la máquina virtual, recibirá una advertencia que indica que no se puede aplicar el artefacto.

    ![Advertencia al reiniciar mientras se aplican artefactos](./media/devtest-lab-restart-vm/devtest-lab-restart-vm-apply-artifacts.png)


   > [!NOTE]
   > Si la máquina virtual se ha detenido al aplicar un artefacto, puede usar la característica de reinicio de máquina virtual para intentar resolver el problema.
   >
   >

## <a name="steps-to-restart-a-vm-in-a-lab-in-azure-devtest-labs"></a>Pasos para reiniciar una máquina virtual en un laboratorio de Azure DevTest Labs
1. Inicie sesión en el [Azure Portal](https://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Seleccione **Todos los servicios** y, luego, **DevTest Labs** en la lista.
1. En la lista de laboratorios, seleccione el que incluye la máquina virtual que quiere reiniciar.
1. En el panel izquierdo, seleccione **Mis máquinas virtuales**.
1. En la lista de máquinas virtuales, seleccione una máquina virtual en ejecución.
1. En la parte superior del panel de administración de máquinas virtuales, seleccione **Reiniciar**.

    ![Botón para reiniciar la máquina virtual](./media/devtest-lab-restart-vm/devtest-lab-restart-vm.png)

1. Supervise el estado del reinicio. Para ello, seleccione el icono **Notificaciones** situado en la parte superior derecha de la ventana.

    ![Consulta del estado del reinicio de la máquina virtual](./media/devtest-lab-restart-vm/devtest-lab-restart-notification.png)

También puede reiniciar una máquina virtual en ejecución si selecciona los puntos suspensivos (…) que aparecen a su lado en la lista de **Mis máquinas virtuales**.

![Reinicio de la máquina virtual mediante los puntos suspensivos](./media/devtest-lab-restart-vm/devtest-lab-restart-elipses.png)

## <a name="next-steps"></a>Pasos siguientes
* Una vez que se haya reiniciado, puede volver a conectarse a la máquina virtual. Para ello, seleccione **Conectar** en el panel de administración.
* Explore la [galería de plantillas de inicio rápido de Azure Resource Manager de DevTest Labs](https://github.com/Azure/azure-devtestlab/tree/master/samples/DevTestLabs/QuickStartTemplates).
