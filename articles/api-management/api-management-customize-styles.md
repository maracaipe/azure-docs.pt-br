---
title: Personalizar o estilo de página no portal do desenvolvedor do Gerenciamento de API do Azure | Microsoft Docs
description: Siga as etapas neste guia de início rápido para personalizar o estilo dos elementos no portal do desenvolvedor do Gerenciamento de API do Azure.
services: api-management
documentationcenter: ''
author: vladvino
manager: cfowler
editor: ''
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.custom: mvc
ms.topic: tutorial
ms.date: 06/15/2018
ms.author: apimpm
ms.openlocfilehash: c3c79e7bd68e7c96b57ea66951c080b7d952ee8c
ms.sourcegitcommit: 5aed7f6c948abcce87884d62f3ba098245245196
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52441750"
---
# <a name="customize-the-style-of-the-developer-portal-pages"></a>Personalizar o estilo das páginas do Portal do Desenvolvedor

Há três maneiras mais comuns de personalizar o Portal do Desenvolvedor no Gerenciamento de API do Azure:
 
* [Editar o conteúdo de páginas estáticas e elementos de layout da página](api-management-modify-content-layout.md)
* Atualizar os estilos usados para elementos de página entre o portal do desenvolvedor (explicado neste guia)
* [Modificar os modelos usados para as páginas geradas pelo portal](api-management-developer-portal-templates.md) (por exemplo, documentos de API, produtos, autenticação do usuário)

Neste tutorial, você aprenderá como:

> [!div class="checklist"]
> * Personalizar o estilo de elementos nas páginas do portal do **Desenvolvedor**
> * Exibir as alterações

![personalizar estilo](./media/modify-developer-portal-style/developer_portal.png)

## <a name="prerequisites"></a>Pré-requisitos

+ Conheça a [terminologia do Gerenciamento de API do Azure](api-management-terminology.md).
+ Conclua o seguinte guia de início rápido: [Criar uma instância do Gerenciamento de API do Azure](get-started-create-service-instance.md).
+ Além disso, conclua o seguinte tutorial: [Importar e publicar sua primeira API](import-and-publish.md).

[!INCLUDE [premium-dev-standard-basic.md](../../includes/api-management-availability-premium-dev-standard-basic.md)]

## <a name="customize-the-developer-portal"></a>Personalizar o Portal do Desenvolvedor

1. Selecione **Visão geral**.
2. Clique no botão **Portal do Desenvolvedor** na parte superior da janela **Visão geral**. Como alternativa, você pode clicar no link **URL do portal do Desenvolvedor**.
3. No canto superior esquerdo da tela, você verá um ícone composto de dois pincéis. Passe o mouse sobre esse ícone para abrir o menu de personalização do portal.

    ![personalizar estilo](./media/modify-developer-portal-style/modify-developer-portal-style01.png)
4. Selecione **Estilos** no menu para abrir o painel de personalização de estilos.

    Todos os elementos que você pode personalizar usando **Estilos** aparecem na página
5. Insira "headings-color" no campo **Alterar valores de variáveis para personalizar a aparência do portal do desenvolvedor:**.

    O elemento **@headings-color** aparece na página. Essa variável controla a cor do texto.

    ![personalizar estilo](./media/modify-developer-portal-style/modify-developer-portal-style02.png)
    
6. Clique no campo da variável **@headings-color**. 
    
    A lista suspensa do seletor de cores é aberta.
7. Selecione uma nova cor na lista suspensa do seletor de cores.

    > [!TIP]
    > A visualização em tempo real está disponível para todas as alterações. Um indicador de progresso aparece na parte superior do painel de personalização. Depois de alguns segundos, o texto do cabeçalho muda para a cor selecionada.

8. Selecione **Publicar** no canto inferior esquerdo do menu do painel de personalização.
9. Selecione **Publicar personalizações** para disponibilizar as alterações publicamente.

## <a name="view-your-change"></a>Exibir as alterações

1. Navegue até o Portal do Desenvolvedor.
2. Você pode ver a alteração feita.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu como:

> [!div class="checklist"]
> * Personalizar o estilo de elementos nas páginas do portal do **Desenvolvedor**
> * Exibir as alterações

Talvez você também esteja interessado em saber [como personalizar o portal de desenvolvedor de Gerenciamento de API do Azure usando modelos](api-management-developer-portal-templates.md).