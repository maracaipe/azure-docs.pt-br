---
author: linda33wj
ms.service: data-factory
ms.topic: include
ms.date: 11/09/2018
ms.author: jingwang
ms.openlocfilehash: 831a72fff0931d116a669060b160f51fde6e1d3e
ms.sourcegitcommit: 6b7c8b44361e87d18dba8af2da306666c41b9396
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/12/2018
ms.locfileid: "51571781"
---
## <a name="verify-the-output"></a>Verificar a saída
O pipeline cria automaticamente a pasta de saída no contêiner de blob adftutorial. Em seguida, ele copia o arquivo emp.txt da pasta de entrada para a pasta de saída. 

1. No Portal do Azure, na página de contêiner **adftutorial**, clique em **Atualizar** para ver a pasta de saída. 
    
    ![Atualizar](media/data-factory-quickstart-verify-output-cleanup/output-refresh.png)
2. Clique em **saída** na lista de pastas. 
2. Confirme que **emp.txt** tenha sido copiado para a pasta de saída. 

    ![Atualizar](media/data-factory-quickstart-verify-output-cleanup/output-file.png)

## <a name="clean-up-resources"></a>Limpar recursos
Limpe os recursos criados no Guia de início rápido de duas maneiras. Você pode excluir o [grupo de recursos do Azure](../articles/azure-resource-manager/resource-group-overview.md), que inclui todos os recursos no grupo de recursos. Se desejar manter os outros recursos intactos, exclua apenas o data factory que você criou neste tutorial.

Ao excluir um grupo de recursos, todos os recursos são excluídos, incluindo os data factories nele. Execute o comando a seguir para excluir o grupo de recursos inteiro: 
```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

Observação: remover um grupo de recursos pode levar algum tempo. Seja paciente com o processo

Se deseja excluir apenas o data factory e não o grupo de recursos inteiro, execute o seguinte comando: 

```powershell
Remove-AzureRmDataFactoryV2 -Name $dataFactoryName -ResourceGroupName $resourceGroupName
```