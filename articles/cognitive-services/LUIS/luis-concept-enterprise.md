---
title: Conceptos empresariales
titleSuffix: Language Understanding - Azure Cognitive Services
description: Comprender los conceptos de diseño para aplicaciones grandes de LUIS o aplicaciones múltiples con LUIS y QnA Maker juntos.
services: cognitive-services
author: diberry
manager: nitinme
ms.custom: seodec18
ms.service: cognitive-services
ms.subservice: language-understanding
ms.topic: conceptual
ms.date: 01/09/2019
ms.author: diberry
ms.openlocfilehash: e5d7e2bfe1ee4e3ca248f40701aa65e757fc4d74
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "60812860"
---
# <a name="enterprise-strategies-for-a-luis-app"></a>Estrategias de Enterprise para una aplicación de LUIS
Revise estas estrategias de diseño de la aplicación de empresa.

## <a name="when-you-expect-luis-requests-beyond-the-quota"></a>Si espera solicitudes de LUIS superiores a la cuota
Si la tasa de solicitudes de la aplicación de LUIS supera la [tasa de cuota](https://azure.microsoft.com/pricing/details/cognitive-services/language-understanding-intelligent-services/) permitida, reparta la carga entre más aplicaciones de LUIS con la [misma definición de aplicación](#use-multiple-apps-with-same-app-definition) o cree y [asigne varias claves](#assign-multiple-luis-keys-to-same-app) a la aplicación. 

### <a name="use-multiple-apps-with-same-app-definition"></a>Usar varias aplicaciones con la misma definición de aplicación
Exporte la aplicación de LUIS original y luego vuelva a importar la aplicación en aplicaciones independientes. Cada aplicación tiene su propio identificador de aplicación. Cuando se publica, en lugar de usar la misma clave en todas las aplicaciones, cree una clave independiente para cada aplicación. Equilibrar la carga entre todas las aplicaciones para que ninguna aplicación única se colapse. Adición de [Application Insights](luis-tutorial-bot-csharp-appinsights.md) para supervisar el uso. 

Para obtener la misma intención principal entre todas las aplicaciones, asegúrese de que la predicción de intención entre la primera y la segunda intención sea lo suficientemente amplia para que LUIS no se confunda y dé resultados diferentes entre aplicaciones con pequeñas variaciones en las expresiones. 

Designar una aplicación única como la maestra. Cualquier expresión que se sugiera para revisión debe agregarse a la aplicación maestra y luego devuelta a las demás aplicaciones. Esto implica una exportación completa de la aplicación, o bien cargar las expresiones etiquetadas desde la maestra a las secundarias. La carga se puede hacer desde el sitio web de [LUIS](luis-reference-regions.md) o la API de creación de una [expresión única](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c08) o para un [lote](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c09). 

Programe una [revisión de expresiones de punto de conexión](luis-how-to-review-endpoint-utterances.md) periódica para obtener un aprendizaje activo, por ejemplo, cada dos semanas, luego vuelva a entrenar y a publicar. 

### <a name="assign-multiple-luis-keys-to-same-app"></a>Asignar varias claves de LUIS a la misma aplicación
Si la aplicación de LUIS recibe más visitas del punto de conexión de las que permite la cuota de la clave única, cree y asigne más claves a la aplicación de LUIS. Cree un administrador de tráfico o un equilibrador de carga para administrar las consultas del punto de conexión entre claves del punto de conexión. 

## <a name="when-your-monolithic-app-returns-wrong-intent"></a>Si la aplicación monolítica devuelve una intención incorrecta
Si la aplicación se ha diseñado para predecir una amplia variedad de expresiones de usuario, considere la posibilidad de implementar el [modelo de distribución](#dispatch-tool-and-model). Si interrumpe una aplicación monolítica, permite que LUIS se centre en la detección correcta entre intenciones, en lugar de confundir intenciones entre las aplicaciones principales y las secundarias. 

Programe una [revisión de expresiones de punto de conexión](luis-how-to-review-endpoint-utterances.md) periódica para obtener un aprendizaje activo, por ejemplo, cada dos semanas, luego vuelva a entrenar y a publicar. 

## <a name="when-you-need-to-have-more-than-500-intents"></a>Si necesita tener más de 500 intenciones
Por ejemplo, supongamos que está desarrollando un asistente de oficina que tiene más de 500 intenciones. Si 200 intenciones se refieren a la programación de reuniones, 200 son de recordatorios, 200 para obtener información sobre compañeros de trabajo y 200 para el envío de correo electrónico, agrupe las intenciones de forma que cada grupo esté en una única aplicación, y luego cree una aplicación de nivel superior que contenga cada intención. Use la [herramienta de distribución y la arquitectura](#dispatch-tool-and-model) para compilar la aplicación de nivel superior. Después, cambie el bot para que use la llamada en cascada como se muestra en el [tutorial de distribución][dispatcher-application-tutorial]. 

## <a name="when-you-need-to-combine-several-luis-and-qna-maker-apps"></a>Si necesita combinar varias aplicaciones de LUIS y QnA Maker
Si tiene varias aplicaciones de LUIS y QnA Maker que necesitan responder a un bot, use la [herramienta de distribución](#dispatch-tool-and-model) para compilar la aplicación de nivel superior. Después, cambie el bot para que use la llamada en cascada como se muestra en el [tutorial de distribución][dispatcher-application-tutorial]. 

## <a name="dispatch-tool-and-model"></a>Modelo y herramienta de distribución
Use la herramienta de línea de comandos [Dispatch][dispatch-tool] que se encuentra en las [herramientas de BotBuilder](https://github.com/Microsoft/botbuilder-tools) para combinar varias aplicaciones de LUIS o QnA Maker en una aplicación principal de LUIS. Este enfoque permite disponer de un dominio primario que incluya todos los asuntos y dominios de sujeto secundarios diferentes en aplicaciones independientes. 

![Imagen conceptual de la arquitectura de distribución](./media/luis-concept-enterprise/dispatch-architecture.png)

El dominio principal se indica en LUIS con una versión denominada `Dispatch` en la lista de aplicaciones. 

El bot de chat recibe la expresión y después la envía a la aplicación principal de LUIS para la predicción. La intención de predicción superior de la aplicación principal determina a qué aplicación secundaria de LUIS se llama a continuación. El bot de chat envía la expresión a la aplicación secundaria para una predicción más específica.

Comprenda cómo se lleva a cabo esta jerarquía de llamadas con el [tutorial de la aplicación Dispatcher][dispatcher-application-tutorial] de Bot Builder v4.  

### <a name="intent-limits-in-dispatch-model"></a>Límites de intención en el modelo de distribución
Una aplicación de distribución tiene 500 orígenes de envío, que equivalen a un máximo de 500 intenciones. 

## <a name="next-steps"></a>Pasos siguientes

* Obtenga información sobre cómo [probar un lote](luis-how-to-batch-test.md).

[dispatcher-application-tutorial]: https://aka.ms/bot-dispatch
[dispatch-tool]: https://aka.ms/dispatch-tool
