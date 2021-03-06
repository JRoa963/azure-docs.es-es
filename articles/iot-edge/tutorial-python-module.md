---
title: 'Creación del módulo personalizado de Python: Azure IoT Edge | Microsoft Docs'
description: En este tutorial, se explica cómo se crea un módulo IoT Edge con código Python y cómo se implementa en un dispositivo perimetral.
services: iot-edge
author: shizn
manager: philmea
ms.reviewer: kgremban
ms.author: xshi
ms.date: 03/24/2019
ms.topic: tutorial
ms.service: iot-edge
ms.custom: mvc, seodec18
ms.openlocfilehash: 0affd965bbfc587933a9cdbf5b96c470a6e4dd6a
ms.sourcegitcommit: c63fe69fd624752d04661f56d52ad9d8693e9d56
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2019
ms.locfileid: "58578295"
---
# <a name="tutorial-develop-and-deploy-a-python-iot-edge-module-to-your-simulated-device"></a>Tutorial: Desarrollo e implementación de un módulo de Python de IoT Edge en su dispositivo simulado

Los módulos Azure IoT Edge se pueden usar para implementar código que, a su vez, implementa una lógica de negocios directamente en los dispositivos IoT Edge. En este tutorial, se detallan los pasos para crear e implementar un módulo de IoT Edge que filtra los datos de sensor en el dispositivo IoT Edge que configuró en el inicio rápido. En este tutorial, aprenderá a:    

> [!div class="checklist"]
> * Usar Visual Studio Code para crear un módulo de Python para IoT Edge.
> * Utilizar Visual Studio Code y Docker para crear una imagen de Docker y publicarla en el Registro.
> * Implementar el módulo en el dispositivo IoT Edge.
> * Ver datos generados.


El módulo IoT Edge que creó en este tutorial filtra lo datos sobre la temperatura generados por el dispositivo. Solo envía mensajes a los niveles superiores si la temperatura sobrepasa el umbral especificado. Este tipo de análisis perimetral resulta útil para reducir la cantidad de datos que se comunican a la nube y se almacenan en ella. 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]


## <a name="prerequisites"></a>Requisitos previos

Un dispositivo de Azure IoT Edge:

* Puede usar una máquina de Azure como dispositivo de IoT Edge; para ello, siga los pasos que se indican en el artículo de inicio rápido para [Linux](quickstart-linux.md).
* Los módulos de Python para IoT Edge no admiten contenedores Windows.

Recursos en la nube:

* Una instancia de [IoT Hub](../iot-hub/iot-hub-create-through-portal.md) de nivel estándar o gratis en Azure. 

Recursos de desarrollo:

