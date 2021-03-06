---
author: dominicbetts
ms.service: iot-hub
ms.topic: include
ms.date: 10/26/2018
ms.author: dobett
ms.openlocfilehash: e6ba2a9c27567ccbd3b744a9bfdc0603758c7068
ms.sourcegitcommit: fec0e51a3af74b428d5cc23b6d0835ed0ac1e4d8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56212926"
---
## <a name="prepare-to-authenticate-azure-resource-manager-requests"></a>Preparar para autenticar solicitações do Azure Resource Manager
Autentique todas as operações que podem ser executadas nos recursos usando o [Azure Resource Manager][lnk-authenticate-arm] com o Azure Active Directory (AD). A maneira mais fácil de configurar isso é usar o PowerShell ou Azure CLI.

Instale os [cmdlets do Azure PowerShell][lnk-powershell-install] antes de continuar.

As etapas a seguir mostram como configurar a autenticação de senha para um aplicativo do AD usando o PowerShell. Você pode executar esses comandos em uma sessão do PowerShell padrão.

1. Conecte em sua assinatura do Azure usando o seguinte comando:

    ```powershell
    Connect-AzureRmAccount
    ```

1. Caso tenha várias assinaturas do Azure, entrar no Azure concede a você acesso a todas as assinaturas do Azure associadas às suas credenciais. Use o comando a seguir para listar as assinaturas do Azure disponíveis para você:

    ```powershell
    Get-AzureRMSubscription
    ```

    Use o comando a seguir para selecionar a assinatura que você deseja usar para executar os comandos e criar seu Hub IoT. Você pode usar a ID ou nome da assinatura da saída do comando anterior:

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

2. Anote seu **TenantId** e **SubscriptionId**. Você precisará dessa informação mais tarde.
3. Crie um novo aplicativo do Active Directory do Azure usando o seguinte comando, substituindo os espaços reservados:
   
   * **{Display name}:** um nome de exibição para seu aplicativo, como **MySampleApp**
   * **{Home page URL}:** a URL da home page do seu aplicativo, como **http://mysampleapp/home**. Essa URL não precisa levar para um aplicativo real.
   * **{Application identifier}:** um identificador exclusivo, como **http://mysampleapp**. Essa URL não precisa levar para um aplicativo real.
   * **{Password}:** uma senha que você usa para autenticar com o seu aplicativo.
     
     ```powershell
     $SecurePassword=ConvertTo-SecureString {password} –asplaintext –force
     New-AzureRmADApplication -DisplayName {Display name} -HomePage {Home page URL} -IdentifierUris {Application identifier} -Password $SecurePassword
     ```
4. Anote o **ApplicationId** do aplicativo que você criou. Você precisa dessa informação mais tarde.
5. Criar uma nova entidade de serviço usando o comando a seguir, substituindo **{MyApplicationId}** pelo **ApplicationId** da etapa anterior:
   
    ```powershell
    New-AzureRmADServicePrincipal -ApplicationId {MyApplicationId}
    ```
6. Configure uma atribuição de função usando o comando a seguir, substituindo **{MyApplicationId}** por **ApplicationId**.
   
    ```powershell
    New-AzureRmRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName {MyApplicationId}
    ```

Você terminou de criar o aplicativo do Azure AD que permitirá autenticar a partir do seu aplicativo C# personalizado. Você precisa dos seguintes valores mais à frente neste tutorial:

* TenantId
* SubscriptionId
* ApplicationId
* Senha

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/azurerm/install-azurerm-ps
