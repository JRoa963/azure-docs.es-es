---
title: SKU de Azure Container Registry
description: Comparación de los diferentes niveles de servicio disponibles en Azure Container Registry.
services: container-registry
author: dlepow
ms.service: container-registry
ms.topic: article
ms.date: 05/06/2019
ms.author: danlep
ms.openlocfilehash: f36b206ff015511dea7369617febe9220282bbe5
ms.sourcegitcommit: 0ae3139c7e2f9d27e8200ae02e6eed6f52aca476
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/06/2019
ms.locfileid: "65069041"
---
# <a name="azure-container-registry-skus"></a>SKU de Azure Container Registry

Azure Container Registry (ACR) está disponible en varios niveles de servicio, conocidos como SKU. Estas SKU proporcionan precios predecibles y varias opciones para alinearse con la capacidad y patrones de uso de su registro de Docker privado en Azure.

| SKU | Administrado | DESCRIPCIÓN |
| --- | :-------: | ----------- |
| **Básico** | Sí | Un punto de entrada optimizado para los costos para que los desarrolladores aprendan sobre Azure Container Registry. Los registros básicos tienen las mismas funcionalidades de programación como estándar y Premium (por ejemplo, Azure Active Directory [integración con la autenticación](container-registry-authentication.md#individual-login-with-azure-ad), [eliminación de la imagen][container-registry-delete], y [webhooks][container-registry-webhook]). Sin embargo, el almacenamiento incluido y el rendimiento de las imágenes son más adecuadas para escenarios de uso inferior. |
| **Estándar** | Sí | Los registros estándar ofrecen las mismas funcionalidades que los básicos, pero con más almacenamiento y un mayor rendimiento de las imágenes. Los registros estándar deberían satisfacer las necesidades de la mayoría de los escenarios de producción. |
| **Premium** | Sí | Los registros premium proporcionan la mayor cantidad de almacenamiento incluido y operaciones simultáneas, por lo que permiten trabajar con escenarios de mayor volumen. Además de mayor rendimiento de las imágenes, el nivel Premium agrega características como [georreplicación] [ container-registry-geo-replication] para administrar un único registro en varias regiones, [de contenido de confianza](container-registry-content-trust.md) para la firma de etiqueta de imagen, y [firewalls y redes virtuales (versión preliminar)](container-registry-vnet.md) para restringir el acceso al registro. |
|  Clásico (*no está disponible después de abril de 2019*) | Sin  | Con esta SKU se habilitó la versión inicial del servicio Azure Container Registry en Azure. Los registros clásicos se basan en una cuenta de almacenamiento que Azure crea en su suscripción, lo que limita la capacidad de ACR de proporcionar funcionalidades de nivel superior, como el aumento del rendimiento y la replicación geográfica. |

> [!IMPORTANT]
> El registro clásico se va SKU **en desuso**y no estará disponible después de **abril de 2019**. Se recomienda usar básico, estándar o Premium para todos los registros nuevos. Todos los registros clásicos existentes deben actualizarse antes de abril de 2019. Para obtener información de actualización, vea [actualizar un registro clásico][container-registry-upgrade].

Básico, estándar y Premium SKU (denominados *administra registros*) proporcionan las mismas funcionalidades de programación. También se beneficiarán de [almacenamiento de imágenes] [ container-registry-storage] administradas completamente por Azure. Elegir una SKU de nivel superior proporciona más rendimiento y escalabilidad. Con varios niveles de servicio, puede empezar a trabajar con el nivel Básico y, después, cambiar a Estándar y a Premium a medida que aumente su uso del registro.

## <a name="sku-feature-matrix"></a>Matriz de características de la SKU

En la tabla siguiente se detallan las características y los límites de los niveles de servicio Básico, Estándar y Premium.

[!INCLUDE [container-instances-limits](../../includes/container-registry-limits.md)]

## <a name="changing-skus"></a>Cambio de SKU

Puede cambiar la SKU de un registro con la CLI de Azure o en Azure Portal. Puede moverse libremente entre SKU administradas siempre que la SKU a la que se vaya a cambiar tenga la capacidad de almacenamiento máximo necesaria. Al cambiar del modelo clásico a una de las SKU administradas, ya no podrá volver al registro clásico: es una conversión unidireccional.

### <a name="azure-cli"></a>Azure CLI

Para mover entre las SKU en la CLI de Azure, use el comando [az acr update][az-acr-update]. Por ejemplo, para cambiar a Premium:

```azurecli
az acr update --name myregistry --sku Premium
```

### <a name="azure-portal"></a>Azure Portal

En la **información general** del registro de contenedor en Azure Portal, seleccione **Actualizar** y después seleccione una **SKU** nueva en la lista desplegable de SKU.

![Actualización de la SKU del registro de contenedor en Azure Portal][update-registry-sku]

Si tiene un registro clásico, no puede seleccionar una SKU administrada en Azure Portal. En su lugar, debe primero [actualizar] [ container-registry-upgrade] a un registro administrado.

## <a name="pricing"></a>Precios

Para más información acerca de cómo precios para cada una de las SKU de Azure Container Registry, consulte [Precios de Container Registry][container-registry-pricing].

Para obtener más información acerca de los precios de las transferencias de datos, consulte [Detalles de precios de Bandwidth](https://azure.microsoft.com/pricing/details/bandwidth/). 

## <a name="next-steps"></a>Pasos siguientes

**Mapa de ruta de Azure Container Registry**

Visite el [mapa de ruta de ACR][acr-roadmap] en GitHub para más información acerca de las próximas características del servicio.

**UserVoice en Azure Container Registry**

Envíe y vote las sugerencias de nuevas características de [UserVoice en ACR][container-registry-uservoice].

<!-- IMAGES -->
[update-registry-sku]: ./media/container-registry-skus/update-registry-sku.png

<!-- LINKS - External -->
[acr-roadmap]: https://aka.ms/acr/roadmap
[container-registry-pricing]: https://azure.microsoft.com/pricing/details/container-registry/
[container-registry-uservoice]: https://feedback.azure.com/forums/903958-azure-container-registry

<!-- LINKS - Internal -->
[az-acr-update]: /cli/azure/acr#az-acr-update
[container-registry-geo-replication]: container-registry-geo-replication.md
[container-registry-upgrade]: container-registry-upgrade.md
[container-registry-storage]: container-registry-storage.md
[container-registry-delete]: container-registry-delete.md
[container-registry-webhook]: container-registry-webhook.md
