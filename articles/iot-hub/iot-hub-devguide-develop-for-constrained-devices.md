---
title: Desarrollo en Azure IoT Hub para dispositivos restringidos mediante los SDK para C de IoT Hub | Microsoft Docs
description: 'Guía del desarrollador: instrucciones sobre cómo desarrollar mediante los SDK de Azure IoT para dispositivos restringidos.'
services: iot-hub
documentationcenter: c
author: yzhong94
manager: timlt
editor: ''
ms.assetid: 979136db-c92d-4288-870c-f305e8777bdd
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
origin.date: 05/24/2018
ms.date: 04/29/2019
ms.author: v-yiso
ms.openlocfilehash: 7788bca621a59ec8cdfe36edf73a99efca8c460c
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61320961"
---
# <a name="develop-for-constrained-devices-using-azure-iot-c-sdk"></a>Desarrollo para dispositivos restringidos con los SDK para C de Azure IoT

El SDK de Azure IoT Hub para C está escrito en ANSI C (C99), lo que resulta ideal para operar en una variedad de plataformas con pequeña superficie de memoria y de disco. La cantidad de RAM recomendada es al menos de 64 KB, pero la superficie de memoria exacta depende del protocolo utilizado, el número de conexiones abiertas, así como la plataforma de destino.
> [!NOTE]
> * Azure SDK IoT para C publica regularmente la información de consumo de recursos para ayudar con el desarrollo.  Visite nuestro [repositorio de GitHub](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/c_sdk_resource_information.md) y revise el banco de pruebas más reciente.
>

El SDK para C está disponible en forma de paquete desde apt-get, NuGet y MBED. Para tener como destino dispositivos restringidos, puede que desee compilar el SDK de forma local para la plataforma de destino. En esta documentación se muestra cómo eliminar ciertas características para reducir la superficie del SDK para C con [cmake](https://cmake.org/). Además, esta documentación describe los modelos de programación recomendados para trabajar con dispositivos restringidos.

## <a name="building-the-c-sdk-for-constrained-devices"></a>Compilación del SDK para C para dispositivos restringidos

Compile el SDK para C para dispositivos restringidos.

### <a name="prerequisites"></a>Requisitos previos

Siga esta [guía de configuración del SDK para C](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) para preparar el entorno de desarrollo para la compilación del SDK para C. Antes de llegar al paso de compilación con cmake, puede invocar cmake con marcas para eliminar las características no utilizadas.

### <a name="remove-additional-protocol-libraries"></a>Eliminación de las bibliotecas de protocolos adicionales

SDK de C admite cinco protocolos hoy mismo: MQTT, MQTT sobre WebSocket, AMQPs, AMQP sobre WebSocket y HTTPS. La mayoría de los escenarios requiere uno o dos protocolos en ejecución en un cliente; por lo tanto, puede eliminar las bibliotecas de protocolo que no se usan del SDK. Puede encontrar información adicional acerca de cómo elegir el protocolo de comunicación apropiado para su escenario en [Elegir un protocolo de comunicación para IoT Hub](iot-hub-devguide-protocols.md). Por ejemplo, MQTT es un protocolo ligero que es a menudo más adecuado para dispositivos restringidos.

Puede eliminar las bibliotecas de AMQP y HTTP mediante el siguiente comando de cmake:

```
cmake -Duse_amqp=OFF -Duse_http=OFF <Path_to_cmake>
```

### <a name="remove-sdk-logging-capability"></a>Eliminación de la funcionalidad de registro del SDK

El SDK para C proporciona una registro extenso para ayudar con la depuración. Puede eliminar la funcionalidad de registro de los dispositivos de producción mediante el siguiente comando de cmake:
```
cmake -Dno_logging=OFF <Path_to_cmake>
```

### <a name="remove-upload-to-blob-capability"></a>Eliminación de la funcionalidad de carga a blob

Puede cargar archivos de gran tamaño en Azure Storage con la funcionalidad integrada del SDK. Azure IoT Hub actúa como un distribuidor hacia una cuenta de Azure Storage asociada. Puede usar esta característica para enviar archivos multimedia, grandes lotes de datos de telemetría y registros. Puede obtener más información en [Carga de archivos con IoT Hub](iot-hub-devguide-file-upload.md). Si la aplicación no necesita esta funcionalidad, puede eliminar esta característica mediante el siguiente comando de cmake:

```
cmake -Ddont_use_uploadtoblob=ON <Path_to_cmake>
```

### <a name="running-strip-on-linux-environment"></a>Ejecución de strip en entornos Linux

Si los archivos binarios se ejecutan en el sistema Linux, puede aprovechar el [comando strip](https://en.wikipedia.org/wiki/Strip_(Unix)) para reducir el tamaño de la aplicación final después de compilar.

```
strip -s <Path_to_executable>
```

## <a name="programming-models-for-constrained-devices"></a>Modelos de programación para dispositivos restringidos

A continuación, consulte los modelos de programación para dispositivos restringidos

### <a name="avoid-using-the-serializer"></a>Evitar utilizar el serializador

El SDK para C tiene un [serializador de SDK para C](https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer) opcional, que le permite usar las tablas de asignación declarativas para definir métodos y propiedades de dispositivos gemelos. El serializador está diseñado para simplificar el desarrollo pero agrega sobrecarga, lo cual no es óptimo para dispositivos restringidos. En este caso, considere el uso de las API de cliente primitivas y analice el código JSON con un analizador ligero como [parson](https://github.com/kgabis/parson).

### <a name="use-the-lower-layer-ll"></a>Uso de la capa inferior (_LL_)

El SDK para C admite dos modelos de programación. Cuenta con un conjunto de API con una porción _LL_ en el nombre, que es el acrónimo de capa inferior. Este conjunto de API es ligero y no crea subprocesos de trabajo, lo que significa que el usuario debe controlar manualmente la programación. Por ejemplo, para el cliente de dispositivo, las API _LL_ se pueden encontrar en este [archivo de encabezado](https://github.com/Azure/azure-iot-sdk-c/blob/master/iothub_client/inc/iothub_device_client_ll.h). 

Otro conjunto de API sin el índice _LL_ se denomina capa de comodidad, en las que se activa automáticamente un subproceso de trabajo. Por ejemplo, las API de la capa de conveniencia para el cliente de dispositivo se pueden encontrar en este [archivo de encabezado del cliente de dispositivo de IoT](https://github.com/Azure/azure-iot-sdk-c/blob/master/iothub_client/inc/iothub_device_client.h). En los dispositivos restringidos en los que cada subproceso adicional puede utilizar un gran porcentaje de los recursos del sistema, considere la posibilidad de usar las API _LL_.

## <a name="next-steps"></a>Pasos siguientes
Para más información acerca de la arquitectura del SDK de Azure IoT para C:
- [Código fuente del SDK de Azure IoT para C](https://github.com/Azure/azure-iot-sdk-c/)
- [Introducción al SDK de dispositivo IoT de Azure para C](iot-hub-device-sdk-c-intro.md)

------
[lnk-cmake]: https://cmake.org/
[lnk-devbox-setup]:  https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md
[lnk-choosing-protocol]: iot-hub-devguide-protocols.md
[lnk-hub-file-upload]: iot-hub-devguide-file-upload.md
[lnk-strip]: https://en.wikipedia.org/wiki/Strip_(Unix)
[lnk-serializer]: https://github.com/Azure/azure-iot-sdk-c/tree/master/serializer
[lnk-parson]: https://github.com/kgabis/parson