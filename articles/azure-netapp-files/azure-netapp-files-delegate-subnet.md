---
title: Delegar uma sub-rede para Azure NetApp Files | Microsoft Docs
description: Descreve como delegar uma sub-rede para o Azure NetApp Files.
services: azure-netapp-files
documentationcenter: ''
author: b-juche
manager: ''
editor: ''
ms.assetid: ''
ms.service: azure-netapp-files
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 11/13/2018
ms.author: b-juche
ms.openlocfilehash: 8ec41c6db8c8e5c62d15dc0638762f2649c637b8
ms.sourcegitcommit: c94cf3840db42f099b4dc858cd0c77c4e3e4c436
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2018
ms.locfileid: "53631644"
---
# <a name="delegate-a-subnet-to-azure-netapp-files"></a>Delegar uma sub-rede ao Azure NetApp Files 

É necessário delegar uma sub-rede para Azure NetApp Files.   Quando você cria um volume, é necessário especificar a sub-rede delegada.

## <a name="about-this-task"></a>Sobre esta tarefa
* O assistente para criar uma nova sub-rede usa como padrão uma máscara de rede /24, que possibilita 251 endereços IP disponíveis. Usar uma máscara de rede /28, que possibilita 16 endereços IP utilizáveis, é suficiente para o serviço.
* Não é possível designar um grupo de segurança de rede nem um ponto de extremidade de serviço na sub-rede delegada. Fazer isso causa a falha da delegação da sub-rede.
* Em cada Vnet (Rede virtual) do Azure, apenas uma sub-rede pode ser delegada para o Azure NetApp Files.
* No momento, não há suporte para o acesso a um volume de uma rede virtual emparelhada.

## <a name="steps"></a>Etapas 
1.  Acesse a folha **Redes virtuais** no portal do Azure e selecione a rede virtual que você deseja usar para o Azure NetApp Files.    

1. Selecione **Sub-redes** na folha da Rede virtual e clique no botão **+ Sub-rede**. 

1. Crie uma nova sub-rede a ser usada para o Azure NetApp Files preenchendo os campos obrigatórios a seguir na página Adicionar sub-rede:
    * **Nome**: especifique o nome da sub-rede.
    * **Intervalo de endereços**: especifique o intervalo de endereços IP.
    * **Delegação de sub-rede**: Selecione **Microsoft.NetApp/volumes**. 

      ![Delegação de sub-rede](../media/azure-netapp-files/azure-netapp-files-subnet-delegation.png)
    
Também é possível criar e delegar uma sub-rede quando você [cria um volume do Azure NetApp Files](azure-netapp-files-create-volumes.md). 

## <a name="next-steps"></a>Próximas etapas  
* [Criar um volume do Azure NetApp Files](azure-netapp-files-create-volumes.md)
* [Saiba mais sobre a integração de rede virtual para os serviços do Azure](https://docs.microsoft.com/azure/virtual-network/virtual-network-for-azure-services)


