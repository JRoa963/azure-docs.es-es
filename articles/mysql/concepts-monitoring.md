---
title: Supervisión en Azure Database for MySQL
description: En este artículo se describen las métricas de supervisión y alerta de Azure Database for MySQL, incluidas las estadísticas de CPU, almacenamiento y conexión.
author: rachel-msft
ms.author: raagyema
ms.service: mysql
ms.topic: conceptual
ms.date: 11/05/2018
ms.openlocfilehash: 9dcb79e7f4ebd43da3f6c6fd35fa0707898d7ec8
ms.sourcegitcommit: 0568c7aefd67185fd8e1400aed84c5af4f1597f9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/06/2019
ms.locfileid: "60525559"
---
# <a name="monitoring-in-azure-database-for-mysql"></a>Supervisión en Azure Database for MySQL
La supervisión de los datos sobre los servidores le permite solucionar problemas y optimizar la carga de trabajo. Azure Database for MySQL proporciona diversas métricas que proporcionan información sobre el comportamiento del servidor.

## <a name="metrics"></a>Métricas
Todas las métricas de Azure tienen una frecuencia de un minuto y cada métrica proporciona 30 días de historial. Puede configurar alertas en las métricas. Para obtener instrucciones paso a paso, consulte [How to set up alerts](howto-alert-on-metric.md) (Configuración de alertas). Otras tareas incluyen la configuración de acciones automatizadas, la realización de análisis avanzados y el archivo del historial. Para obtener más información, consulte [Información general sobre las métricas en Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).

### <a name="list-of-metrics"></a>Lista de métricas
Estas métricas están disponibles para Azure Database for MySQL:

|Métrica|Nombre de métrica para mostrar|Unidad|DESCRIPCIÓN|
|---|---|---|---|
|cpu_percent|Porcentaje de CPU|Percent|Porcentaje de CPU en uso.|
|memory_percent|Porcentaje de memoria|Percent|Porcentaje de memoria en uso.|
|io_consumption_percent|Porcentaje de E/S|Percent|Porcentaje de E/S en uso.|
|storage_percent|Porcentaje de almacenamiento|Percent|Porcentaje de almacenamiento que se usa más allá del límite máximo del servidor.|
|storage_used|Almacenamiento utilizado|Bytes|Cantidad de almacenamiento en uso. El almacenamiento que usa el servicio puede incluir los archivos de base de datos, los registros de transacciones y los registros de servidor.|
|serverlog_storage_percent|Porcentaje de almacenamiento del registro del servidor|Percent|El porcentaje usado del almacenamiento máximo de registro del servidor.|
|serverlog_storage_usage|Almacenamiento del registro del servidor usado|Bytes|La cantidad de almacenamiento de registro del servidor en uso.|
|serverlog_storage_limit|Límite de almacenamiento del registro del servidor|Bytes|El almacenamiento máximo de registro de este servidor.|
|storage_limit|Límite de almacenamiento|Bytes|Almacenamiento máximo de este servidor.|
|active_connections|Conexiones activas|Count|Número de conexiones activas al servidor.|
|connections_failed|Conexiones con errores|Count|Número de conexiones con errores al servidor.|
|seconds_behind_master|Intervalo de replicación en segundos|Count|El número de segundos que el servidor de réplica se retrasa en relación con el servidor maestro.|
|network_bytes_egress|Red interna|Bytes|Red externa a través de conexiones activas.|
|network_bytes_ingress|Red interna|Bytes|Red interna a través de conexiones activas.|
|backup_storage_used|Almacenamiento de copia de seguridad utilizado|Bytes|Cantidad de almacenamiento de copia de seguridad utilizado.|

## <a name="server-logs"></a>Registros del servidor
Puede habilitar el registro de consultas lentas en el servidor. Estos registros también están disponibles a través de los registros de diagnóstico de Azure en la cuenta de almacenamiento, Event Hubs y los registros de Azure Monitor. Para más información sobre el registro, visite la página  [Registros de servidor](concepts-server-logs.md).

## <a name="next-steps"></a>Pasos siguientes
- Consulte [How to set up alerts](howto-alert-on-metric.md) (Configuración de alertas) para obtener instrucciones sobre cómo crear una alerta en una métrica.
- Para obtener más información sobre cómo acceder a las métricas y exportarlas con Azure Portal, la API de REST o la CLI, consulte [Información general sobre las métricas en Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).
- Lea nuestro blog sobre [procedimientos recomendados para supervisar el servidor](https://azure.microsoft.com/blog/best-practices-for-alerting-on-metrics-with-azure-database-for-mysql-monitoring/).
