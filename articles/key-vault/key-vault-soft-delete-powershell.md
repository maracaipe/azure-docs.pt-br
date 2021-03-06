---
title: Azure Key Vault – Como usar a exclusão reversível com PowerShell
description: Usar exemplos de caso de exclusão reversível com trechos de código do PowerShell
author: bryanla
manager: mbaldwin
ms.service: key-vault
ms.topic: conceptual
ms.date: 02/01/2018
ms.author: bryanla
ms.openlocfilehash: c979d6eccd5c185d89252302b40fdd674e3c5916
ms.sourcegitcommit: de32e8825542b91f02da9e5d899d29bcc2c37f28
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55657494"
---
# <a name="how-to-use-key-vault-soft-delete-with-powershell"></a>Como usar a exclusão reversível do Key Vault com o PowerShell

O recurso de exclusão reversível do Azure Key Vault permite a recuperação de cofres e objetos de cofre excluídos. Especificamente, a exclusão reversível atende aos seguintes cenários:

- Suporte à exclusão reversível de cofres de chaves
- Suporte à exclusão reversível de objetos do cofre de chaves, chaves, segredos e certificados

## <a name="prerequisites"></a>Pré-requisitos

- Azure PowerShell 4.0.0 ou posterior – se você ainda não tiver configurado isso, instale o Azure PowerShell e associe-o à sua assinatura do Azure, veja [Como instalar e configurar o Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview). 

>[!NOTE]
> Há uma versão desatualizada de nosso arquivo de formatação de saída do PowerShell do Key Vault que **pode** ser carregada em seu ambiente, em vez da versão correta. Estamos antecipando uma versão atualizada do PowerShell para conter a correção necessária para a formatação de saída e atualizaremos este tópico nessa ocasião. A solução alternativa atual, caso você tenha esse problema de formatação, é:
> - Use a consulta a seguir se você perceber que não está vendo a propriedade habilitada para exclusão reversível descrita neste tópico: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.


Para saber mais sobre referências específicas do Key Vault para o PowerShell, veja [Referência do PowerShell do Azure Key Vault](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).

## <a name="required-permissions"></a>Permissões necessárias

As operações de Key Vault são gerenciadas separadamente por meio de permissões de RBAC (controle de acesso baseado em função) da seguinte maneira:

| Operação | DESCRIÇÃO | Permissão de usuário |
|:--|:--|:--|
|Listar|Lista os cofres de chaves excluídos.|Microsoft.KeyVault/deletedVaults/read|
|Recuperar|Recupera o cofre de chaves excluído.|Microsoft.KeyVault/vaults/write|
|Limpar|Remove permanentemente um cofre de chaves excluído e todo o seu conteúdo.|Microsoft.KeyVault/locations/deletedVaults/purge/action|

Para saber mais sobre permissões e controle de acesso, veja [Proteger seu cofre de chaves](key-vault-secure-your-key-vault.md).

## <a name="enabling-soft-delete"></a>Habilitar a exclusão reversível

Você habilita "exclusão suave" para permitir a recuperação de um cofre de chaves excluído ou objetos armazenados em um cofre de chaves.

> [!IMPORTANT]
> Habilitar 'exclusão reversível' em um cofre de chaves é uma ação irreversível. Depois que a propriedade de exclusão reversível tiver sido definida como "true", ele não pode ser alterado ou removido.  

### <a name="existing-key-vault"></a>Cofre de chaves existente

Para um cofre de chaves existente chamado ContosoVault, habilite a exclusão reversível da seguinte maneira. 

```powershell
($resource = Get-AzureRmResource -ResourceId (Get-AzureRmKeyVault -VaultName "ContosoVault").ResourceId).Properties | Add-Member -MemberType "NoteProperty" -Name "enableSoftDelete" -Value "true"

Set-AzureRmResource -resourceid $resource.ResourceId -Properties $resource.Properties
```

### <a name="new-key-vault"></a>Novo cofre de chaves

A habilitação da exclusão reversível para um novo cofre de chaves é feita no momento da criação adicionando o sinalizador de habilitação de exclusão reversível ao comando create.

```powershell
New-AzureRmKeyVault -Name "ContosoVault" -ResourceGroupName "ContosoRG" -Location "westus" -EnableSoftDelete
```

### <a name="verify-soft-delete-enablement"></a>Verificar a habilitação da exclusão reversível

Para verificar se um cofre de chaves tem exclusão reversível habilitada, execute o comando *show* e procure o atributo 'Exclusão Reversível Habilitada?' atributo:

