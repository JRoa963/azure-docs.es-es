---
title: Habilitación del Cifrado de datos transparente en Azure Security Center | Microsoft Docs
description: En este documento se muestra cómo implementar la recomendación **Habilitar el Cifrado de datos transparente** de Azure Security Center.
services: security-center
documentationcenter: na
author: rkarlin
manager: barbkess
editor: ''
ms.assetid: e4be8a0e-2118-4ee9-a266-69e52d9f7f8e
ms.service: security-center
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/28/2018
ms.author: rkarlin
ms.openlocfilehash: d5ddec40a1b20e377ec18ce871018f674557e7b4
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "60704039"
---
# <a name="enable-transparent-data-encryption-in-azure-security-center"></a>Habilitación del Cifrado de datos transparente en Azure Security Center
Azure Security Center recomienda que habilite el Cifrado de datos transparente (TDE) en bases de datos SQL si aún no lo ha hecho. TDE protege los datos y le ayuda a cumplir con los requisitos normativos cifrando la base de datos, las copias de seguridad asociadas y los archivos de registro de transacciones en reposo sin requerir cambios en la aplicación. Para obtener más información, consulte [Cifrado de datos transparente con Azure SQL Database](https://msdn.microsoft.com/library/dn948096).

Esta recomendación se aplica solo al servicio de SQL de Azure; no incluye al servicio SQL que se ejecuta en las máquinas virtuales.

> [!NOTE]
> En este documento se presenta el servicio mediante una implementación de ejemplo.  No se trata de una guía paso a paso.
>
>

## <a name="implement-the-recommendation"></a>Implementación de la recomendación
1. En la hoja **Recomendaciones**, seleccione **Habilitar el cifrado de datos transparente**.
   ![Habilitar el cifrado de datos transparente][1]
2. De este modo, se abre la hoja **Habilitar el cifrado de datos transparente en bases de datos SQL** . Seleccione una base de datos SQL en la que habilitar el TDE.
   ![Selección de la base de datos SQL en la que habilitar TDE][2]
3. En la hoja **Cifrado de datos transparente**, seleccione **Activar** en Cifrado de datos y seleccione **Guardar** en la cinta de opciones superior de la hoja.
   ![Activación de TDE][3]

   Una vez que el TDE esté habilitado en la base de datos SQL seleccionada, el **Estado de cifrado** cambiará a **Cifrado**.    

   ![Estado de cifrado][4]

## <a name="see-also"></a>Vea también
En este artículo mostramos cómo implementar la recomendación "Habilitar el cifrado de datos transparente" de Security Center. Para obtener más información sobre TDE de SQL, vea lo siguiente:

* [Cifrado de datos transparente con Azure SQL Database](https://msdn.microsoft.com/library/dn948096)
* [Introducción al cifrado de datos transparente (TDE)](../sql-data-warehouse/sql-data-warehouse-encryption-tde.md)

Para más información sobre el Centro de seguridad, consulte los siguientes recursos:

* [Establecimiento de directivas de seguridad en Azure Security Center](tutorial-security-policy.md): aprenda a configurar directivas de seguridad para las suscripciones y los grupos de recursos de Azure.
* [Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md): recomendaciones que le ayudan a proteger los recursos de Azure.
* [Supervisión del estado de seguridad en Azure Security Center](security-center-monitoring.md): obtenga información sobre cómo supervisar el mantenimiento de los recursos de Azure.
* [Administración y respuesta a las alertas de seguridad en Azure Security Center](security-center-managing-and-responding-alerts.md): obtenga información sobre cómo administrar y responder a alertas de seguridad.
* [Supervisión de las soluciones de asociados con Azure Security Center](security-center-partner-solutions.md): aprenda a supervisar el estado de mantenimiento de las soluciones de asociados.
* [Preguntas más frecuentes sobre Azure Security Center](security-center-faq.md): busque las preguntas más frecuentes sobre cómo usar el servicio.
* [Blog de seguridad de Azure](https://blogs.msdn.com/b/azuresecurity/): obtenga las últimas noticias e información sobre la seguridad en Azure.

<!--Image references-->
[1]: ./media/security-center-enable-tde-on-sql-databases/enable-tde.png
[2]:./media/security-center-enable-tde-on-sql-databases/transparent-data-encryption-blade.png
[3]: ./media/security-center-enable-tde-on-sql-databases/turn-on-tde.png
[4]: ./media/security-center-enable-tde-on-sql-databases/encrypted.png
