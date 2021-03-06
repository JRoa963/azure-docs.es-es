---
title: Creación de un dispositivo de puerta de enlace transparente con Azure IoT Edge | Microsoft Docs
description: Uso de un dispositivo Azure IoT Edge como una puerta de enlace transparente que puede procesar información para dispositivos de bajada
author: kgremban
manager: philmea
ms.author: kgremban
ms.date: 04/23/2019
ms.topic: conceptual
ms.service: iot-edge
services: iot-edge
ms.custom: seodec18
ms.openlocfilehash: 722ee6197b467454818026c960e1ce0e5b39efb4
ms.sourcegitcommit: 44a85a2ed288f484cc3cdf71d9b51bc0be64cc33
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2019
ms.locfileid: "64717197"
---
# <a name="configure-an-iot-edge-device-to-act-as-a-transparent-gateway"></a>Configuración de un dispositivo IoT Edge para que actúe como puerta de enlace transparente

Este artículo proporciona instrucciones detalladas para configurar dispositivos IoT Edge para que funcionen como una puerta de enlace transparente para que otros dispositivos se comuniquen con IoT Hub. En este artículo, el término *puerta de enlace IoT Edge* hace referencia a un dispositivo IoT Edge que se usa como una puerta de enlace transparente. Para obtener más información, consulte [cómo un dispositivo IoT Edge puede utilizarse como una puerta de enlace](./iot-edge-as-gateway.md).

>[!NOTE]
>Actualmente:
> * Si la puerta de enlace se desconecta de IoT Hub, los dispositivos de nivel inferior no se pueden autenticar con la puerta de enlace.
> * Los dispositivos habilitados para Edge no pueden conectarse a puertas de enlace de IoT Edge. 
> * Los dispositivos de bajada no pueden usar la carga de archivos.

Para que un dispositivo funcione como una puerta de enlace, debe poder conectarse de forma segura a los dispositivos de bajada. Azure IoT Edge le permite usar una infraestructura de clave pública (PKI) para configurar conexiones seguras entre los dispositivos. En este caso, vamos a permitir que un dispositivo de bajada se conecte a un dispositivo IoT Edge que actúa como puerta de enlace transparente. Para mantener una seguridad razonable, el dispositivo de nivel inferior debe confirmar la identidad del dispositivo IoT Edge. Desea que los dispositivos se conectan a solo las puertas de enlace, no las puertas de enlace potencialmente malintencionados.