```powershell
Get-AzureRmKeyVault -VaultName "ContosoVault"
```

## <a name="deleting-a-soft-delete-protected-key-vault"></a>Fazendo a exclusão reversível de um cofre de chaves protegido

O comando para excluir um cofre de chaves muda de comportamento, dependendo se a exclusão suave está ativada.

> [!IMPORTANT]
>Se você executar o seguinte comando para um cofre de chaves que não tenha a exclusão por software ativada, você excluirá permanentemente esse cofre de chaves e todo o seu conteúdo, sem opções de recuperação!

```powershell
Remove-AzureRmKeyVault -VaultName 'ContosoVault'
```

### <a name="how-soft-delete-protects-your-key-vaults"></a>Como a exclusão reversível protege seus cofres de chaves

Com a exclusão reversível habilitada:

- Um cofre de chaves excluído é removido de seu grupo de recursos e colocado em um namespace reservado, associado ao local em que foi criado. 
- Objetos excluídos, como chaves, segredos e certificados, ficam inacessíveis desde que o cofre da chave contida esteja no estado excluído. 
- O nome DNS de um cofre de chaves excluído é reservado, evitando que um novo cofre de chaves com o mesmo nome seja criado.  

Você pode exibir cofres de chave no estado excluído, associados à sua assinatura, usando o seguinte comando:

```powershell
PS C:\> Get-AzureRmKeyVault -InRemovedState 
```

- *ID* pode ser usado para identificar o recurso durante a recuperação ou limpeza. 
- *ID do recurso* é a ID do recurso original desse cofre. Como este cofre de chaves está em um estado excluído, não há um recurso com essa ID de recurso. 
- *Data de eliminação agendada* é quando o cofre será eliminado permanentemente, se nenhuma ação for realizada. O período de retenção padrão, usado para calcular a *Data de Limpeza Agendada*, é de 90 dias.

## <a name="recovering-a-key-vault"></a>Recuperação de um cofre de chaves

Para recuperar um cofre de chaves, especifique o nome do vault de chaves, o grupo de recursos e o local. Observe o local e o grupo de recursos do cofre de chaves excluído, conforme necessário para o processo de recuperação.

```powershell
Undo-AzureRmKeyVaultRemoval -VaultName ContosoVault -ResourceGroupName ContosoRG -Location westus
```

Quando um cofre de chaves é recuperado, um novo recurso é criado com o ID do recurso original do cofre da chave. Se o grupo de recursos original for removido, será necessário criar um com o mesmo nome antes de tentar a recuperação.

## <a name="deleting-and-purging-key-vault-objects"></a>Excluindo e limpando objetos de cofre de chaves

O comando a seguir excluirá a chave “ContosoFirstKey” em um cofre de chaves chamado “ContosoVault”, que tem exclusão reversível habilitada:

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey
```

Com o cofre de chaves habilitado para exclusão reversível, uma chave excluída ainda aparece como excluída, exceto se você listar explicitamente as chaves excluídas. A maioria das operações em uma chave no estado excluído falhará, exceto listagem, recuperação ou limpeza de uma chave excluída. 

Por exemplo, o comando a seguir lista as chaves excluídas no cofre de chaves “ContosoVault”:

```powershell
Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
```

### <a name="transition-state"></a>Estado de transição 

Quando você exclui uma chave em um cofre de chaves com exclusão reversível habilitada, talvez demore alguns segundos para a transição ser concluída. Durante essa transição, pode parecer que a chave não está no estado ativo ou no estado excluído. 

### <a name="using-soft-delete-with-key-vault-objects"></a>Usar exclusão reversível com objetos de cofre de chaves

Assim como os cofres das chaves, uma chave, segredo ou certificado excluído permanecem no estado excluído por até 90 dias, a menos que você os recupere ou purga. 

#### <a name="keys"></a>simétricas

Para recuperar uma chave excluída:

```powershell
Undo-AzureKeyVaultKeyRemoval -VaultName ContosoVault -Name ContosoFirstKey
```

Para excluir permanentemente (também conhecido como limpeza) uma chave excluída por software:

> [!IMPORTANT]
> Purgar uma chave irá excluí-la permanentemente e ela não será recuperável! 

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey -InRemovedState
```

As ações de **recuperação** e **limpeza** têm suas próprias permissões associadas em uma política de acesso de cofre de chaves. Para que um usuário ou diretor de serviço possa executar uma ação **recover** ou **purge**, eles devem ter a respectiva permissão para essa chave ou segredo. Por padrão, **purge** não é adicionada à política de acesso de um cofre de chaves, quando o atalho 'all' é usado para conceder todas as permissões. Você deve conceder especificamente **limpar** permissão. 

