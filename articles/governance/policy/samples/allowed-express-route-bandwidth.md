---
title: Exemplo – Largura de banda permitida do ExpressRoute
description: Essa política de exemplo exige que o ExpressRoute use um conjunto especificado de larguras de banda.
services: azure-policy
author: DCtheGeek
manager: carmonm
ms.service: azure-policy
ms.topic: sample
ms.date: 01/23/2019
ms.author: dacoulte
ms.openlocfilehash: fc98e9085844749153ee6f45466cc367eef2ffff
ms.sourcegitcommit: b3d74ce0a4acea922eadd96abfb7710ae79356e0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56244736"
---
# <a name="allowed-expressroute-bandwidth"></a>Largura de banda do ExpressRoute permitida

Essa política requer que o ExpressRoute use um conjunto de larguras de bandas especificado. Você especifica uma matriz de SKUs que pode ser definida para o Express Route.

[!INCLUDE [quickstarts-free-trial-note](../../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a>Modelo de exemplo

[!code-json[main](../../../../policy-templates/samples/Network/express-route-bandwidthInMbps/azurepolicy.json "Allowed ExpressRoute bandwidth")]

Você pode implantar este modelo usando o [portal do Azure](#deploy-with-the-portal), com [PowerShell](#deploy-with-powershell) ou com o [CLI do Azure](#deploy-with-azure-cli).

## <a name="deploy-with-the-portal"></a>Implantar com o portal

[![Implantar no Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FNetwork%2Fexpress-route-bandwidthInMbps%2Fazurepolicy.json)

## <a name="deploy-with-powershell"></a>Implantação com o PowerShell

[!INCLUDE [sample-powershell-install](../../../../includes/sample-powershell-install-no-ssh-az.md)]

```azurepowershell-interactive
$definition = New-AzPolicyDefinition -Name "express-route-bandwidthInMbps" -DisplayName "Allowed ExpressRoute bandwidth" -description "This policy enables you to specify a set of express-route bandwidths that your organization can deploy." -Policy 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/express-route-bandwidthInMbps/azurepolicy.rules.json' -Parameter 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/express-route-bandwidthInMbps/azurepolicy.parameters.json' -Mode All
$definition
$assignment = New-AzPolicyAssignment -Name <assignmentname> -Scope <scope>  -listOfBandwidthinMbps <Allowed Bandwidth> -PolicyDefinition $definition
$assignment
```

### <a name="clean-up-powershell-deployment"></a>Limpar a implantação do PowerShell

Execute o comando a seguir para remover o grupo de recursos, a VM e todos os recursos relacionados.

```azurepowershell-interactive
Remove-AzResourceGroup -Name myResourceGroup
```

## <a name="deploy-with-azure-cli"></a>Implantar com a CLI do Azure

[!INCLUDE [sample-cli-install](../../../../includes/sample-cli-install.md)]

```azurecli-interactive
az policy definition create --name 'express-route-bandwidthInMbps' --display-name 'Allowed ExpressRoute bandwidth' --description 'This policy enables you to specify a set of ExpressRoute bandwidths that your organization can deploy.' --rules 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/express-route-bandwidthInMbps/azurepolicy.rules.json' --params 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/express-route-bandwidthInMbps/azurepolicy.parameters.json' --mode All

az policy assignment create --name <assignmentname> --scope <scope> --policy "express-route-bandwidthInMbps"
```

### <a name="clean-up-azure-cli-deployment"></a>Limpar a implantação da CLI do Azure

Execute o comando a seguir para remover o grupo de recursos, a VM e todos os recursos relacionados.

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

## <a name="next-steps"></a>Próximas etapas

- Examine mais exemplos nos [exemplos do Azure Policy](index.md)