---
title: archivo de inclusión
description: archivo de inclusión
services: virtual-machines
author: roygara
ms.service: virtual-machines
ms.topic: include
ms.date: 01/22/2019
ms.author: rogarana
ms.custom: include file
ms.openlocfilehash: 42ab8be45d4086589f0793531003700e7552a440
ms.sourcegitcommit: 44a85a2ed288f484cc3cdf71d9b51bc0be64cc33
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2019
ms.locfileid: "64744568"
---
**Transferencias de datos de salida**: [transferencias de datos de salida](https://azure.microsoft.com/pricing/details/bandwidth/) (datos que salen de los centros de datos de Azure) incurren en la facturación por el uso de ancho de banda.

**Transacciones**: se le factura por el número de transacciones que realiza en un disco administrado estándar. Para SSD estándar, se usa el tamaño de unidad de E/S de 256 KiB para teniendo en cuenta el número de transacciones. Los tamaños de E/S más grandes se cuentan como varias operaciones de E/S con un tamaño de 256 KiB. Para unidades de disco duro estándar, cada operación de E/S se considera como una única transacción, independientemente del tamaño de E/S.

Para obtener información detallada sobre los precios de Managed Disks, incluidos los costos de transacción, vea [precios de Managed Disks](https://azure.microsoft.com/pricing/details/managed-disks).

### <a name="ultra-ssd-vm-reservation-fee"></a>Precio de reserva de VM de Ultra SSD

Las máquinas virtuales de Azure tienen la funcionalidad para indicar si son compatibles con SSD Ultra. Una máquina virtual compatible con SSD Ultra asigna capacidad dedicada de ancho de banda entre la instancia de la máquina virtual de proceso y la unidad de escalado de almacenamiento en bloque, para así poder optimizar el rendimiento y reducir la latencia. Al agregar esta funcionalidad en la máquina virtual, se crea un cargo por reserva que solo se cobra si habilita la funcionalidad de discos Ultra en la máquina virtual sin asociarle uno de estos discos. Cuando un disco Ultra está asociado a la máquina virtual compatible con estos discos, este cargo no se aplicará. Este cargo se calcula según la vCPU aprovisionada en la máquina virtual.

Para información sobre los precios de los discos Ultra, consulte la [página de precios de discos de Azure](https://azure.microsoft.com/pricing/details/managed-disks/).