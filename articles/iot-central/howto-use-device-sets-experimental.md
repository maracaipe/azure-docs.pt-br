---
title: Usar conjuntos de dispositivos no aplicativo Azure IoT Central | Microsoft Docs
description: Como um operador, saiba como usar conjuntos de dispositivos no aplicativo Azure IoT Central.
author: ellenfosborne
ms.author: elfarber
ms.date: 02/05/2019
ms.topic: conceptual
ms.service: iot-central
services: iot-central
manager: peterpfr
ms.openlocfilehash: dd8fa36acaf3f4871d63200a4863778180e9be1a
ms.sourcegitcommit: 415742227ba5c3b089f7909aa16e0d8d5418f7fd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2019
ms.locfileid: "55771629"
---
# <a name="use-device-sets-in-your-azure-iot-central-application"></a>Usar conjuntos de dispositivos no aplicativo Azure IoT Central

Este artigo descreve como, como operador, usar conjuntos de dispositivos no seu Microsoft IoT Central.

Um conjunto de dispositivos é uma lista de dispositivos agrupados porque todos correspondem a alguns critérios especificados. Os conjuntos de dispositivos ajudam a gerenciar, visualizar e analisar dispositivos em grande escala, agrupando dispositivos em grupos lógicos menores. Por exemplo, você cria uma lista de todos os dispositivos de ar condicionado em Seattle para permitir que o técnico de Seattle encontre todos os dispositivos pelos quais o técnico é responsável. Este artigo mostra como criar e configurar conjuntos de dispositivos.

## <a name="create-a-device-set"></a>Criar um conjunto de dispositivos

Para criar um conjunto de dispositivos:

1. Escolha **Conjuntos de Dispositivos** no menu de navegação esquerdo.

1. Clique em **+ Novo**.

    ![Novo conjunto de dispositivos](media/howto-use-device-sets-experimental/image1.png)

1. Forneça ao dispositivo um nome que seja exclusivo em todo o aplicativo. Também é possível adicionar uma descrição. Um conjunto de dispositivos somente pode conter dispositivos de um único modelo de dispositivo. Escolha o modelo de dispositivo a ser usado para esse conjunto.

1. Crie a consulta para identificar os dispositivos para o conjunto de dispositivos, selecionando uma propriedade, um operador de comparação e um valor. É possível adicionar várias consultas e dispositivos que atendam a **todos** os critérios colocados no conjunto de dispositivos. O conjunto de dispositivos criado por você é acessível a qualquer pessoa que tenha acesso ao aplicativo, para que qualquer pessoa possa visualizar, modificar ou excluir o conjunto de dispositivos.

    ![Consulta do conjunto de dispositivos](media/howto-use-device-sets-experimental/image2.png)

    > [!NOTE]
    > O conjunto de dispositivos é uma consulta dinâmica. Cada vez que você visualizar a lista de dispositivos, poderá haver diferentes dispositivos na lista. A lista depende de quais dispositivos atualmente atendem aos critérios da consulta.

1. Escolha **Salvar**.

## <a name="configure-the-dashboard-for-your-device-set"></a>Configurar o Painel para o conjunto de dispositivos

Após criar o conjunto de dispositivos, você poderá configurar o **Painel**. O **Painel** é a home page onde é possível colocar imagens e links. Além disso, é possível adicionar grades que listam os dispositivos no conjunto de dispositivos.

1. Escolha **Conjuntos de Dispositivos** no menu de navegação esquerdo.

1. Escolher o conjunto do dispositivo.

1. Selecione a guia **Painel** .

1. Clique em **Editar**.

    ![Modo de design ativado](media/howto-use-device-sets-experimental/image3.png)

1. Para obter informações sobre como adicionar uma imagem, consulte [Preparar e carregar imagens no aplicativo Azure IoT Central](howto-prepare-images-experimental.md?toc=/azure/iot-central-experimental/toc.json&bc=/azure/iot-central-experimental/breadcrumb/toc.json).

