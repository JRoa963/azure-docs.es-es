---
title: Realizar un seguimiento de saldo de crédito de Azure para contrato de cliente de Microsoft | Microsoft Docs
description: Aprenda a comprobar el saldo de crédito de Azure para contrato de cliente de Microsoft.
services: ''
documentationcenter: ''
author: amberbhargava
manager: amberb
editor: banders
tags: billing
ms.service: billing
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/28/2019
ms.author: amberb
ms.openlocfilehash: 1e8c3e6863b9cd8f2f5ced18a57918c32c865e75
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "60372259"
---
# <a name="track-azure-credit-balance-for-microsoft-customer-agreement"></a>Realizar un seguimiento de saldo de crédito de Azure para contrato de cliente de Microsoft

Puede comprobar el saldo de crédito de Azure para contrato de cliente de Microsoft en Azure portal. Usar créditos para pagar productos que están cubiertos por el importe del crédito.

Se le cobrará cuando use productos que no están cubiertos por los créditos o el uso supera el saldo de crédito. Para obtener más información, consulte [productos que no están cubiertos por los créditos de Azure.](#products-that-arent-covered-by-azure-credits)

En este artículo se aplica a una cuenta de facturación para un contrato de cliente de Microsoft. [Compruebe si tiene acceso a un contrato de cliente de Microsoft](#check-access-to-a-microsoft-customer-agreement).

## <a name="check-credit-balance-in-the-azure-portal"></a>Comprobar el saldo de crédito en Azure portal

1. Inicie sesión en el [Azure Portal]( https://portal.azure.com).

2. Busque en **Administración de costos + facturación**.

   ![Captura de pantalla que muestra la búsqueda en el portal de administración de costos + facturación](./media/billing-mca-check-azure-credits-balance/billing-search-cost-management-billing.png)

3. Vaya al perfil de facturación. Dependiendo de su acceso, es posible que tenga que seleccionar una cuenta de facturación. En la cuenta de facturación, seleccione **facturación perfiles** y, a continuación, un perfil de facturación.

4. Seleccione **créditos de Azure**.

5. La página de créditos de Azure muestra la siguiente información:

   ![Captura de pantalla de saldo de crédito y transacciones para un perfil de facturación](./media/billing-mca-check-azure-credits-balance/billing-mca-credits-overview.png)

   | Término               | Definición                           |
   |--------------------|--------------------------------------------------------|
   | Saldo estimado  | Cantidad estimada de créditos tiene después teniendo en cuenta todos los factura y las transacciones pendientes |
   | Saldo actual    | Cantidad de créditos a partir de la última factura. No incluye las transacciones pendientes |
   | Transacciones       | Todas las transacciones de facturación que se ve afectado el saldo de crédito de Azure |

   Cuando el saldo estimado cae a 0, se le cobrará el uso, incluidos para los productos que están cubiertos por los créditos.

6. Seleccione **lista créditos** para ver la lista de créditos para el perfil de facturación. La lista de créditos proporciona la siguiente información:

   ![Captura de pantalla de las listas de créditos para un perfil de facturación](./media/billing-mca-check-azure-credits-balance/billing-mca-credits-list.png)

   | Término                 | Definición                           |
   |----------------------|--------------------------------------------------------|
   | Origen               | El origen de la adquisición del crédito |
   | Fecha de inicio           | La fecha se adquirió el crédito |
   | Fecha de expiración      | Cuando expira el crédito |
   | Saldo              | El saldo a partir de la última factura |
   | Cantidad original      | La cantidad original de crédito |
   | Status               | El estado actual de crédito. Estado puede ser activo, ha usado, expirado o que expire |

## <a name="how-credits-are-used-in-microsoft-customer-agreement"></a>Cómo se usan los créditos en el contrato del cliente de Microsoft

En una cuenta de facturación para un contrato de cliente de Microsoft, utiliza perfiles de facturación para administrar las facturas y los métodos de pago. Se genera una factura mensual para cada perfil de facturación y usar los métodos de pago para pagar la factura.

Los créditos de Azure son uno de los métodos de pago. Obtener crédito de Microsoft como crédito promocional y el crédito de nivel de servicio. Estos créditos se asignan a un perfil de facturación. Cuando se genera una factura para el perfil de facturación, los créditos se aplican automáticamente a la cantidad total de facturación para calcular la cantidad que debe pagar. Pagar el monto restante con otro método de pago, como la comprobación o transferencia bancaria.

## <a name="products-that-arent-covered-by-azure-credits"></a>Productos que no están cubiertos por los créditos de Azure

 Los siguientes productos no están cubiertos por sus créditos de Azure. Se le cobrará por usar estos productos, independientemente de su saldo de crédito:

- Canonical
- Citrix XenApp Essentials
- Citrix XenDesktop 
- Usuario registrado
- Openlogic
- Usuario registrado de Remote Access Rights XenApp Essentials
- Ubuntu Advantage
- Visual Studio Enterprise (mensual)
- Visual Studio Enterprise (anual)
- Visual Studio Professional (mensual)
- Visual Studio Professional (anual)
- Productos de Azure Marketplace
- Planes de soporte técnico de Azure

## <a name="check-access-to-a-microsoft-customer-agreement"></a>Comprobar el acceso a un contrato de cliente de Microsoft
[!INCLUDE [billing-check-mca](../../includes/billing-check-mca.md)]

## <a name="need-help-contact-support"></a>¿Necesita ayuda? Ponerse en contacto con soporte técnico

Si necesita ayuda, [póngase en contacto con soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) para resolver el problema rápidamente.

## <a name="next-steps"></a>Pasos siguientes

- [Descripción de cuenta de facturación de contrato de cliente de Microsoft](billing-mca-overview.md)
- [Descripción de los términos en la factura del contrato de cliente de Microsoft](billing-mca-understand-your-invoice.md)