---
author: clemensv
ms.service: service-bus-relay
ms.topic: include
ms.date: 11/09/2018
ms.author: clemensv
ms.openlocfilehash: ceb2626a43ed44338bb0faad475ae2333af2de9e
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "60553910"
---
Asegúrese de haber [creado un espacio de nombres de Relay][namespace-how-to].

1. Inicie sesión en el [Azure Portal](https://portal.azure.com).
2. En el menú izquierdo, seleccione **Todos los recursos**.
3. Seleccione el espacio de nombres en el que quiere crear la conexión híbrida. En este caso, es **mynewns**.  
4. En **Relay namespace** (Espacio de nombres de Relay), seleccione **Conexiones híbridas**.

    ![Create a hybrid connection](./media/relay-create-hybrid-connection-portal/create-hc-1.png)

5. En la ventana de información general del espacio de nombres, haga clic en **+ Hybrid Connection** (+ Conexión híbrida).
   
    ![Seleccione la conexión híbrida](./media/relay-create-hybrid-connection-portal/create-hc-2.png)
6. En **Crear conexión híbrida**, escriba un valor para el nombre de la conexión híbrida. Deje los demás valores predeterminados.
   
    ![Seleccionar Nuevo](./media/relay-create-hybrid-connection-portal/create-hc-3.png)
7. Seleccione **Crear**.

[namespace-how-to]: ../articles/service-bus-relay/relay-create-namespace-portal.md 