1. Adicione um bloco de link:
    1. Escolha**Link** no painel direito.
    1. Forneça um **Título** ao link.
    1. Escolha um URL a ser aberta quando o link for clicado.
    1. Forneça ao link uma descrição que exiba abaixo do **Título**.
    1. Escolha **Salvar**.

        ![Link salvo](media/howto-use-device-sets-experimental/image7.png)

    1. É possível mover e redimensionar o bloco de link no **Painel**.

1. Adicione uma grade. Uma grade é uma tabela de dispositivos no conjunto de dispositivos com as colunas escolhidas.
    1. Escolha **Grade** no painel direito.
    1. Forneça um **Título** à grade.
    1. Selecione as colunas a serem mostrados, escolhendo **Adicionar/remover**. No painel que é exibido, escolha a coluna que você deseja mostrar e escolha a seta direita para selecioná-la.
    1. Escolha **OK**.
    1. Escolha **Salvar**.

        ![Salvar grade](media/howto-use-device-sets-experimental/image9.png)

    1. Arraste e solte a grade para colocá-la no **Painel**.

        > [!NOTE]
        > É possível adicionar várias imagens, links e grades.
  
    1. Clique em **Concluído**.

### <a name="configuring-location-map-in-your-device-sets-dashboard"></a>Configurando um Mapa de Localização em seu painel de conjuntos de dispositivos

É possível adicionar um mapa de local para visualizar a localização de seus conjuntos de dispositivos em um mapa.

Para adicionar um mapa de localização ao seu painel de conjuntos de dispositivos, você precisa ter configurado a propriedade de localização em seu modelo de Dispositivo, confira [Criar uma Propriedade de localização desenvolvida pelo Azure Mapas](howto-set-up-template-experimental.md?toc=/azure/iot-central-experimental/toc.json&bc=/azure/iot-central-experimental/breadcrumb/toc.json).

1. No painel de conjuntos de dispositivos, selecione Mapa na biblioteca.
2. Dê um título e escolha a propriedade de localização que você configurou anteriormente como parte da Propriedade de seu dispositivo.
3. Salve e você verá a peça de mapa exibindo a localização de seus dispositivos no Conjunto de Dispositivos.
4. Agora, quando um operador visualiza o painel de conjuntos de dispositivos, o operador pode ver todas as peças que você configurou, incluindo o Mapa de locais para visualizar rapidamente toda a localização dos dispositivos! 
    
> [!NOTE] 
> Será possível redimensionar o mapa para o tamanho desejado. Clicar em um alfinete no mapa exibirá as informações, o nome e o local do dispositivo. Você pode clicar no pop-up para ir para a página de propriedades do dispositivo.  

## <a name="configure-the-list-for-your-device-set"></a>Configurar a lista para o conjunto de dispositivos

Após criar o conjunto de dispositivos, será possível configurar uma **Lista**. A **Lista** mostra todos os dispositivos no conjunto de dispositivos em uma tabela com as colunas escolhidas.

1. Escolha **Conjuntos de Dispositivos** no menu de navegação esquerdo.

1. Escolha a guia **Lista**.

1. Escolha **Opções de Coluna**.

    ![Opções de Coluna](media/howto-use-device-sets-experimental/image11.png)

1. Escolha as colunas a serem mostradas, selecionando a coluna que você deseja mostrar e escolhendo a seta direita para selecioná-la.

    ![Escolher coluna](media/howto-use-device-sets-experimental/image12.png)

1. Escolha **OK**.

## <a name="analytics"></a>Análise

A análise em conjuntos de dispositivos é igual à guia de análise principal no menu de navegação esquerdo. É possível saber mais sobre análise, consultando o artigo sobre [como criar análises](howto-use-device-sets-experimental.md?toc=/azure/iot-central-experimental/toc.json&bc=/azure/iot-central-experimental/breadcrumb/toc.json).

## <a name="next-steps"></a>Próximas etapas

Agora que você aprendeu como usar conjuntos de dispositivos no aplicativo Azure IoT Central, a próxima etapa sugerida é apresentada:

> [!div class="nextstepaction"]
> [Como criar regras de telemetria](howto-create-telemetry-rules-experimental.md?toc=/azure/iot-central-experimental/toc.json&bc=/azure/iot-central-experimental/breadcrumb/toc.json)
