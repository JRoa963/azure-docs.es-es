---
title: Ejemplo de desencadenador y enlace de Azure Functions
description: Aprenda a configurar los enlaces de función de Azure
services: functions
documentationcenter: na
author: craigshoemaker
manager: jeconnoc
ms.service: azure-functions
ms.devlang: multiple
ms.topic: reference
origin.date: 02/18/2019
ms.date: 03/04/2019
ms.author: v-junlch
ms.openlocfilehash: 6d5f9b171a4efc5e52d281655de143ac9d40d437
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61437895"
---
# <a name="azure-functions-trigger-and-binding-example"></a>Ejemplo de desencadenador y enlace de Azure Functions

En este artículo se muestra cómo configurar un [desencadenador y enlaces](./functions-triggers-bindings.md) en una función de Azure.

Supongamos que quiere escribir una fila nueva en Azure Table Storage cada vez que aparezca un nuevo mensaje en Azure Queue Storage. Este escenario puede implementarse mediante un desencadenador de Azure Queue Storage y un enlace de salida de Azure Table Storage. 

Este es un archivo *function.json* para este escenario. 

```json
{
  "bindings": [
    {
      "type": "queueTrigger",
      "direction": "in",
      "name": "order",
      "queueName": "myqueue-items",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    },
    {
      "type": "table",
      "direction": "out",
      "name": "$return",
      "tableName": "outTable",
      "connection": "MY_TABLE_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```

El primer elemento de la matriz `bindings` es el desencadenador de Queue Storage. Las propiedades `type` y `direction` identifican el desencadenador. La propiedad `name` identifica el parámetro de función que va a recibir el contenido del mensaje de cola. El nombre de la cola que supervisar está en `queueName` y la cadena de conexión, en la configuración de la aplicación identificada por `connection`.

El segundo elemento de la matriz `bindings` es el enlace de salida de Azure Table Storage. Las propiedades `type` y `direction` identifican el enlace. La propiedad `name` especifica cómo la función proporcionará la nueva fila de tabla, en este caso, con el valor devuelto de función. El nombre de la tabla está en `tableName` y la cadena de conexión, en la configuración de la aplicación identificada por `connection`.

Para ver y editar el contenido de *function.json* en el portal de Azure, haga clic en la opción **Editor avanzado** en la pestaña **Integrar** de la función.

> [!NOTE]
> El valor de `connection` es el nombre de una configuración de aplicación que contiene la cadena de conexión, no la propia cadena de conexión. Los enlaces utilizan las cadenas de conexión almacenadas en la configuración de la aplicación para que *function.json* no contenga secretos de los servicios (procedimiento recomendado).

## <a name="c-script-example"></a>Ejemplo de script de C#

Este es el código de script de C# que funciona con este enlace y este desencadenador. Tenga en cuenta que el nombre del parámetro que proporciona el contenido del mensaje de cola es `order`; este nombre es necesario porque el valor de propiedad `name`de *function.json* es `order`. 

```cs
#r "Newtonsoft.Json"

using Microsoft.Extensions.Logging;
using Newtonsoft.Json.Linq;

// From an incoming queue message that is a JSON object, add fields and write to Table storage
// The method return value creates a new row in Table Storage
public static Person Run(JObject order, ILogger log)
{
    return new Person() { 
            PartitionKey = "Orders", 
            RowKey = Guid.NewGuid().ToString(),  
            Name = order["Name"].ToString(),
            MobileNumber = order["MobileNumber"].ToString() };  
}
 
public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
    public string MobileNumber { get; set; }
}
```

## <a name="javascript-example"></a>Ejemplo de JavaScript

El mismo *function.json* archivo puede utilizarse con una función de JavaScript:

```javascript
// From an incoming queue message that is a JSON object, add fields and write to Table Storage
// The second parameter to context.done is used as the value for the new row
module.exports = function (context, order) {
    order.PartitionKey = "Orders";
    order.RowKey = generateRandomId(); 

    context.done(null, order);
};

function generateRandomId() {
    return Math.random().toString(36).substring(2, 15) +
        Math.random().toString(36).substring(2, 15);
}
```

## <a name="class-library-example"></a>Ejemplo de la biblioteca de clase

En una biblioteca de clases, los atributos proporcionan la misma información &mdash; de desencadenador y enlace (nombres de tabla y cola, cuentas de almacenamiento, parámetros de función de entrada y salida &mdash;), en lugar de un archivo function.json. Este es un ejemplo:

```csharp
public static class QueueTriggerTableOutput
{
    [FunctionName("QueueTriggerTableOutput")]
    [return: Table("outTable", Connection = "MY_TABLE_STORAGE_ACCT_APP_SETTING")]
    public static Person Run(
        [QueueTrigger("myqueue-items", Connection = "MY_STORAGE_ACCT_APP_SETTING")]JObject order,
        ILogger log)
    {
        return new Person() {
                PartitionKey = "Orders",
                RowKey = Guid.NewGuid().ToString(),
                Name = order["Name"].ToString(),
                MobileNumber = order["MobileNumber"].ToString() };
    }
}

public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
    public string MobileNumber { get; set; }
}
```

Ahora tiene una función de trabajo desencadenado por almacenamiento de tablas de Azure que envía los datos a una cola.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Los patrones de expresiones de enlace de Azure Functions](./functions-bindings-expressions-patterns.md)

