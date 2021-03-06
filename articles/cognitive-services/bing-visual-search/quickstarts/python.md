---
title: 'Inicio rápido: Obtención de conclusiones de imágenes mediante la API REST Bing Visual Search y Python'
titleSuffix: Azure Cognitive Services
description: Aprenda a cargar una imagen en Bing Visual Search API y obtener conclusiones sobre ella.
services: cognitive-services
author: swhite-msft
manager: nitinme
ms.service: cognitive-services
ms.subservice: bing-visual-search
ms.topic: quickstart
ms.date: 4/02/2019
ms.author: scottwhi
ms.openlocfilehash: 7ec37b4c3bdeb924b3e35dbcb5d07a478611f631
ms.sourcegitcommit: c174d408a5522b58160e17a87d2b6ef4482a6694
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59047133"
---
# <a name="quickstart-get-image-insights-using-the-bing-visual-search-rest-api-and-python"></a>Inicio rápido: Obtención de conclusiones de imágenes mediante la API REST Bing Visual Search y Python

Use este inicio rápido para realizar la primera llamada a Bing Visual Search API y ver los resultados. Esta aplicación de Python carga una imagen en la API y muestra la información que se devuelve. Si bien esta aplicación está escrita en Python, la API es un servicio web RESTful compatible con la mayoría de los lenguajes de programación.

Al cargar una imagen local, los datos del formulario deben incluir el encabezado `Content-Disposition`. Debe establecer su parámetro `name` en "image", y puede establecer el parámetro `filename` en cualquier cadena. El contenido del formulario incluye los datos binarios de la imagen. El tamaño de imagen máximo que puede cargar es de 1 MB.

```
--boundary_1234-abcd
Content-Disposition: form-data; name="image"; filename="myimagefile.jpg"

ÿØÿà JFIF ÖÆ68g-¤CWŸþ29ÌÄøÖ‘º«™æ±èuZiÀ)"óÓß°Î= ØJ9á+*G¦...

--boundary_1234-abcd--
```

## <a name="prerequisites"></a>Requisitos previos

* [Python 3.x](https://www.python.org/)

[!INCLUDE [cognitive-services-bing-visual-search-signup-requirements](../../../../includes/cognitive-services-bing-image-search-signup-requirements.md)]

## <a name="initialize-the-application"></a>Inicialización de la aplicación

1. Cree un archivo de Python en el IDE o editor que prefiera y agregue las siguientes instrucciones `import`:

    ```python
    import requests, json
    ```

2. Cree variables para la clave de suscripción, el punto de conexión y la ruta de acceso a la imagen que está cargando:

    ```python

    BASE_URI = 'https://api.cognitive.microsoft.com/bing/v7.0/images/visualsearch'
    SUBSCRIPTION_KEY = 'your-subscription-key'
    imagePath = 'your-image-path'
    ```

3. Cree un objeto de diccionario para almacenar la información de encabezado de la solicitud. Enlace la clave de suscripción a la cadena `Ocp-Apim-Subscription-Key`, como se muestra a continuación:

    ```python
    HEADERS = {'Ocp-Apim-Subscription-Key': SUBSCRIPTION_KEY}
    ```

4. Cree otro diccionario para almacenar la imagen, que se abrirá y cargará cuando envíe la solicitud:

    ```python
    file = {'image' : ('myfile', open(imagePath, 'rb'))}
    ```

## <a name="parse-the-json-response"></a>Procese la respuesta JSON.

1. Cree un método denominado `print_json()` para ejecutar en la respuesta de API e imprima el código JSON.

    ```python
    def print_json(obj):
        """Print the object as json"""
        print(json.dumps(obj, sort_keys=True, indent=2, separators=(',', ': ')))
    ```

## <a name="send-the-request"></a>Envío de la solicitud

1. Use `requests.post()` para enviar una solicitud a Bing Visual Search API. Incluya la cadena para la información de archivo, encabezado y punto de conexión. Imprima `response.json()` con `print_json()`:

    ```python
    try:
        response = requests.post(BASE_URI, headers=HEADERS, files=file)
        response.raise_for_status()
        print_json(response.json())
    
    except Exception as ex:
        raise ex
    ```

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Creación de una aplicación web de página única de Visual Search](../tutorial-bing-visual-search-single-page-app.md)
