---
title: 'Início Rápido: Enviar telemetria ao Hub IoT do Azure (Python) | Microsoft Docs'
description: Neste início rápido, você executa um aplicativo Python de exemplo para enviar telemetria simulada a um hub IoT e usar um utilitário para ler a telemetria do Hub IoT.
author: dominicbetts
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.devlang: python
ms.topic: quickstart
ms.custom: mvc
ms.date: 01/22/2019
ms.author: dobett
ms.openlocfilehash: 104be28d1b438dc862b2b8a2effd51be4b9b2bc9
ms.sourcegitcommit: fea5a47f2fee25f35612ddd583e955c3e8430a95
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2019
ms.locfileid: "55510911"
---
# <a name="quickstart-send-telemetry-from-a-device-to-an-iot-hub-and-read-it-with-a-back-end-application-python"></a>Início rápido: Enviar a telemetria de um dispositivo para um hub IoT e lê-la com um back-end (Python)

[!INCLUDE [iot-hub-quickstarts-1-selector](../../includes/iot-hub-quickstarts-1-selector.md)]

O Hub IoT é um serviço do Azure que permite a ingestão de grandes volumes de telemetria de seus dispositivos IoT pela nuvem para processamento ou armazenamento. Neste início rápido, você envia telemetria de um aplicativo de dispositivo simulado, por meio do Hub IoT, para um aplicativo de back-end para processamento.

Este início rápido usa um aplicativo Python previamente codificado para enviar a telemetria, e um utilitário CLI para ler a telemetria do Hub. Antes de executar esses dois aplicativos, você cria um hub IoT e registra um dispositivo com o hub.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

## <a name="prerequisites"></a>Pré-requisitos

Os dois exemplos de aplicativo executados neste início rápido são escritos usando Python. Você precisa do Python 2.7.x ou 3.5.x no computador de desenvolvimento.

Você pode fazer o download do Python para várias plataformas a partir do [Python.org](https://www.python.org/downloads/). O instalador do Python que você escolher deve ser baseado na arquitetura do sistema com a qual você está trabalhando. Se a arquitetura de CPU do sistema for de 32 bits, baixe o x86, que é o instalador padrão, em Python.org. Para a arquitetura de 64 bits, é necessário baixar o instalador de x86-64.

Você pode verificar a versão atual do Python no computador de desenvolvimento usando um dos seguintes comandos:

```python
python --version
```

```python
python3 --version
```

Faça o download do projeto de exemplo de Python do https://github.com/Azure-Samples/azure-iot-samples-python/archive/master.zip e extraia o arquivo ZIP.

## <a name="create-an-iot-hub"></a>Crie um hub IoT

[!INCLUDE [iot-hub-include-create-hub](../../includes/iot-hub-include-create-hub.md)]

## <a name="register-a-device"></a>Registrar um dispositivo

Um dispositivo deve ser registrado no hub IoT antes de poder se conectar. Neste início rápido, você usa o Azure Cloud Shell para registrar um dispositivo simulado.

1. Execute os seguintes comandos no Azure Cloud Shell para adicionar a extensão da CLI do Hub IoT e criar a identidade do dispositivo. 

    **YourIoTHubName**: substitua o espaço reservado abaixo pelo nome escolhido para o hub IoT.

    **MyPythonDevice**: Esse é o nome fornecido para o dispositivo registrado. Use MyPythonDevice conforme mostrado. Se você escolher um nome diferente para seu dispositivo, você também precisará usar esse nome ao longo deste artigo e atualizar o nome de dispositivo nos aplicativos de exemplo antes de executá-los.

    ```azurecli-interactive
    az extension add --name azure-cli-iot-ext
    az iot hub device-identity create --hub-name YourIoTHubName --device-id MyPythonDevice
    ```

1. Execute os seguintes comandos no Azure Cloud Shell para obter a _cadeia de conexão de dispositivo_ referente ao dispositivo que você acabou de registrar:

    **YourIoTHubName**: substitua o espaço reservado abaixo pelo nome escolhido para o hub IoT.

    ```azurecli-interactive
    az iot hub device-identity show-connection-string --hub-name YourIoTHubName --device-id MyPythonDevice --output table
    ```

    Tome nota da cadeia de conexão do dispositivo, que se parece com:

   `HostName={YourIoTHubName}.azure-devices.net;DeviceId=MyNodeDevice;SharedAccessKey={YourSharedAccessKey}`

    Você usará esse valor posteriormente no início rápido.

## <a name="send-simulated-telemetry"></a>Enviar telemetria simulada

O aplicativo de dispositivo simulado se conecta a um ponto de extremidade específico do dispositivo em seu hub IoT e envia telemetria simulada de temperatura e umidade.

1. Em uma janela de terminal local, navegue até a pasta raiz do projeto Python de exemplo. Em seguida, navegue até a pasta **iot-hub\Quickstarts\simulated-device**.

1. Abra o arquivo **SimulatedDevice.py** em seu editor de texto preferido.

    Substitua o valor da variável `CONNECTION_STRING` pela cadeia de conexão do dispositivo que você anotou anteriormente. Salve as alterações no arquivo **SimulatedDevice.py**.

1. Na janela de terminal local, execute os seguintes comandos para instalar as bibliotecas necessárias para o aplicativo de dispositivo simulado:

    ```cmd/sh
    pip install azure-iothub-device-client
    ```

1. Na janela de terminal local, execute os seguintes comandos para executar o aplicativo de dispositivo simulado:

    ```cmd/sh
    python SimulatedDevice.py
    ```

    A captura de tela a seguir mostra o resultado à medida que o aplicativo de dispositivo simulado envia telemetria para o seu hub IoT:

    ![Executar o dispositivo simulado](media/quickstart-send-telemetry-python/SimulatedDevice.png)

## <a name="read-the-telemetry-from-your-hub"></a>Ler a telemetria do hub

A extensão de CLI do Hub IoT pode se conectar ao ponto de extremidade **Eventos** do lado do serviço em seu Hub IoT. A extensão recebe as mensagens do dispositivo para a nuvem, enviadas de seu dispositivo simulado. Um aplicativo de back-end do Hub IoT normalmente é executado na nuvem para receber e processar as mensagens do dispositivo para a nuvem.

Execute os seguintes comandos no Azure Cloud Shell, substituindo `YourIoTHubName` pelo nome do Hub IoT:

```azurecli-interactive
az iot hub monitor-events --hub-name YourIoTHubName --device-id MyPythonDevice 
```

A captura de tela a seguir mostra a saída à medida que a extensão recebe a telemetria enviada pelo dispositivo simulado para o hub:

![Executar o aplicativo de back-end](media/quickstart-send-telemetry-python/ReadDeviceToCloud.png)

## <a name="clean-up-resources"></a>Limpar recursos

[!INCLUDE [iot-hub-quickstarts-clean-up-resources](../../includes/iot-hub-quickstarts-clean-up-resources.md)]

## <a name="next-steps"></a>Próximas etapas

Neste início rápido, você configurou um hub IoT, registrou um dispositivo, enviou telemetria simulada para o hub usando um aplicativo Python e leu a telemetria do hub usando um aplicativo de back-end simples.

Para saber como controlar o dispositivo simulado em um aplicativo de back-end, continue no próximo início rápido.

> [!div class="nextstepaction"]
> [Início Rápido: Controlar um dispositivo conectado a um hub IoT](quickstart-control-device-python.md)