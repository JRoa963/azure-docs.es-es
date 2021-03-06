---
title: Obtener datos de utilización de la máquina virtual de Azure mediante la API de REST | Microsoft Docs
description: Use las API de REST de Azure para recopilar métricas de utilización de una máquina virtual.
services: virtual-machines
author: rloutlaw
ms.reviewer: routlaw
manager: jeconnoc
ms.service: load-balancer
ms.custom: REST
ms.topic: article
ms.date: 06/13/2018
ms.author: routlaw
ms.openlocfilehash: 924154a64673b4ff646f3b6ece373b278ee37181
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "60773271"
---
# <a name="get-virtual-machine-usage-metrics-using-the-rest-api"></a>Obtener métricas de utilización de máquina virtual mediante la API de REST

En este ejemplo se muestra cómo recuperar la utilización de CPU de una [máquina virtual con Linux](https://docs.microsoft.com/azure/virtual-machines/linux/monitor) mediante la [API de REST de Azure](/rest/api/azure/).

La documentación de referencia completa y ejemplos adicionales para la API de REST están disponibles en [Azure Monitor REST reference](/rest/api/monitor) (Referencia de REST de Azure Monitor). 

## <a name="build-the-request"></a>Compilar la solicitud

Utilice la siguiente solicitud GET para recopilar la [métrica de porcentaje de CPU](/azure/monitoring-and-diagnostics/monitoring-supported-metrics#microsoftcomputevirtualmachines) desde una máquina Virtual

```http
GET https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmname}/providers/microsoft.insights/metrics?api-version=2018-01-01&metricnames=Percentage%20CPU&timespan=2018-06-05T03:00:00Z/2018-06-07T03:00:00Z
```

### <a name="request-headers"></a>Encabezados de solicitud

Los siguientes encabezados son obligatorios: 

|Encabezado de solicitud|DESCRIPCIÓN|  
|--------------------|-----------------|  
|*Content-Type:*|Necesario. Establézcalo en `application/json`.|  
|*Authorization:*|Necesario. Establézcalo en un [token de acceso](/rest/api/azure/#authorization-code-grant-interactive-clients) `Bearer` válido. |  

### <a name="uri-parameters"></a>Parámetros del identificador URI

| NOMBRE | DESCRIPCIÓN |
| :--- | :---------- |
| subscriptionId | El id. de suscripción que identifica una suscripción de Azure. Si tiene varias suscripciones, consulte [Trabajo con varias suscripciones](https://docs.microsoft.com/cli/azure/manage-azure-subscriptions-azure-cli?view=azure-cli-latest). |
| resourceGroupName | El nombre del grupo de recursos de Azure asociado al recurso. Puede obtener este valor de la API Azure Resource Manager, la CLI o el portal. |
| vmname | El nombre de la máquina virtual de Azure. |
| metricnames | Lista separada por comas de [métricas válidas de Load Balancer](/azure/load-balancer/load-balancer-standard-diagnostics). |
| api-version | La versión de API que se usará para la solicitud.<br /><br /> En este documento se describe la versión `2018-01-01` de la API que se incluye en la dirección URL anterior.  |
| timespan | Cadena con el siguiente formato `startDateTime_ISO/endDateTime_ISO` que define el intervalo de tiempo de las métricas devueltas. Este parámetro opcional se establece para devolver los datos recopilados durante un día en el ejemplo. |
| &nbsp; | &nbsp; |

### <a name="request-body"></a>Cuerpo de la solicitud

No se necesita ningún cuerpo de solicitud para esta operación.

## <a name="handle-the-response"></a>Control de la respuesta

Cuando la lista de valores de métricas se devuelve correctamente, se devuelve el código de estado 200. Una lista completa de códigos de error está disponible en la [documentación de referencia](/rest/api/monitor/metrics/list#errorresponse).

## <a name="example-response"></a>Respuesta de ejemplo 

```json
{
    "cost": 0,
    "timespan": "2018-06-08T23:48:10Z/2018-06-09T00:48:10Z",
    "interval": "PT1M",
    "value": [
        {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmname}/providers/microsoft.insights/metrics?api-version=2018-01-01&metricnames=Percentage%20CPU",
            "type": "Microsoft.Insights/metrics",
            "name": {
                "value": "Percentage CPU",
                "localizedValue": "Percentage CPU"
            },
            "unit": "Percent",
            "timeseries": [
                {
                    "metadatavalues": [],
                    "data": [
                        {
                            "timeStamp": "2018-06-08T23:48:00Z",
                            "average": 0.44
                        },
                        {
                            "timeStamp": "2018-06-08T23:49:00Z",
                            "average": 0.31
                        },
                        {
                            "timeStamp": "2018-06-08T23:50:00Z",
                            "average": 0.29
                        },
                        {
                            "timeStamp": "2018-06-08T23:51:00Z",
                            "average": 0.29
                        },
                        {
                            "timeStamp": "2018-06-08T23:52:00Z",
                            "average": 0.285
                        } ]
                } ]
        } ]
}
```
