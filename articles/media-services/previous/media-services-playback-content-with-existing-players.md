---
title: Uso de reproductores existentes para reproducir el contenido - Azure | Microsoft Docs
description: En este tema se enumeran los reproductores existentes que puede usar para reproducir el contenido.
services: media-services
documentationcenter: ''
author: Juliako
manager: femila
editor: ''
ms.assetid: 7e9fcf89-0fb6-4fa4-96cb-666320684d69
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/19/2019
ms.author: juliako
ms.openlocfilehash: c96710d6dcca9f5ef99b3a02a0bc875d433f814d
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61463422"
---
# <a name="playing-your-content-with-existing-players"></a>Reproducción de contenido con existentes
Azure Media Services admite muchos formatos de streaming populares como Smooth Streaming, HTTP Live Streaming y MPEG-Dash. Este tema remite a reproductores existentes que puede usar para probar sus transmisiones.

### <a name="the-azure-portal-media-services-content-player"></a>Reproductor del contenido de Media Services de Azure Portal
**Azure Portal** proporciona un reproductor de contenido que puede usar para probar el vídeo.

Haga clic en el vídeo deseado (asegúrese de que se ha [publicado](media-services-portal-publish.md)) y haga clic en el botón **Reproducir** situado en la parte inferior del portal.

Se aplican algunas consideraciones:

* El **REPRODUCTOR DE CONTENIDO DE SERVICIOS MULTIMEDIA** reproduce desde el extremo de streaming predeterminado. Si desea reproducir desde un extremo de streaming que no esté predeterminado, use otro reproductor. Por ejemplo, [Azure Media Player](https://amsplayer.azurewebsites.net/azuremediaplayer.html).

![AMSPlayer][AMSPlayer]

### <a name="azure-media-player"></a>Azure Media Player
Use [Azure Media Player](https://amsplayer.azurewebsites.net/azuremediaplayer.html) para reproducir el contenido (libre o protegido) en cualquiera de los siguientes formatos:

* Smooth Streaming
* MPEG DASH
* HLS
* MP4 progresivo

### <a name="flash-player"></a>Flash Player
#### <a name="aes-encrypted-with-token"></a>Cifrado de AES con token
[https://aestoken.azurewebsites.net](https://aestoken.azurewebsites.net)

### <a name="silverlight-players"></a>Reproductores de Silverlight

#### <a name="playready-with-token"></a>PlayReady con token
[https://sltoken.azurewebsites.net](https://sltoken.azurewebsites.net)

### <a name="dash-players"></a>Reproductores DASH
[https://dashplayer.azurewebsites.net](https://dashplayer.azurewebsites.net)

[https://dashif.org](https://dashif.org)

### <a name="other"></a>Otros
Para probar las direcciones URL de HLS también puede utilizar:

* **Safari** en un dispositivo iOS o
* **3ivx HLS Player** en Windows.

## <a name="developing-video-players"></a>Desarrollo de reproductores de vídeo
Para obtener información sobre cómo desarrollar sus propios reproductores, consulte [Desarrollo de reproductores de vídeo](media-services-develop-video-players.md)

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Media Services
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

[AMSPlayer]: ./media/media-services-playback-content-with-existing-players/media-services-portal-player.png
