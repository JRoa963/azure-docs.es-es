---
author: diberry
ms.author: v-junlch
ms.service: cognitive-services
ms.topic: include
origin.date: 04/01/2019
ms.date: 04/23/2019
ms.openlocfilehash: 2d3d7b37721ca1b19f5d73133352cabdbffe6d68
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "60599422"
---
Si necesita configurar un proxy HTTP para realizar solicitudes de salida, use estos dos argumentos:

| NOMBRE | Tipo de datos | DESCRIPCIÓN |
|--|--|--|
|HTTP_PROXY|string|el proxy que se va a usar, por ejemplo, `http://proxy:8888`|
|HTTP_PROXY_CREDS|string|cualquier credencial necesaria para autenticarse en el proxy, por ejemplo, nombre de usuario: contraseña.|

```bash
docker run --rm -it -p 5000:5000 \
--memory 2g --cpus 1 \
--mount type=bind,src=/home/azureuser/output,target=/output \
<registry-location>/<image-name> \
Eula=accept \
Billing=<billing-endpoint> \
ApiKey=<api-key> \
HTTP_PROXY=http://190.169.1.6:3128 \
HTTP_PROXY_CREDS=jerry:123456 \
```

