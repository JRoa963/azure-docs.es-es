---
title: API de entrega SaaS | Azure Marketplace
description: Presenta las versiones de la realización de las API que le permiten integrar su SaaS ofrece con Azure Marketplace.
services: Azure, Marketplace, Cloud Partner Portal,
author: v-miclar
ms.service: marketplace
ms.topic: conceptual
ms.date: 03/26/2019
ms.author: pabutler
ms.openlocfilehash: ec206c2d637f9fb2727d72cf17087050a765672c
ms.sourcegitcommit: c53a800d6c2e5baad800c1247dce94bdbf2ad324
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/30/2019
ms.locfileid: "64941961"
---
# <a name="saas-fulfillment-apis"></a>API de suministro de SaaS

Las API de entrega SaaS habilitar proveedores de software independientes (ISV) integrar sus aplicaciones SaaS con Azure Marketplace. Estas API permiten a las aplicaciones de ISV participar en todos los canales de comercio electrónico: directo, dirigidos por asociados (distribuidor) y liderado por el campo.  Son un requisito para enumerar permiten transacciones ofertas de SaaS en Azure Marketplace.

> [!WARNING]
> La versión actual de esta API es la versión 2, que debe usarse para SaaS nuevo todas las ofertas.  Versión 1 de la API está en desuso y se mantiene por razones de compatibilidad con las ofertas existentes.


## <a name="business-model-support"></a>Compatibilidad con el modelo empresarial

Esta API admite las siguientes capacidades de modelo de negocio; Puedes:

* Especifique varios planes de una oferta. Estos planes tienen una funcionalidad diferente y es posible que precios diferentes.
* Proporcionar una oferta en una por sitio o una por cada modelo de facturación de usuario.
* Proporcionar mensuales y anuales (pagadas por adelantado) opciones de facturación.
* Proporcionar precios privada a un cliente basado en un acuerdo de negocio negociado.


## <a name="next-steps"></a>Pasos siguientes

Si no lo ha hecho ya, registre la aplicación de SaaS en la [portal Azure](https://ms.portal.azure.com) como se explica en [registrar una aplicación de Azure AD](./cpp-saas-registration.md).  Después, use la versión más reciente de esta interfaz para el desarrollo: [Versión 2 de la API de entrega SaaS](./cpp-saas-fulfillment-api-v2.md).
