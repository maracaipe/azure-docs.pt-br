---
title: 'Início rápido: Criar um projeto de detecção de objeto com o SDK de Visão Personalizada para C#'
titlesuffix: Azure Cognitive Services
description: Crie um projeto, adicione marcas, faça upload de imagens, treine seu projeto e detecte objetos usando o SDK do .NET com C#.
services: cognitive-services
author: areddish
manager: nitinme
ms.service: cognitive-services
ms.subservice: custom-vision
ms.topic: quickstart
ms.date: 10/31/2018
ms.author: areddish
ms.openlocfilehash: 9d8340d505308753855fa0fcd286949e80d3ecaa
ms.sourcegitcommit: 90cec6cccf303ad4767a343ce00befba020a10f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/07/2019
ms.locfileid: "55879268"
---
# <a name="quickstart-create-an-object-detection-project-with-the-custom-vision-net-sdk"></a>Início rápido: Criar um projeto de detecção de objeto com o SDK do .NET para Visão Personalizada

Este artigo fornece informações e código de exemplo para ajudar você a começar a usar o SDK da Visão Personalizada com C# para criar um modelo de detecção de objeto. Depois de criada, você poderá adicionar regiões marcadas, fazer upload de imagens, treinar o projeto, obter a URL de ponto de extremidade de previsão do projeto padrão e usar o ponto de extremidade para testar programaticamente uma imagem. Use este exemplo como um modelo para criar seu próprio aplicativo .NET. 

## <a name="prerequisites"></a>Pré-requisitos

- Qualquer edição do [Visual Studio 2015 ou 2017](https://www.visualstudio.com/downloads/)

## <a name="get-the-custom-vision-sdk-and-sample-code"></a>Obter o SDK de Visão Personalizada e um exemplo de código
Para escrever um aplicativo .NET que usa a Visão Personalizada, você precisará dos pacotes NuGet da Visão Personalizada. Eles estão incluídos no projeto de exemplo que você vai baixar, mas é possível acessá-los individualmente aqui.

* [Microsoft.Azure.CognitiveServices.Vision.CustomVision.Training](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Vision.CustomVision.Training/)
* [Microsoft.Azure.CognitiveServices.Vision.CustomVision.Prediction](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Vision.CustomVision.Prediction/)

Clone ou baixe o projeto [Exemplos de .NET dos Serviços Cognitivos](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples). Navegue até a pasta **CustomVision/ObjectDetection** e abra _ObjectDetection.csproj_ no Visual Studio.

Este projeto do Visual Studio cria um novo projeto de Visão Personalizada denominado __My New Project__, que pode ser acessado pelo [site da Visão Personalizada](https://customvision.ai/). Ele carrega as imagens para treinar e testar um modelo de detecção de objeto. Neste projeto, o modelo é treinado para detectar garfos e tesouras nas imagens.

[!INCLUDE [get-keys](includes/get-keys.md)]

## <a name="understand-the-code"></a>Compreender o código

Abra o arquivo _Program.cs_ e inspecione o código. Insira suas chaves de assinatura nas definições pertinentes no método **Main**.

[!code-csharp[](~/cognitive-services-dotnet-sdk-samples/CustomVision/ObjectDetection/Program.cs?range=18-27)]

O parâmetro de ponto de extremidade deve apontar para a região em que o grupo de recursos do Azure que contém os recursos de Visão Personalizada foi criado. Para este exemplo, consideramos a região Centro-Sul dos EUA e usamos:

[!code-csharp[](~/cognitive-services-dotnet-sdk-samples/CustomVision/ImageClassification/Program.cs?range=14-14)]

### <a name="create-a-new-custom-vision-service-project"></a>Criar um novo projeto do Serviço de Visão Personalizada

Este próximo trecho de código cria um projeto de detecção de objeto. O projeto criado será exibido no [site da Visão Personalizada](https://customvision.ai/) visitado anteriormente. 

[!code-csharp[](~/cognitive-services-dotnet-sdk-samples/CustomVision/ObjectDetection/Program.cs?range=29-35)]

### <a name="add-tags-to-the-project"></a>Adicionar marcas ao projeto

[!code-csharp[](~/cognitive-services-dotnet-sdk-samples/CustomVision/ObjectDetection/Program.cs?range=37-39)]

### <a name="upload-and-tag-images"></a>Carregar e marcar imagens

Ao marcar imagens em projetos de detecção de objeto, você precisa especificar a região de cada objeto marcado usando coordenadas normalizadas. O código a seguir associa cada uma das imagens de exemplo à região marcada.

[!code-csharp[](~/cognitive-services-dotnet-sdk-samples/CustomVision/ObjectDetection/Program.cs?range=41-84)]

Em seguida, esse mapa de associações é usado para carregar cada imagem de exemplo com suas coordenadas de região.

[!code-csharp[](~/cognitive-services-dotnet-sdk-samples/CustomVision/ObjectDetection/Program.cs?range=86-104)]

Aqui, todas as imagens de amostra foram carregadas, e cada uma tem uma marca (**fork** ou **scissors**) e um retângulo de pixels associado a essa marca.

### <a name="train-the-project"></a>Treinar o projeto

Esse código cria a primeira iteração de treinamento no projeto.

[!code-csharp[](~/cognitive-services-dotnet-sdk-samples/CustomVision/ObjectDetection/Program.cs?range=106-117)]

### <a name="set-the-current-iteration-as-default"></a>Definir a iteração atual como padrão

Esse código marca a iteração atual como a iteração padrão. A iteração padrão reflete a versão do modelo que responderá às solicitações de previsão. Você deve atualizar isso sempre que readaptar o modelo.

[!code-csharp[](~/cognitive-services-dotnet-sdk-samples/CustomVision/ObjectDetection/Program.cs?range=119-124)]

### <a name="create-a-prediction-endpoint"></a>Criar um ponto de extremidade de previsão

[!code-csharp[](~/cognitive-services-dotnet-sdk-samples/CustomVision/ObjectDetection/Program.cs?range=126-131)]

### <a name="use-the-prediction-endpoint"></a>Usar o ponto de extremidade de previsão

Essa parte do script carrega a imagem de teste, consulta o ponto de extremidade do modelo e gera dados de previsão para o console.

[!code-csharp[](~/cognitive-services-dotnet-sdk-samples/CustomVision/ObjectDetection/Program.cs?range=133-145)]

## <a name="run-the-application"></a>Executar o aplicativo

Enquanto o aplicativo é executado, ele deve abrir uma janela do console e gravar a seguinte saída:

```
Creating new project:
        Training
Done!

Making a prediction:
        fork: 98.2% [ 0.111609578, 0.184719115, 0.6607002, 0.6637112 ]
        scissors: 1.2% [ 0.112389535, 0.119195729, 0.658031344, 0.7023591 ]
```
Em seguida, você pode verificar se a imagem de teste (encontrada em **Images/Test/**) foi marcada corretamente e se a região da detecção está correta. Aqui você pode pressionar qualquer tecla para sair do aplicativo.

[!INCLUDE [clean-od-project](includes/clean-od-project.md)]

## <a name="next-steps"></a>Próximas etapas

Agora você viu como cada etapa do processo de detecção de objeto pode ser executada em código. Este exemplo executa uma iteração de treinamento única, mas muitas vezes você precisará treinar e testar o modelo várias vezes para torná-lo mais preciso. O guia a seguir lida com a classificação de imagens, mas seus princípios são semelhantes aos da detecção de objetos.

> [!div class="nextstepaction"]
> [Testar e readaptar um modelo](test-your-model.md)