#### <a name="set-a-key-vault-access-policy"></a>Definir uma política de acesso de cofre de chaves

O comando a seguir concede a user@contoso.com permissão para usar várias operações em chaves em *ContosoVault*, incluindo **eliminação**:

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -UserPrincipalName user@contoso.com -PermissionsToKeys get,create,delete,list,update,import,backup,restore,recover,purge
```

>[!NOTE] 
> Se você tiver um cofre de chaves para o qual acabou de habilitar a exclusão reversível, talvez você não tenha as permissões de **recuperação** e **limpeza**.

#### <a name="secrets"></a>Segredos

Como as chaves, segredos sejam gerenciados com seus próprios comandos:

- Excluir um segredo chamado SQLPassword: 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -name SQLPassword
```

- Listar todos os segredos excluídos em um cofre de chaves: 
```powershell
Get-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState
```

- Recuperar um segredo no estado excluído: 
```powershell
Undo-AzureKeyVaultSecretRemoval -VaultName ContosoVault -Name SQLPAssword
```

- Limpar um segredo no estado excluído: 

  > [!IMPORTANT]
  > Purgar um segredo irá apagá-lo permanentemente e não será recuperável!

  ```powershell
  Remove-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState -name SQLPassword
  ```

## <a name="purging-a-soft-delete-protected-key-vault"></a>Limpando um cofre de chaves com exclusão reversível

> [!IMPORTANT]
> Limpar um cofre de chaves ou um de seus objetos contidos o excluirá permanentemente, ou seja, ele não poderá ser recuperado!

A função de limpeza é usada para excluir permanentemente um objeto do cofre de chaves que tenha sofrido uma exclusão reversível, ou todo ele. Conforme demonstrado na seção anterior, os objetos armazenados em um cofre de chaves com o recurso de exclusão reversível habilitado podem passar por vários estados:

- **Ativo**: antes da exclusão.
- **Exclusão reversível**: após a exclusão, ele pode ser listado e retornado ao estado ativo.
- **Excluído permanentemente**: após a limpeza, ele não pode ser recuperado.

O mesmo vale para o cofre de chaves. Para excluir permanentemente um cofre de chaves com exclusão reversível e seu conteúdo, você deve limpar o próprio cofre de chaves.

### <a name="purging-a-key-vault"></a>Limpando um cofre de chaves

Quando um cofre de chaves é removido, todo o seu conteúdo é excluído permanentemente, incluindo chaves, segredos e certificados. Para limpar um cofre de chaves com exclusão reversível, use o comando `Remove-AzureRmKeyVault` com a opção `-InRemovedState` e especifique o local do cofre da chave excluído com o argumento `-Location location`. Você pode encontrar o local de um cofre excluído usando o comando `Get-AzureRmKeyVault -InRemovedState`.

```powershell
Remove-AzureRmKeyVault -VaultName ContosoVault -InRemovedState -Location westus
```

### <a name="purge-permissions-required"></a>Permissões de limpeza necessárias
- Para limpar um cofre de chaves excluído, o usuário precisa da permissão RBAC para a operação *Microsoft.KeyVault / locations / deletedVaults / purge / action*. 
- Para listar um cofre de chaves excluído, o usuário precisa da permissão RBAC para a operação *Microsoft.KeyVault / deletedVaults / read*. 
- Por padrão, somente um administrador de assinatura tem essas permissões. 

### <a name="scheduled-purge"></a>Limpeza agendada

A listagem de objetos de cofre de chaves excluídos também mostra quando eles estão programados para serem removidos pelo Key Vault. *Data de eliminação agendada* indica quando um objeto do cofre da chave será excluído permanentemente, se nenhuma ação for executada. Por padrão, o período de retenção para um objeto do cofre de chaves excluído é de 90 dias.

>[!IMPORTANT]
>Um objeto de cofre limpo, disparado pelo campo *Data de Limpeza Agendada*, será excluído permanentemente. Não é recuperável!

## <a name="other-resources"></a>Outros recursos

- Para obter uma visão geral do recurso de exclusão reversível do Key Vault, veja [Visão geral da exclusão reversível do Azure Key Vault](key-vault-ovw-soft-delete.md).
- Para obter uma visão geral do uso do Azure Key Vault, veja [Introdução ao Azure Key Vault](key-vault-get-started.md).