* [Visual Studio Code](https://code.visualstudio.com/) 
* [Azure IoT Tools](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-edge) para Visual Studio Code.
* [Extensión de Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python) para Visual Studio Code. 
* [Python](https://www.python.org/downloads/)
* [Pip](https://pip.pypa.io/en/stable/installing/#installation) para instalar paquetes de Python (normalmente, se incluye con la instalación de Python).
* [Docker CE](https://docs.docker.com/install/). 
  * Si está desarrollando en una máquina Windows, asegúrese de que Docker esté [configurado para usar contenedores de Linux](https://docs.docker.com/docker-for-windows/#switch-between-windows-and-linux-containers). 

>[!Note]
>Asegúrese de que su carpeta `bin` se encuentra en la ruta de acceso de su plataforma. Normalmente `~/.local/` para UNIX y macOS, o `%APPDATA%\Python` en Windows.

## <a name="create-a-container-registry"></a>Creación de un Registro de contenedor

En este tutorial, puede usar Azure IoT Tools para Visual Studio Code a fin de compilar un módulo y crear una **imagen de contenedor** a partir de los archivos. Después, insertará esta imagen en un **Registro** donde se almacenan y administran las imágenes. Por último, implementará la imagen en el Registro para que se ejecute en el dispositivo IoT Edge.  

Puede usar cualquier registro compatible con Docker para almacenar las imágenes de contenedor. Dos de los servicios de registro de Docker más conocidos son [Azure Container Registry](https://docs.microsoft.com/azure/container-registry/) y [Docker Hub](https://docs.docker.com/docker-hub/repos/#viewing-repository-tags). En este tutorial, utilizaremos Azure Container Registry. 

Si no dispone de un registro de contenedores, siga estos pasos para crear uno nuevo en Azure:

1. En [Azure Portal](https://portal.azure.com), seleccione **Crear un recurso** > **Contenedores** > **Container Registry**.

2. Especifique los siguientes valores para crear un registro de contenedor:

   | Campo | Valor | 
   | ----- | ----- |
   | Nombre de registro | Especifique un nombre único. |
   | Subscription | Seleccione una suscripción en la lista desplegable. |
   | Grupos de recursos | Se recomienda usar el mismo grupo de recursos para todos los recursos de prueba que se crean en las guías de inicio rápido y los tutoriales de IoT Edge. Por ejemplo, **IoTEdgeResources**. |
   | Ubicación | Elija una ubicación cercana a usted. |
   | Usuario administrador | Seleccione **Habilitar**. |
   | SKU | Seleccione **Básica**. | 

5. Seleccione **Crear**.

6. Una vez que se haya creado el Registro de contenedor, desplácese hasta él y seleccione **Claves de acceso**. 

7. Copie los valores de **Servidor de inicio de sesión**, **Nombre de usuario** y **Contraseña**. Utilice estos valores más adelante en el tutorial para proporcionar acceso al registro de contenedor. 

## <a name="create-an-iot-edge-module-project"></a>Creación de un proyecto de módulo IoT Edge
En los siguientes pasos creará un módulo de Python para IoT Edge mediante Visual Studio Code y Azure IoT Tools.

### <a name="create-a-new-solution"></a>Creación de una nueva solución

Use el paquete **cookiecutter** de Python para crear una plantilla con la que generar la solución. 

1. En Visual Studio Code, seleccione **Ver** > **Terminal** para abrir el terminal integrado de VS Code.

2. En el terminal, escriba el siguiente comando para instalar (o actualizar) **cookiecutter**, ya que lo necesitará para crear la plantilla de la solución de IoT Edge:

    ```cmd/sh
    pip install --upgrade --user cookiecutter
    ```
   >[!Note]
   >Asegúrese de que el directorio en el que se va a instalar cookiecutter está en la RUTA DE ACCESO de su entorno para que sea posible invocarlo desde un símbolo del sistema. El directorio es parte de la salida del script de instalación, por ejemplo `C:\Users\{user}\AppData\Roaming\Python\Python{version}\Scripts`.
   >
   >Reinicie Visual Studio Code para que recoja los cambios en la RUTA DE ACCESO. 

3. Seleccione **Ver** > **Paleta de comandos** para abrir la paleta de comandos de VS Code. 

4. En la paleta de comandos, escriba y ejecute el comando **Azure: Sign in** (Azure: iniciar sesión) y siga las instrucciones para iniciar sesión en la cuenta de Azure. Si ya ha iniciado sesión, puede omitir este paso.

5. En la paleta de comandos, escriba y ejecute el comando **Azure IoT Edge: New IoT Edge solution** (Azure IoT Edge: nueva solución de IoT Edge). Siga los mensajes y proporcione la siguiente información para crear la solución:

   | Campo | Valor |
   | ----- | ----- |
   | Seleccionar carpeta | Elija la ubicación en el equipo de desarrollo en la que VS Code creará los archivos de la solución. |
   | Proporcionar un nombre de la solución | Escriba un nombre descriptivo para la solución o acepte el valor predeterminado **EdgeSolution**. |
   | Seleccionar plantilla del módulo | Elija **Módulo de Python**. |
   | Proporcionar un nombre de módulo | Llame al módulo **PythonModule**. |
   | Proporcionar repositorio de imágenes de Docker del módulo | Un repositorio de imágenes incluye el nombre del registro de contenedor y el nombre de la imagen de contenedor. La imagen de contenedor se rellena previamente con el nombre que proporcionó en el último paso. Reemplace **localhost:5000** por el valor del servidor de inicio de sesión del registro de contenedor de Azure. Puede recuperar el servidor de inicio de sesión de la página de información general del registro de contenedor en Azure Portal. <br><br>El repositorio de imágenes final será similar a este: \<nombre del Registro\>.azurecr.io/pythonmodule. |
 
   ![Especificación del repositorio de imágenes de Docker](./media/tutorial-python-module/repository.png)

El área de trabajo de la solución de IoT Edge se carga en la ventana de Visual Studio Code. El área de trabajo de la solución contiene cinco componentes de nivel superior. La carpeta **modules** contiene el código de Pyhton del módulo, así como archivos Dockerfile para compilar el módulo como una imagen de contenedor. El archivo **\.env** almacena las credenciales del registro de contenedor. El archivo **deployment.template.json** contiene la información que usa el entorno de ejecución de IoT Edge para implementar módulos en un dispositivo. Y el archivo **deployment.debug.template.json** contiene la versión de depuración de los módulos. En este tutorial no se editarán la carpeta **\.vscode** ni el archivo **\.gitignore**.  

Si no especificó un registro de contenedor al crear la solución y aceptó el valor predeterminado localhost:5000, no tendrá un archivo \.env. 

<!--
   ![Python solution workspace](./media/tutorial-python-module/workspace.png)
-->

### <a name="add-your-registry-credentials"></a>Adición de las credenciales del Registro

El archivo del entorno almacena las credenciales del repositorio de contenedores y las comparte con el entorno de ejecución de IoT Edge. El entorno de ejecución necesita estas credenciales para extraer las imágenes privadas e insertarlas en el dispositivo IoT Edge. 

1. En el explorador de VS Code, abra el archivo **.env**. 
2. Actualice los campos con los valores de **nombre de usuario** y **contraseña** que ha copiado del Registro de contenedor de Azure. 
3. Guarde el archivo .env. 

### <a name="update-the-module-with-custom-code"></a>Actualización del módulo con código personalizado

Cada plantilla incluye un código de ejemplo, que toma los datos del sensor simulado del módulo **tempSensor** y los enruta al centro de IoT. En esta sección, agregue el código que expande **PythonModule** para analizar los mensajes antes de enviarlos. 

1. En el explorador de VS Code, abra **módulos**  > **PythonModule** > **main.py**.

2. En la parte superior del archivo **main.py**, importe la biblioteca **json**:

    ```python
    import json
    ```

3. Agregue las variables **TEMPERATURE_THRESHOLD** y **TWIN_CALLBACKS** bajo los contadores globales. El umbral de temperatura establece el valor que debe superar la temperatura de la máquina para que los datos se envíen al centro de IoT.

    ```python
    TEMPERATURE_THRESHOLD = 25
    TWIN_CALLBACKS = 0
    ```

4. Reemplace la función **receive_message_callback** por el código siguiente:

    ```python
    # receive_message_callback is invoked when an incoming message arrives on the specified 
    # input queue (in the case of this sample, "input1").  Because this is a filter module, 
    # we forward this message to the "output1" queue.
    def receive_message_callback(message, hubManager):
        global RECEIVE_CALLBACKS
        global TEMPERATURE_THRESHOLD
        message_buffer = message.get_bytearray()
        size = len(message_buffer)
        message_text = message_buffer[:size].decode('utf-8')
        print ( "    Data: <<<%s>>> & Size=%d" % (message_text, size) )
        map_properties = message.properties()
        key_value_pair = map_properties.get_internals()
        print ( "    Properties: %s" % key_value_pair )
        RECEIVE_CALLBACKS += 1
        print ( "    Total calls received: %d" % RECEIVE_CALLBACKS )
        data = json.loads(message_text)
        if "machine" in data and "temperature" in data["machine"] and data["machine"]["temperature"] > TEMPERATURE_THRESHOLD:
            map_properties.add("MessageType", "Alert")
            print("Machine temperature %s exceeds threshold %s" % (data["machine"]["temperature"], TEMPERATURE_THRESHOLD))
        hubManager.forward_event_to_output("output1", message, 0)
        return IoTHubMessageDispositionResult.ACCEPTED
    ```

5. Agregue una nueva función llamada **module_twin_callback**. Esta función se invoca cuando se actualicen las propiedades deseadas.

    ```python
    # module_twin_callback is invoked when the module twin's desired properties are updated.
    def module_twin_callback(update_state, payload, user_context):
        global TWIN_CALLBACKS
        global TEMPERATURE_THRESHOLD
        print ( "\nTwin callback called with:\nupdateStatus = %s\npayload = %s\ncontext = %s" % (update_state, payload, user_context) )
        data = json.loads(payload)
        if "desired" in data and "TemperatureThreshold" in data["desired"]:
            TEMPERATURE_THRESHOLD = data["desired"]["TemperatureThreshold"]
        if "TemperatureThreshold" in data:
            TEMPERATURE_THRESHOLD = data["TemperatureThreshold"]
        TWIN_CALLBACKS += 1
        print ( "Total calls confirmed: %d\n" % TWIN_CALLBACKS )
    ```

6. En la clase **HubManager**, agregue una nueva línea al método **__init__** para inicializar la función **module_twin_callback** que acaba de agregar:

    ```python
    # Sets the callback when a module twin's desired properties are updated.
    self.client.set_module_twin_callback(module_twin_callback, self)
    ```

7. Guarde el archivo main.py.

8. En el explorador de VS Code, abra el archivo **deployment.template.json** en el área de trabajo de la solución de IoT Edge. Este archivo le indica al agente de IoT Edge qué módulos implementar, en este caso **tempSensor** y **PythonModule**, y a IoT Edge Hub cómo enrutar los mensajes entre ellos. La extensión de Visual Studio Code rellena de forma automática la mayor parte de la información que necesita en la plantilla de implementación, aunque comprueba que todo sea correcto para la solución: 

   1. La plataforma predeterminada de la instancia de IoT Edge está establecida en **amd64** en la barra de estado de VS Code, lo que significa que **PythonModule** está establecido en la versión Linux amd64 de la imagen. Cambie la plataforma predeterminada en la barra de estado de **amd64** a **arm32v7** si esa es la arquitectura del dispositivo de IoT Edge. 

      ![Actualización de la plataforma de imagen del módulo](./media/tutorial-python-module/image-platform.png)

   2. Compruebe que la plantilla tiene el nombre de módulo correcto, no el nombre **SampleModule** predeterminado que cambió cuando creó la solución de IoT Edge.

   3. En la sección **registryCredentials** se almacenan las credenciales de Docker Registry, para que el agente de IoT Edge pueda extraer la imagen del módulo. Los pares reales de nombre de usuario y contraseña se almacenan en el archivo .env, que Git pasa por alto. Agregue sus credenciales al archivo .env si no lo ha hecho ya.  

   4. Si desea más información sobre los manifiestos de implementación, consulte [Obtenga información sobre cómo implementar módulos y establecer rutas en IoT Edge](module-composition.md).

9. Agregue el módulo gemelo de **PythonModule** que se corresponde con el manifiesto de implementación. Inserte el siguiente contenido JSON en la parte inferior de la sección **moduleContent**, después del módulo gemelo **$edgeHub**: 

   ```json
       "PythonModule": {
           "properties.desired":{
               "TemperatureThreshold":25
           }
       }
   ```

   ![Adición de un módulo gemelo a una plantilla de implementación](./media/tutorial-python-module/module-twin.png)

10. Guarde el archivo deployment.template.json.

## <a name="build-and-push-your-solution"></a>Compilación e inserción de la solución

En la sección anterior, creó una solución de IoT Edge y agregó código a **PythonModule** para filtrar los mensajes en los que la temperatura registrada por la máquina está por debajo del umbral aceptable. Ahora, tiene que compilar la solución como una imagen de contenedor e insertarla en el registro de contenedor. 

1. Escriba el comando siguiente en el terminal integrado de Visual Studio Code para iniciar sesión en Docker. A continuación, puede insertar la imagen del módulo en Azure Container Registry: 
     
   ```csh/sh
   docker login -u <ACR username> -p <ACR password> <ACR login server>
   ```
   Utilice el nombre de usuario, la contraseña y el servidor de inicio de sesión que copió de Azure Container Registry en la primera sección. También puede recuperar estos valores en la sección **Claves de acceso** del registro en Azure Portal.

   También puede ver una advertencia de seguridad que recomienda el uso del parámetro --password-stdin. Cuando su uso esté fuera del ámbito de este artículo, recomendamos seguir este procedimiento recomendado. Para más información, vea la referencia del comando [docker login](https://docs.docker.com/engine/reference/commandline/login/#provide-a-password-using-stdin). 


2. En el explorador de VS Code, haga clic con el botón derecho en el archivo deployment.template.json y seleccione **Build and Push IoT Edge solution** (Compilar e insertar solución de IoT Edge). 

Cuando le indica a Visual Studio Code que compile la solución, esta herramienta primero toma la información de la plantilla de implementación y genera un archivo deployment.json en una nueva carpeta denominada **config**. Después, ejecuta dos comandos en el terminal integrado: `docker build` y `docker push`. Estos dos comandos compilan el código, empaquetan el código Python en contenedores e insertan el código en el registro de contenedor que especificó cuando inicializó la solución. 

Puede ver la dirección completa de la imagen de contenedor con la etiqueta del comando `docker build` que se ejecuta en el terminal integrado de VS Code. La dirección de la imagen se crea a partir de la información del archivo module.json, con el formato \<repositorio\>:\<versión\>-\<plataforma\>. En este tutorial, debería ser similar a registryname.azurecr.io/pythonmodule:0.0.1-amd64.

>[!TIP]
>Si recibe un error al intentar compilar e insertar su módulo, realice las siguientes comprobaciones:
>* ¿Ha iniciado sesión en Docker en Visual Studio Code con las credenciales de su registro de contenedor? Estas credenciales son diferentes a las que se utilizan para iniciar sesión en Azure Portal.
>* ¿Es el repositorio de contenedor correcto? Abra **módulos** > **PythonModule** > **module.json** y busque el campo **repositorio**. El repositorio de imágenes final será similar a este: **\<nombre del Registro\>.azurecr.io/pythonmodule**. 
>* ¿Va a compilar el mismo tipo de contenedores que está ejecutando la máquina de desarrollo? Visual Studio Code establece de forma predeterminada contenedores de Linux amd64. Si el equipo de desarrollo ejecuta contenedores de Linux arm32v7, actualice la plataforma en la barra de estado azul en la parte inferior de la ventana de VS Code para que coincida. Los módulos de Python no son compatibles con los contenedores de Windows. 

## <a name="deploy-and-run-the-solution"></a>Implementación y ejecución de la solución

En el artículo de la guía de inicio rápido que siguió para configurar el dispositivo de IoT Edge, implementó un módulo mediante Azure Portal. También puede implementar módulos con la extensión Azure IoT Hub Toolkit (anteriormente, extensión Azure IoT Toolkit) para Visual Studio Code. Ya tiene un manifiesto de implementación preparado para su escenario, el archivo **deployment.json**. Ahora todo lo que necesita hacer es seleccionar un dispositivo que reciba la implementación.

1. En la paleta de comandos de VS Code, ejecute **Azure IoT Hub: Select IoT Hub** (Azure IoT Hub: seleccione IoT Hub). 

2. Elija la suscripción y la instancia de IoT Hub que contienen el dispositivo IoT Edge que desea configurar. 

3. En el explorador de VS Code, expanda la sección **Azure IoT Hub Devices** (Dispositivos de Azure IoT Hub). 

4. Haga clic con el botón derecho en el nombre del dispositivo IoT Edge y seleccione **Create Deployment for IoT Edge device** (Crear una implementación para un dispositivo individual). 

   ![Crear una implementación para un dispositivo individual](./media/tutorial-python-module/create-deployment.png)

5. Seleccione el archivo **deployment.amd64** o **deployment.arm32v7** (dependiendo de la arquitectura de destino) en la carpeta **config** y, a continuación, haga clic en **Seleccionar Edge Deployment Manifest**. No utilice el archivo deployment.template.json. 

6. Haga clic en el botón Actualizar. Debería ver el nuevo **PythonModule** en ejecución junto con el módulo **TempSensor**, así como **$edgeAgent** y **$edgeHub**. 

## <a name="view-generated-data"></a>Visualización de datos generados

Una vez aplicado el manifiesto de implementación al dispositivo de IoT Edge, el entorno de ejecución de IoT Edge del dispositivo recopila la información de implementación nueva y comienza a ejecutarse con ella. Los módulos que se ejecuten en el dispositivo y que no están incluidos en el manifiesto de implementación se detienen. Los módulos que falten en el dispositivo se inician. 

Puede ver el estado del dispositivo de IoT Edge con la sección **Azure IoT Hub Devices** (Dispositivos de Azure IoT Hub) del explorador de Visual Studio Code. Expanda los detalles del dispositivo para ver una lista de los módulos implementados y en ejecución. 

En el propio dispositivo de IoT Edge puede ver el estado de los módulos de implementación mediante el comando `iotedge list`. Debería ver cuatro módulos: los dos módulos personalizados del entorno de ejecución de IoT Edge, tempSensor y el sensor personalizado que ha creado en este tutorial. Los módulos pueden tardar unos minutos en comenzar; si no los ve inicialmente, vuelva a ejecutar el comando. 

Los mensajes que generan los módulos se ven con el comando `iotedge logs <module name>`. 

Puede ver los mensajes conforme llegan a IoT Hub mediante Visual Studio Code. 

1. Para supervisar los datos que llegan al centro de IoT, seleccione los puntos suspensivos (**...**) y, luego, **Start Monitoring D2C Messages** (Inicio de la supervisión de mensajes de D2C).
2. Para supervisar el mensaje de D2C de un determinado dispositivo, haga clic con el botón derecho en un dispositivo de la lista y seleccione **Start Monitoring D2C Messages** (Iniciar supervisión de mensajes de D2C).
3. Para detener la supervisión de datos, ejecute el comando **Azure IoT Hub: Stop Monitoring D2C Message** (Detener supervisión de mensaje de D2C) en la paleta de comandos. 
4. Para ver o actualizar el módulo gemelo, haga clic con el botón derecho en el módulo de la lista y seleccione **Edit module twin** (Editar módulo gemelo). Para actualizar el módulo gemelo, guarde el archivo JSON gemelo, haga clic con el botón derecho en el área del editor y seleccione **Update Module Twin** (Actualizar módulo gemelo).
5. Abra los registros de Docker e instale [la extensión de Docker para Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=PeterJausovec.vscode-docker). Puede encontrar los módulos que se están ejecutando localmente en el explorador de Docker. En el menú contextual, haga clic en **Show Logs** (Mostrar registros) en la vista del terminal integrado. 

## <a name="clean-up-resources"></a>Limpieza de recursos 

Si prevé seguir con el siguiente artículo recomendado, puede mantener los recursos y las configuraciones que ya ha creado y volverlos a utilizar. También puede seguir usando el mismo dispositivo de IoT Edge como dispositivo de prueba. 

En caso contrario, para evitar gastos, puede eliminar las configuraciones locales y los recursos de Azure que creó en este artículo. 

[!INCLUDE [iot-edge-clean-up-cloud-resources](../../includes/iot-edge-clean-up-cloud-resources.md)]


## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha creado un módulo IoT Edge que contiene código para filtrar datos sin procesar generados por el dispositivo IoT Edge. Puede continuar con los siguientes tutoriales para aprender otras formas en las que Azure IoT Edge puede ayudarle a convertir los datos en información empresarial en el perímetro.

> [!div class="nextstepaction"]
> [Implementación de Función de Azure como módulo](tutorial-deploy-function.md)
> [Implementación de Azure Stream Analytics como módulo](tutorial-deploy-stream-analytics.md)
