---
title: Comparación de valores predeterminados de Video Indexer y Azure Media Services v3 | Microsoft Docs
description: En este tema se comparan los valores predeterminados de Video Indexer y Azure Media Services v3.
services: media-services
documentationcenter: ''
author: juliako
manager: femila
editor: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2019
ms.author: juliako
ms.openlocfilehash: 2c98f6d12f4868e5f90874fe3210fe5368f7ca2d
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "60196004"
---
# <a name="compare-azure-media-services-v3-presets-and-video-indexer"></a>Comparación de los valores predeterminados de Video Indexer y Azure Media Services v3 

En este artículo se comparan las funcionalidades de las **API de Video Indexer** y las **API de Media Services v3**. 

Actualmente, hay una superposición entre las características que ofrece el [Video Indexer API](https://api-portal.videoindexer.ai/) y [las API de Media Services v3](https://github.com/Azure/azure-rest-api-specs/blob/master/specification/mediaservices/resource-manager/Microsoft.Media/stable/2018-07-01/Encoding.json). En la tabla siguiente se ofrecen las instrucciones actuales para entender las similitudes y diferencias. 

## <a name="compare"></a>Comparación

|Característica|API de Video Indexer |Valores predeterminados del analizador de vídeo y el analizador de audio<br/>en Azure Media Services v3|
|---|---|---|
|Información de medios sociales|[Mejorado](video-indexer-output-json-v2.md). |[Aspectos básicos](../latest/intelligence-concept.md)|
|Experiencias|Consulte la lista completa de características admitidas: <br/> [Información general](video-indexer-overview.md)|Devuelve solo información de vídeo.|
|Facturación|[Precios de Media Services](https://azure.microsoft.com/pricing/details/media-services/#analytics)|[Precios de Media Services](https://azure.microsoft.com/pricing/details/media-services/#analytics)|
|Cumplimiento normativo|[ISO 27001](https://www.microsoft.com/TrustCenter/Compliance/ISO-IEC-27001), [ISO 27018](https://www.microsoft.com/trustcenter/Compliance/ISO-IEC-27018), [SOC 1,2,3](https://www.microsoft.com/TrustCenter/Compliance/SOC), [HIPAA](https://www.microsoft.com/trustcenter/compliance/hipaa), [FedRAMP](https://www.microsoft.com/TrustCenter/Compliance/fedramp), [PCI](https://www.microsoft.com/trustcenter/compliance/pci)y [ HITRUST](https://www.microsoft.com/TrustCenter/Compliance/hitrust) certificada. Para las actualizaciones más recientes, visite [estado actual de las certificaciones de Video Indexer](https://gallery.technet.microsoft.com/Overview-of-Azure-c1be3942).|Media Services es compatible con muchas certificaciones. Consulte el [documento PDF de ofertas de cumplimiento de Azure](https://gallery.technet.microsoft.com/Overview-of-Azure-c1be3942/file/178110/23/Microsoft%20Azure%20Compliance%20Offerings.pdf) y busque "Media Services" para ver si cumple con un certificado de interés.|
|Versión de prueba gratuita|Este de EE. UU|No disponible|
|Disponibilidad en regiones|East US 2, sur EE. UU., oeste de EE.UU. 2, Europa del Norte, Europa occidental, sudeste asiático, Asia oriental y este de Australia.  Para las actualizaciones más recientes, visite el [productos por región](https://azure.microsoft.com/global-infrastructure/services/?products=cognitive-services) página.|Consulte el [estado de Azure](https://azure.microsoft.com/global-infrastructure/services/?products=media-services).|

## <a name="next-steps"></a>Pasos siguientes

[Introducción a Video Indexer](video-indexer-overview.md)

[Introducción a Media Services v3](../latest/media-services-overview.md)