Un dispositivo de bajada puede ser cualquier aplicación o plataforma que tenga una identidad creada con el servicio en la nube [Azure IoT Hub](https://docs.microsoft.com/azure/iot-hub). En muchos casos, estas aplicaciones utilizan el [SDK de dispositivo IoT de Azure](../iot-hub/iot-hub-devguide-sdks.md). En la práctica, un dispositivo de bajada podría ser incluso una aplicación que se ejecuta en el propio dispositivo de puerta de enlace IoT Edge. 

Puede crear cualquier infraestructura de certificados que permita la confianza necesaria para la topología de la puerta de enlace de dispositivo. En este artículo, se supone que la misma configuración de certificado que usaría para habilitar [seguridad de la entidad de certificación X.509](../iot-hub/iot-hub-x509ca-overview.md) en IoT Hub, lo que implica un certificado de entidad de certificación X.509 asociado a un centro de IoT específico (el propietario de hub IoT CA) y una serie de certificados, firmados con esta entidad de certificación y una entidad de certificación para el dispositivo de IoT Edge.

![Configuración del certificado de puerta de enlace](./media/how-to-create-transparent-gateway/gateway-setup.png)

La puerta de enlace presenta su IoT Edge certificado de entidad emisora de certificados de dispositivo para el dispositivo de nivel inferior durante el inicio de la conexión. El dispositivo de nivel inferior se comprueba para asegurarse de que el certificado de entidad emisora de certificados de dispositivo IoT Edge está firmado por el certificado de entidad de certificación del propietario. Este proceso permite que el dispositivo de bajada confirme que la puerta de enlace procede de un origen de confianza.

Los pasos siguientes le guían por el proceso de crear los certificados e instalarlos en los lugares adecuados.

## <a name="prerequisites"></a>Requisitos previos

Un dispositivo Azure IoT Edge para su configuración como una puerta de enlace. Use los pasos de instalación de IoT Edge para los sistemas operativos siguientes:
* [Windows](./how-to-install-iot-edge-windows.md)
* [Linux x64](./how-to-install-iot-edge-linux.md)
* [Linux ARM32](./how-to-install-iot-edge-linux-arm.md)

Puede usar cualquier máquina para generar los certificados y, a continuación, copiarlos en el dispositivo IoT Edge.

>[!NOTE]
>El "nombre de puerta de enlace" usado para crear los certificados de esta instrucción, debe ser el mismo nombre que se usa como nombre de host en el archivo config.yaml de IoT Edge y como GatewayHostName en la cadena de conexión del dispositivo de nivel inferior. El "nombre de la puerta de enlace" debe poderse resolver con una dirección IP, ya sea mediante DNS o una entrada de archivo host. La comunicación se basa en el protocolo usado (MQTTS:8883 / AMQPS:5671 / HTTPS:433) debe ser posible entre el dispositivo de nivel inferior y el sea transparente IoT Edge. Si existe un firewall entre ellos, es necesario abrir el puerto correspondiente.

## <a name="generate-certificates-with-windows"></a>Generación de certificados con Windows

Use los pasos de esta sección para generar certificados de prueba en un dispositivo Windows. Puede utilizar estos pasos para generar los certificados en un dispositivo Windows IoT Edge. O bien, puede generar los certificados en el equipo de desarrollo de Windows y, a continuación, cópielos en cualquier dispositivo de IoT Edge. 

Los certificados generados en esta sección están pensados solo para fines de prueba. 

### <a name="install-openssl"></a>Instalación de OpenSSL

Instale OpenSSL para Windows en el equipo que usa para generar los certificados. Existen varias maneras de instalar OpenSSL:

   >[!NOTE]
   >Si ya ha instalado OpenSSL en el dispositivo Windows, puede omitir este paso, pero asegúrese de que openssl.exe está disponible en la variable de entorno PATH.

* **Más fácil:** Descargue e instale cualquier [archivo binario de OpenSSL de terceros](https://wiki.openssl.org/index.php/Binaries), por ejemplo, de [este proyecto en SourceForge](https://sourceforge.net/projects/openssl/). Agregue la ruta de acceso completa al archivo openssl.exe a la variable de entorno PATH. 
   
* **Se recomienda que use:** Descargue el código fuente de OpenSSL y compile los archivos binarios en su máquina por sí mismo o a través de [vcpkg](https://github.com/Microsoft/vcpkg). Las instrucciones que aparecen a continuación usan vcpkg para descargar el código fuente, compilar e instalar OpenSSL en el equipo Windows con pasos fáciles.

   1. Vaya al directorio donde quiera instalar vcpkg. Nos referiremos a este directorio como *\<VCPKGDIR>*. Siga las instrucciones para descargar e instalar [vcpkg](https://github.com/Microsoft/vcpkg).
   
   2. Después de instalar vcpkg, desde un símbolo del sistema de Powershell, ejecute el siguiente comando para instalar el paquete de OpenSSL para Windows x64. Esta instalación suele tardar, aproximadamente, 5 minutos en completarse.

      ```powershell
      .\vcpkg install openssl:x64-windows
      ```
   3. Agregue `<VCPKGDIR>\installed\x64-windows\tools\openssl` a la variable de entorno PATH para que el archivo openssl.exe esté disponible para su invocación.

### <a name="prepare-creation-scripts"></a>Preparación de los scripts de creación

El SDK de dispositivo IoT de Azure para C contiene scripts que puede usar para generar certificados de prueba. En esta sección, va a clonar el SDK y configurar PowerShell.

1. Abra una ventana de Azure PowerShell en modo de administrador. 

2. Clone el repositorio de git que contiene los scripts para generar los certificados para entornos que no sean de producción. Estos scripts ayudan a crear los certificados necesarios para configurar una puerta de enlace transparente. Use el comando `git clone` o [descargue el archivo ZIP](https://github.com/Azure/azure-iot-sdk-c/archive/master.zip). 

   ```powershell
   git clone https://github.com/Azure/azure-iot-sdk-c.git
   ```

3. Vaya al directorio en el que quiere trabajar. Nos referiremos a este directorio como *\<WRKDIR>*.  Todos los archivos se crearán en este directorio.

4. Copie los archivos de configuración y de script en el directorio de trabajo. 

   ```powershell
   copy <path>\azure-iot-sdk-c\tools\CACertificates\*.cnf .
   copy <path>\azure-iot-sdk-c\tools\CACertificates\ca-certs.ps1 .
   ```

   Si descargó el SDK como un archivo ZIP, el nombre de la carpeta es `azure-iot-sdk-c-master` y el resto de la ruta de acceso es la misma. 

5. Establezca la variable de entorno OPENSSL_CONF para que use el archivo de configuración openssl_root_ca.cnf.

    ```powershell
    $env:OPENSSL_CONF = "$PWD\openssl_root_ca.cnf"
    ```

6. Habilite PowerShell para ejecutar los scripts.

   ```powershell
   Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope CurrentUser
   ```

7. Lleve las funciones, usadas por los scripts, al espacio de nombres global de PowerShell.
   
   ```powershell
   . .\ca-certs.ps1
   ```

8. Compruebe que OpenSSL se ha instalado correctamente y asegúrese de que no haya conflictos de nombres con los certificados existentes. Si hay problemas, el script debe describir cómo corregirlos en el sistema.

   ```powershell
   Test-CACertsPrerequisites
   ```

### <a name="create-certificates"></a>Creación de certificados

En esta sección, se crean tres certificados y, a continuación, se conectan en una cadena. La colocación de los certificados en un archivo de cadena permite instalarlos fácilmente en el dispositivo de puerta de enlace IoT Edge y los dispositivos de bajada.  

1. Cree el certificado de entidad de certificación de propietario y firme con él un certificado intermedio. Los certificados se colocan en *\<WRKDIR>*.

      ```powershell
      New-CACertsCertChain rsa
      ```

2. Crear IoT Edge de certificado de entidad emisora de certificados de dispositivo y la clave privada con el siguiente comando. Proporcione un nombre para el dispositivo de puerta de enlace, que se usará para dar nombre a los archivos y durante la generación del certificado. 

   ```powershell
   New-CACertsEdgeDevice "<gateway name>"
   ```

3. Crear una cadena de certificados desde el certificado de entidad de certificación del propietario, el certificado intermedio y el certificado de entidad emisora de certificados de dispositivo IoT Edge con el siguiente comando. 

   ```powershell
   Write-CACertsCertificatesForEdgeDevice "<gateway name>"
   ```

   El script crea los certificados y la clave siguientes:
   * `<WRKDIR>\certs\new-edge-device.*`
   * `<WRKDIR>\private\new-edge-device.key.pem`
   * `<WRKDIR>\certs\azure-iot-test-only.root.ca.cert.pem`

## <a name="generate-certificates-with-linux"></a>Generación de certificados con Linux

Use los pasos de esta sección para generar certificados de prueba en un dispositivo Linux. Puede generar los certificados en el propio dispositivo IoT Edge o utilizar un equipo independiente y copiar los certificados finales en cualquier dispositivo IoT Edge que ejecute un sistema operativo compatible. 

### <a name="prepare-creation-scripts"></a>Preparación de los scripts de creación

1. Clone el repositorio de git que contiene los scripts para generar los certificados para entornos que no sean de producción. Estos scripts ayudan a crear los certificados necesarios para configurar una puerta de enlace transparente. 

   ```bash
   git clone https://github.com/Azure/azure-iot-sdk-c.git
   ```

2. Vaya al directorio en el que quiere trabajar. Nos referiremos a este directorio como *\<WRKDIR>*.  Todos los archivos se crearán en este directorio.
  
3. Copie los archivos de configuración y de script en el directorio de trabajo.

   ```bash
   cp <path>/azure-iot-sdk-c/tools/CACertificates/*.cnf .
   cp <path>/azure-iot-sdk-c/tools/CACertificates/certGen.sh .
   ```

4. Configure OpenSSL para generar los certificados mediante el script proporcionado. 

   ```bash
   chmod 700 certGen.sh 
   ```

### <a name="create-certificates"></a>Creación de certificados

En esta sección, se crean tres certificados y, a continuación, se conectan en una cadena. La colocación de los certificados en un archivo de cadena permite instalarlos fácilmente en el dispositivo de puerta de enlace IoT Edge y los dispositivos de bajada.  

1. Cree el certificado de entidad de certificación de propietario y un certificado intermedio. Estos certificados se colocan en *\<WRKDIR>*.

   ```bash
   ./certGen.sh create_root_and_intermediate
   ```

   El script crea los certificados y las claves siguientes:
   * `<WRKDIR>/certs/azure-iot-test-only.root.ca.cert.pem`
   * `<WRKDIR>/certs/azure-iot-test-only.intermediate.cert.pem`
   * `<WRKDIR>/private/azure-iot-test-only.root.ca.key.pem`
   * `<WRKDIR>/private/azure-iot-test-only.intermediate.key.pem`

2. Crear IoT Edge de certificado de entidad emisora de certificados de dispositivo y la clave privada con el siguiente comando. Proporcione un nombre para el dispositivo de puerta de enlace, que se usará para dar nombre a los archivos y durante la generación del certificado. 

   ```bash
   ./certGen.sh create_edge_device_certificate "<gateway name>"
   ```

   El script crea los certificados y la clave siguientes:
   * `<WRKDIR>/certs/new-edge-device.*`
   * `<WRKDIR>/private/new-edge-device.key.pem`

3. Crear una cadena de certificados denominada **nueva-edge-dispositivo-full-chain.cert.pem** desde el certificado de entidad de certificación del propietario, certificados intermedios y certificado de entidad emisora de certificados de dispositivo IoT Edge.

   ```bash
   cat ./certs/new-edge-device.cert.pem ./certs/azure-iot-test-only.intermediate.cert.pem ./certs/azure-iot-test-only.root.ca.cert.pem > ./certs/new-edge-device-full-chain.cert.pem
   ```

## <a name="install-certificates-on-the-gateway"></a>Instalación de los certificados en la puerta de enlace

Ahora que ha creado una cadena de certificados, debe instalarla en el dispositivo de puerta de enlace IoT Edge y configurar el entorno de ejecución de IoT Edge para que haga referencia a los nuevos certificados. 

1. Copie los archivos siguientes desde *\<WRKDIR>*. Guárdelos en cualquier lugar en el dispositivo IoT Edge. Nos referiremos al directorio de destino en el dispositivo IoT Edge como *\<CERTDIR>*. 

   Si ha generado los certificados en el propio dispositivo de IoT Edge, puede omitir este paso y usar la ruta de acceso al directorio de trabajo.

   * Certificado de entidad de certificación del dispositivo: `<WRKDIR>\certs\new-edge-device-full-chain.cert.pem`
   * Clave privada de entidad de certificación del dispositivo: `<WRKDIR>\private\new-edge-device.key.pem`
   * Entidad de certificación del propietario: `<WRKDIR>\certs\azure-iot-test-only.root.ca.cert.pem`

2. Abra el archivo de configuración del demonio de seguridad de IoT Edge. 

   * Windows: `C:\ProgramData\iotedge\config.yaml`
   * Linux: `/etc/iotedge/config.yaml`

3. Establezca las propiedades del **certificado** en el archivo config.yaml en la ruta de acceso en la que ha colocado los archivos de certificado y de clave en el dispositivo IoT Edge.

   * Windows:

      ```yaml
      certificates:
        device_ca_cert: "<CERTDIR>\\certs\\new-edge-device-full-chain.cert.pem"
        device_ca_pk: "<CERTDIR>\\private\\new-edge-device.key.pem"
        trusted_ca_certs: "<CERTDIR>\\certs\\azure-iot-test-only.root.ca.cert.pem"
      ```
   
   * Linux: 
      ```yaml
      certificates:
        device_ca_cert: "<CERTDIR>/certs/new-edge-device-full-chain.cert.pem"
        device_ca_pk: "<CERTDIR>/private/new-edge-device.key.pem"
        trusted_ca_certs: "<CERTDIR>/certs/azure-iot-test-only.root.ca.cert.pem"
      ```

4. En los dispositivos de Linux, asegúrese de que el usuario **iotedge** tiene permisos para el directorio que contiene los certificados de lectura. 

## <a name="deploy-edgehub-to-the-gateway"></a>Implementación de EdgeHub en la puerta de enlace

Cuando instala por primera vez IoT Edge en un dispositivo, el módulo de un único sistema se inicia automáticamente: el agente de IoT Edge. Para que el dispositivo funcione como una puerta de enlace, necesita ambos módulos del sistema. Si no ha implementado todos los módulos en el dispositivo de puerta de enlace antes de, cree una implementación del dispositivo iniciar el segundo módulo del sistema, el centro de IoT Edge. La implementación parecerá vacía porque no agrega ningún módulo en el asistente, pero implementará ambos módulos del sistema. 

Puede comprobar qué módulos se ejecutan en un dispositivo con el comando `iotedge list`.

1. En Azure Portal, vaya hasta el centro de IoT.

2. Vaya a **IoT Edge** y seleccione el dispositivo IoT Edge que quiere usar como puerta de enlace.

3. Seleccione **Set modules** (Establecer módulos).

4. Seleccione **Next** (Siguiente).

5. En la página **Specify routes** (Especificar rutas), debe tener una ruta predeterminada que envíe todos los mensajes de todos los módulos a IoT Hub. Si no es así, agregue el código siguiente y seleccione **Next** (Siguiente).

   ```JSON
   {
       "routes": {
           "route": "FROM /* INTO $upstream"
       }
   }
   ```

6. En la página **Review template** (Revisar plantilla), seleccione **Submit** (Enviar).

## <a name="open-ports-on-gateway-device"></a>Abrir puertos en el dispositivo de puerta de enlace

Los dispositivos de IoT Edge estándares no necesitan conectividad entrante a la función, porque toda la comunicación con IoT Hub se realiza a través de las conexiones salientes. Sin embargo, los dispositivos de puerta de enlace son diferentes porque tienen que ser capaz de recibir mensajes desde sus dispositivos de nivel inferior.

Para que un escenario de puerta de enlace trabajar, al menos uno de los protocolos admitidos del centro de IoT Edge debe estar abierto para el tráfico entrante desde dispositivos de nivel inferior. Los protocolos compatibles son MQTT, AMQP y HTTPS.

| Port | Protocol |
| ---- | -------- |
| 8883 | MQTT |
| 5671 | AMQP |
| 443 | HTTPS <br> MQTT + WS <br> AMQP + WS | 

## <a name="route-messages-from-downstream-devices"></a>Enrutamiento de mensajes desde dispositivos de bajada
El entorno de ejecución de Azure IoT Edge puede enrutar los mensajes enviados desde dispositivos de bajada igual que los mensajes enviados por los módulos. Esta característica permite realizar análisis en un módulo que se ejecutan en la puerta de enlace antes de enviar datos a la nube. 

Actualmente, la manera de enrutar los mensajes enviados por los dispositivos de bajada es diferenciándolos de los mensajes enviados por los módulos. Los mensajes enviados por los módulos contienen una propiedad del sistema denominada **connectionModuleId**, pero los mensajes enviados por los dispositivos de bajada no la tienen. Puede usar la cláusula WHERE de la ruta para excluir los mensajes que contengan dicha propiedad del sistema. 

La siguiente ruta se usaría para enviar mensajes desde cualquier dispositivo de bajada a un módulo denominado `ai_insights`.

```json
{
    "routes":{
        "sensorToAIInsightsInput1":"FROM /messages/* WHERE NOT IS_DEFINED($connectionModuleId) INTO BrokeredEndpoint(\"/modules/ai_insights/inputs/input1\")", 
        "AIInsightsToIoTHub":"FROM /messages/modules/ai_insights/outputs/output1 INTO $upstream" 
    } 
}
```

Para obtener más información sobre el enrutamiento de mensajes, vea [Implementar módulos y establecer rutas](./module-composition.md#declare-routes).

[!INCLUDE [iot-edge-extended-ofline-preview](../../includes/iot-edge-extended-offline-preview.md)]

## <a name="next-steps"></a>Pasos siguientes

Ahora que tiene un dispositivo IoT Edge que funciona como una puerta de enlace transparente, deberá configurar los dispositivos de bajada para que confíen en la puerta de enlace y envíen mensajes. Para más información, consulte [Conexión de un dispositivo de bajada a una puerta de enlace Azure IoT Edge](how-to-connect-downstream-device.md).
