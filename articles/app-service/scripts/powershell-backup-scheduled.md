---
title: Exemplo de Script do Azure PowerShell – Criar um backup agendada para um aplicativo Web | Microsoft Docs
description: Script do Azure PowerShell de exemplo - Criar um backup agendado para um aplicativo Web
services: app-service\web
documentationcenter: ''
author: msangapu
manager: jeconnoc
editor: ''
tags: azure-service-management
ms.assetid: a2a27d94-d378-4c17-a6a9-ae1e69dc4a72
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 10/30/2017
ms.author: msangapu
ms.custom: seodec18
ms.openlocfilehash: d1b1605b3ef98f9b918e166c540231c6462bcf88
ms.sourcegitcommit: 7cd706612a2712e4dd11e8ca8d172e81d561e1db
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/18/2018
ms.locfileid: "53585907"
---
# <a name="create-a-scheduled-backup-for-a-web-app-using-powershell"></a>Criar um backup agendado para um aplicativo Web usando o PowerShell

Este script de exemplo cria um aplicativo Web no Serviço de Aplicativo com seus recursos relacionados e então cria um backup agendado para ele. 

Se necessário, instale o Azure PowerShell usando a instrução encontrada no [guia do Azure PowerShell](/powershell/azure/overview) e, em seguida, execute `Connect-AzureRmAccount` para criar uma conexão com o Azure. 

## <a name="sample-script"></a>Script de exemplo

[!code-azurepowershell-interactive[main](../../../powershell_scripts/app-service/backup-scheduled/backup-scheduled.ps1?highlight=1-4 "Create a scheduled backup for a web app")]

## <a name="clean-up-deployment"></a>Limpar a implantação 

Após a execução da amostra de script, o comando a seguir pode ser usado para remover o grupo de recursos, o aplicativo Web e todos os recursos relacionados.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a>Explicação sobre o script

Este script usa os seguintes comandos. Cada comando da tabela é vinculado à documentação específica do comando.

| Comando | Observações |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Cria um grupo de recursos no qual todos os recursos são armazenados. |
| [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) | Cria uma conta de armazenamento. |
| [New-AzureStorageContainer](/powershell/module/azure.storage/new-azurestoragecontainer) | Cria um contêiner de armazenamento do Azure. |
| [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) | Gera um token SAS para um contêiner de armazenamento do Azure. |
| [New-AzureRmAppServicePlan](/powershell/module/azurerm.websites/new-azurermappserviceplan) | Cria um Plano do Serviço de Aplicativo. |
| [New-AzureRmWebApp](/powershell/module/azurerm.websites/new-azurermwebapp) | Cria um aplicativo web. |
| [Edit-AzureRmWebAppBackupConfiguration](/powershell/module/azurerm.websites/edit-azurermwebappbackupconfiguration) | Edita a configuração de backup para o aplicativo Web. |
| [Get-AzureRmWebAppBackupList](/powershell/module/azurerm.websites/get-azurermwebappbackuplist) | Obtém uma lista de backups para um aplicativo Web. |
| [Get-AzureRmWebAppBackupConfiguration](/powershell/module/azurerm.websites/get-azurermwebappbackupconfiguration) | Obtém a configuração de backup para o aplicativo Web. |

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o módulo do Azure PowerShell, confira a [Documentação do Azure PowerShell](/powershell/azure/overview).

Exemplos adicionais do Azure PowerShell para Aplicativos Web do Serviço de Aplicativo do Azure podem ser encontrados nos [exemplos do Azure PowerShell](../samples-powershell.md).
