---
title: Execução de runbook na Automação do Azure
description: Descreve os detalhes de como um runbook na Automação do Azure é processado.
services: automation
ms.service: automation
ms.subservice: process-automation
author: georgewallace
ms.author: gwallace
ms.date: 01/10/2019
ms.topic: conceptual
manager: carmonm
ms.openlocfilehash: 4e5c64dc43be10eead1da35ec2337aa1f83f2f91
ms.sourcegitcommit: cf88cf2cbe94293b0542714a98833be001471c08
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54472119"
---
# <a name="runbook-execution-in-azure-automation"></a>Execução de runbook na Automação do Azure

Quando você inicia um runbook na Automação do Azure, um trabalho é criado. Um trabalho é uma instância única de execução de um runbook. Um trabalhador da Automação do Azure é atribuído para executar cada tarefa. Enquanto os trabalhadores são compartilhados por muitas contas do Azure, os trabalhos de diferentes contas de automação ficam isolados uns dos outros. Você não tem controle sobre qual trabalhador atende a solicitação do seu trabalho. Um único runbook pode ter muitos trabalhos em execução ao mesmo tempo. O ambiente de execução para trabalhos da mesma conta de Automação do Azure pode ser reutilizado. Quanto mais trabalhos você executar ao mesmo tempo, mais frequentemente eles poderão ser enviados à mesma área restrita. Trabalhos em execução no mesmo processo de área restrita podem afetar uns aos outros, sendo um exemplo a execução do cmdlet `Disconnect-AzureRMAccount`. Executar este cmdlet desconectaria cada trabalho de runbook no processo de área restrita compartilhado. Quando você exibe a lista de runbooks no Portal do Azure, ela lista o status de todos os trabalhos iniciados para cada runbook. Você pode exibir a lista de trabalhos para cada runbook para acompanhar o status de cada um. Os logs de trabalho são armazenados por 30 dias, no máximo. Para obter uma descrição das diferentes opções de status de trabalho, confira [Status de trabalho](#job-statuses).

[!INCLUDE [GDPR-related guidance](../../includes/gdpr-dsr-and-stp-note.md)]

O diagrama a seguir mostra o ciclo de vida de um trabalho de runbook para [runbooks gráficos](automation-runbook-types.md#graphical-runbooks) e [runbooks de fluxo de trabalho do PowerShell](automation-runbook-types.md#powershell-workflow-runbooks).

![Status de trabalho - Fluxo de trabalho do PowerShell](./media/automation-runbook-execution/job-statuses.png)

O diagrama a seguir mostra o ciclo de vida de um trabalho de runbook para [runbooks do PowerShell](automation-runbook-types.md#powershell-runbooks).

![Status de trabalho - Script do PowerShell](./media/automation-runbook-execution/job-statuses-script.png)

Os trabalhos têm acesso aos recursos do Azure fazendo uma conexão à sua assinatura do Azure. Eles só têm acesso aos recursos no seu data center se estes puderem ser acessados da nuvem pública.

## <a name="where-to-run-your-runbooks"></a>Onde executar seus runbooks

Os runbooks na Automação do Azure podem ser executados em uma área restrita no Azure ou em um [Hybrid Runbook Worker](automation-hybrid-runbook-worker.md). Uma área restrita é um ambiente compartilhado no Azure que pode ser usado por vários trabalhos. Os trabalhos que usam a mesma área restrita são restringidos pelas limitações de recurso da área restrita. Os Hybrid Runbook Workers podem ser usados para executar runbooks diretamente no computador que está hospedando a função e em relação aos recursos do ambiente para gerenciamento desses recursos locais. Runbooks são armazenados e gerenciados na Automação do Azure e, em seguida, entregues a um ou mais computadores atribuídos. A maioria dos runbooks pode ser executada facilmente em áreas restritas do Azure. Há cenários específicos em que pode ser recomendada a escolha de um Hybrid Runbook ao invés de uma área restrita do Azure para execução do seu runbook. Veja a seguinte tabela com uma lista de alguns exemplos de cenário:

|Tarefa|Melhor opção|Observações|
|---|---|---|
|Integração com serviços do Azure|Área restrita do Azure|Com hospedagem no Azure, a autenticação é mais simples. Se você está usando o Hybrid Runbook Worker em uma VM do Azure, é possível usar [identidades gerenciadas para recursos do Azure](automation-hrw-run-runbooks.md#managed-identities-for-azure-resources)|
|Desempenho ideal para gerenciar recursos do Azure|Área restrita do Azure|O script é executado no mesmo ambiente que, por sua vez, tem menos latência|
|Redução de custos operacionais|Área restrita do Azure|Não há sobrecarga de computação, nem a necessidade de uma VM|
|Script de execução prolongada|Hybrid Runbook Worker|Áreas restritas do Azure têm [limitação de recursos](../azure-subscription-service-limits.md#automation-limits)|
|Interação com serviços locais|Hybrid Runbook Worker|Pode ter acesso diretamente ao computador host|
|Exigência de software de terceiros e executáveis|Hybrid Runbook Worker|Você gerencia o SO e pode instalar software|
|Monitoramento de um arquivo ou uma pasta com um runbook|Hybrid Runbook Worker|Use uma [tarefa do Inspetor](automation-watchers-tutorial.md) em um Hybrid Runbook Worker|
|O script usa muitos recursos|Hybrid Runbook Worker| Áreas restritas do Azure têm [limitação de recursos](../azure-subscription-service-limits.md#automation-limits)|
|Uso de módulos com requisitos específicos| Hybrid Runbook Worker|Alguns exemplos incluem:</br> **WinSCP**: dependência de winscp.exe </br> **IISAdministration**: necessidade de que o IIS seja desabilitado|
|Instalação do módulo que requer o instalador|Hybrid Runbook Worker|Módulos para a área restrita devem ser xcopyable|
|Uso de runbooks ou módulos que exigem o .NET Framework diferente da versão 4.7.2|Hybrid Runbook Worker|Áreas restritas da Automação têm o .NET Framework 4.7.2 e não há maneira de atualizá-lo|

## <a name="runbook-behavior"></a>Comportamento do runbook

Os runbooks são executados com base na lógica que é definida dentro deles. Se um runbook é interrompido, ele é reiniciado no início. Esse comportamento exige que os runbooks sejam escritos de maneira a permitir a reinicialização em caso de problemas transitórios.

### <a name="creating-resources"></a>Criar recursos

Se o seu script cria recursos, você deve verificar se o recurso já existe antes de tentar criá-lo novamente. Um exemplo básico é mostrado no seguinte exemplo:

```powershell
$vmName = "WindowsVM1"
$resourceGroupName = "myResourceGroup"
$myCred = Get-AutomationPSCredential "MyCredential"
$vmExists = Get-AzureRmResource -Name $vmName -ResourceGroupName $resourceGroupName

if(!$vmExists)
    {
    Write-Output "VM $vmName does not exists, creating"
    New-AzureRmVM -Name $vmName -ResourceGroupName $resourceGroupName -Credential $myCred
    }
else
    {
    Write-Output "VM $vmName already exists, skipping"
    }
```

### <a name="time-dependant-scripts"></a>Scripts dependentes de tempo

É preciso ponderar cuidadosamente ao criar runbooks. Como mencionado anteriormente, os runbooks precisam ser criados de maneira que sejam robustos e possam tratar de erros transitórios que podem fazer com que o runbook reinicie ou falhe. Se um runbook falhar, ele é repetido. Se um runbook é executado normalmente dentro de um limite de tempo, a lógica para verificar o tempo de execução deve ser implementada no runbook de modo a garantir que operações como a inicialização, o desligamento ou a expansão sejam executadas somente durante horários específicos.

### <a name="tracking-progress"></a>Acompanhar o progresso

Uma boa prática é criar runbooks para que sejam modulares por natureza. Isso significa estruturar a lógica no runbook de modo que ele possa ser reutilizado e reiniciado facilmente. Acompanhar o progresso em um runbook é uma maneira de garantir que a lógica em um runbook seja executada corretamente em caso de problemas. Algumas maneiras possíveis de acompanhar o progresso do runbook é usar uma fonte externa, como contas de armazenamento, um banco de dados ou arquivos compartilhados. Ao acompanhar o estado externamente, você pode criar a lógica em seu runbook para verificar primeiro o estado da última ação que o runbook recebeu e, com base nos resultados, ignorar ou continuar tarefas específicas no runbook.

### <a name="prevent-concurrent-jobs"></a>Evitar trabalhos simultâneos

Alguns runbooks podem se comportar de forma estranha se estiverem sendo executados em vários trabalhos ao mesmo tempo. Nesse caso, é importante implementar a lógica para verificar se um runbook já tem um trabalho em execução. Um exemplo básico de como você pode reproduzir esse comportamento é mostrado no seguinte exemplo:

```powershell
# Authenticate to Azure
$connection = Get-AutomationConnection -Name AzureRunAsConnection
Connect-AzureRmAccount -ServicePrincipal -Tenant $connection.TenantID `
-ApplicationID $connection.ApplicationID -CertificateThumbprint $connection.CertificateThumbprint

$AzureContext = Select-AzureRmSubscription -SubscriptionId $connection.SubscriptionID

# Check for already running or new runbooks
$runbookName = "<RunbookName>"
$rgName = "<ResourceGroupName>"
$aaName = "<AutomationAccountName>"
$jobs = Get-AzureRmAutomationJob -ResourceGroupName $rgName -AutomationAccountName $aaName -RunbookName $runbookName -AzureRmContext $AzureContext

# If then check to see if it is already running
$runningCount = ($jobs | ? {$_.Status -eq "Running"}).count

If (($jobs.status -contains "Running" -And $runningCount -gt 1 ) -Or ($jobs.Status -eq "New")) {
    # Exit code
    Write-Output "Runbook is already running"
    Exit 1
} else {
    # Insert Your code here
}
```

### <a name="using-executables-or-calling-processes"></a>Usar executáveis ou chamar processos

Os runbooks executados nas áreas restritas do Azure não oferecem suporte à chamada de processos (como .exe ou subprocess.call). Isso porque as áreas restritas do Azure são processos compartilhados executados em contêineres, que podem não ter acesso a todas as APIs subjacentes. Para cenários em que são necessários softwares de terceiros ou a chamada de subprocessos, é recomendável executar o runbook em um [Hybrid Runbook Worker](automation-hybrid-runbook-worker.md).

## <a name="job-statuses"></a>Status de trabalho

A tabela a seguir descreve os diferentes status possíveis para um trabalho. O PowerShell tem dois tipos de erros, erros de finalização e sem finalização. Erros de finalização definem o status do runbook como **Falhou**, caso ocorram. Erros sem finalização permitem que o script continue mesmo depois de ocorrerem. Um exemplo de um erro sem finalização é usar o cmdlet `Get-ChildItem` com um caminho que não existe. O PowerShell vê que o caminho não existe, gera um erro e continua até a próxima pasta. Esse erro não definiria o status do runbook como **Falhou** e poderia ser marcado como **Concluído**. Para forçar um runbook a parar se houver um erro sem finalização, você pode usar `-ErrorAction Stop` no cmdlet.

| Status | DESCRIÇÃO |
|:--- |:--- |
| Concluído |Operação concluída com sucesso. |
| Com falha |Para [runbooks gráficos e de fluxo de trabalho do PowerShell](automation-runbook-types.md), o runbook falhou ao compilar. Para [runbooks de Script do PowerShell](automation-runbook-types.md), o runbook falhou ao iniciar ou o trabalho sofreu uma exceção. |
| Erro, aguardando recursos |O trabalho falhou porque atingiu o limite de [fração justa](#fair-share) três vezes e iniciou do mesmo ponto de verificação ou desde o início do runbook em cada uma das vezes. |
| Em fila |O trabalho está aguardando recursos de um trabalho do Automation ficar disponível para que ele possa ser iniciado. |
| Iniciando |O trabalho foi atribuído a um trabalhador e o sistema está iniciando-o. |
| Continuando |O sistema está retomando o trabalho depois que ele ter sido suspenso. |
| Executando |O trabalho está em execução. |
| Executando, aguardando recursos |O trabalho foi descarregado, pois atingiu o limite de [fração justa](#fair-share) . Ele será retomado em breve do seu último ponto de verificação. |
| Parado |O trabalho foi interrompido pelo usuário antes de ser concluído. |
| Parando |O sistema está parando o trabalho. |
| Suspenso |O trabalho foi suspenso pelo usuário, pelo sistema ou por um comando no runbook. Se um runbook não tiver um ponto de verificação, ele começará desde o início do runbook. Se ele tiver um ponto de verificação, poderá iniciar novamente e retomar no último ponto de verificação. O runbook só é suspenso pelo sistema quando ocorre uma exceção. Por padrão, ErrorActionPreference é definido como **Continuar** o que significa que o trabalho continua a ser executado no caso de um erro. Se essa variável de preferência for definida como **Parar**, o trabalho será suspenso no caso de um erro. Aplica-se a somente [runbooks gráficos e de fluxo de trabalho do PowerShell](automation-runbook-types.md). |
| Suspensão |O sistema está tentando suspender o trabalho por solicitação do usuário. O runbook precisa atingir seu próximo ponto de verificação antes de poder ser suspenso. Se já passou de seu último ponto de verificação, ele será concluído antes de ser suspenso. Aplica-se a somente [runbooks gráficos e de fluxo de trabalho do PowerShell](automation-runbook-types.md). |

## <a name="viewing-job-status-from-the-azure-portal"></a>Exibindo o status do trabalho no portal do Azure

Você pode exibir um status resumido de todos os trabalhos do runbook ou analisar os detalhes de um trabalho específico do runbook no portal do Azure. Você também pode configurar a integração com o seu espaço de trabalho do Log Analytics a fim de encaminhar fluxos de trabalho e status do trabalho do runbook. Para saber mais sobre a integração com o Log Analytics, consulte [Encaminhar status do trabalho e fluxos de trabalho de Automação para Log Analytics](automation-manage-send-joblogs-log-analytics.md).

### <a name="automation-runbook-jobs-summary"></a>Resumo dos trabalhos de runbook da Automação

À direita da conta de Automação selecionada, é possível ver um resumo de todos os trabalhos de runbook no bloco **Estatísticas de Trabalho**.

![Bloco Estatísticas de Trabalho](./media/automation-runbook-execution/automation-account-job-status-summary.png)

Esse bloco exibe a contagem e a representação gráfica do status do trabalho para todos os trabalhos executados.

Clicar no bloco apresenta a página **Trabalhos**, que contém uma lista resumida de todos os trabalhos executados. Esta página mostra o status, os horários de início e os horários de término.

![Página Trabalhos da conta de automação](./media/automation-runbook-execution/automation-account-jobs-status-blade.png)

Você pode filtrar a lista de trabalhos selecionando **Filtrar trabalhos** e filtrar em um runbook específico, status de trabalho ou lista suspensa pelo intervalo de hora dentro do qual pesquisar.

![Filtrar por status do Trabalho](./media/automation-runbook-execution/automation-account-jobs-filter.png)

Como alternativa, você pode exibir detalhes de resumo do trabalho para um runbook específico selecionando esse runbook na página **Runbooks** da sua conta de Automação e selecionando o bloco **Trabalhos**. Essa ação apresenta a página **Trabalhos** e, nela, é possível clicar no registro do trabalho para exibir seus detalhes e seu resultado.

![Página Trabalhos da conta de automação](./media/automation-runbook-execution/automation-runbook-job-summary-blade.png)

### <a name="job-summary"></a>Resumo do trabalho

Você pode exibir uma lista de todos os trabalhos que foram criados para um determinado runbook e o status mais recente deles. Você pode filtrar essa lista pelo status do trabalho e o intervalo de datas para a última alteração no trabalho. Para exibir as informações detalhadas e o resultado, clique no nome de um trabalho. A exibição detalhada do trabalho inclui os valores para os parâmetros de runbook que foram fornecidos para esse trabalho.

Você pode usar as etapas a seguir para exibir os trabalhos de um runbook.

1. No Portal do Azure, selecione **Automação** e, em seguida, selecione no nome de uma Conta de automação.
2. No hub, selecione **Runbooks** e, em seguida, na página **Runbooks**, selecione um runbook da lista.
3. Na página do runbook selecionado, clique no bloco **Trabalhos**.
4. Clique em um dos trabalhos na lista e, na página de detalhes do trabalho do runbook, você pode exibir seus detalhes e resultados.

## <a name="retrieving-job-status-using-windows-powershell"></a>Recuperando o status do trabalho usando o Windows PowerShell

Você pode usar o [Get-AzureRmAutomationJob](https://docs.microsoft.com/powershell/module/azurerm.automation/get-azurermautomationjob) para recuperar os trabalhos criados para um runbook e os detalhes de um trabalho específico. Se você inicia um runbook com o Windows PowerShell usando [Start-AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook), ele retorna o trabalho resultante. Use [Get-AzureRmAutomationJobOutput](https://docs.microsoft.com/powershell/module/azurerm.automation/get-azurermautomationjoboutput) para obter a saída de um trabalho.

Os comandos de exemplo a seguir recuperam o último trabalho para um exemplo de runbook e exibe seu status, os valores fornecidos para os parâmetros de runbook e a saída do trabalho.

```azurepowershell-interactive
$job = (Get-AzureRmAutomationJob –AutomationAccountName "MyAutomationAccount" `
–RunbookName "Test-Runbook" -ResourceGroupName "ResourceGroup01" | sort LastModifiedDate –desc)[0]
$job.Status
$job.JobParameters
Get-AzureRmAutomationJobOutput -ResourceGroupName "ResourceGroup01" `
–AutomationAccountName "MyAutomationAcct" -Id $job.JobId –Stream Output
```

O exemplo a seguir recupera a saída de um trabalho específico e retorna cada registro. No caso de que houve uma exceção para um dos registros, a exceção é gravada em vez do valor. Esse comportamento é útil como exceções podem fornecer informações adicionais que não podem ser registradas normalmente durante a saída.

```azurepowershell-interactive
$output = Get-AzureRmAutomationJobOutput -AutomationAccountName <AutomationAccountName> -Id <jobID> -ResourceGroupName <ResourceGroupName> -Stream "Any"
foreach($item in $output)
{
    $fullRecord = Get-AzureRmAutomationJobOutputRecord -AutomationAccountName <AutomationAccountName> -ResourceGroupName <ResourceGroupName> -JobId <jobID> -Id $item.StreamRecordId
    if ($fullRecord.Type -eq "Error")
    {
        $fullRecord.Value.Exception
    }
    else
    {
    $fullRecord.Value
    }
}
```

## <a name="get-details-from-activity-log"></a>Obter detalhes do log de atividades

Outros detalhes, como o usuário ou conta que iniciou o runbook, podem ser recuperados do log de atividades da conta de automação. O exemplo do PowerShell a seguir fornece o último usuário a executar o runbook em questão:

```powershell-interactive
$SubID = "00000000-0000-0000-0000-000000000000"
$rg = "ResourceGroup01"
$AutomationAccount = "MyAutomationAccount"
$RunbookName = "Test-Runbook"
$JobResourceID = "/subscriptions/$subid/resourcegroups/$rg/providers/Microsoft.Automation/automationAccounts/$AutomationAccount/jobs"

Get-AzureRmLog -ResourceId $JobResourceID -MaxRecord 1 | Select Caller
```

## <a name="fair-share"></a>fração justa

Para compartilhar recursos entre todos os runbooks na nuvem, a Automação do Azure descarrega ou interrompe temporariamente qualquer trabalho que tenha sido executado por mais de três horas. Os trabalhos para [runbooks com base em PowerShell](automation-runbook-types.md#powershell-runbooks) e [runbooks Python](automation-runbook-types.md#python-runbooks) são interrompidos e não são reiniciados, e o status do trabalho é mostrado como Parado.

Para tarefas de execução prolongada, é recomendável usar um [Hybrid Runbook Worker](automation-hrw-run-runbooks.md#job-behavior). Os Hybrid Runbook Workers não são limitados por fração justa e não limitam o tempo de execução de um runbook. Os outros [limites](../azure-subscription-service-limits.md#automation-limits) do trabalho se aplicam a áreas restritas do Azure e ao Hybrid Runbook Workers. Embora Hybrid Runbook Workers não sejam limitados pelo limite de fração justa de 3 horas, os runbooks executados neles ainda devem ser desenvolvidos para oferecer suporte a comportamentos de reinicialização devido a problemas de infraestrutura local inesperados.

Outra opção é otimizar o runbook usando runbooks filho. Se o runbook percorre continuamente a mesma função em diversos recursos, como uma operação de banco de dados em vários bancos de dados, você pode mover essa função para um [runbook filho](automation-child-runbooks.md) e chamá-la com o cmdlet [Start-AzureRMAutomationRunbook](/powershell/module/azurerm.automation/start-azurermautomationrunbook). Cada um desses runbooks filhos será executado em paralelo em processos separados, diminuindo a quantidade total de tempo para que o runbook pai seja concluído. Você poderá usar o cmdlet [Get-AzureRmAutomationJob](/powershell/module/azurerm.automation/Get-AzureRmAutomationJob) no seu runbook para verificar o status do trabalho de cada filho se houver operações que precisem ser executadas depois que o runbook filho for concluído.

## <a name="next-steps"></a>Próximas etapas

* Para saber mais sobre os diferentes métodos que podem ser usados para iniciar um runbook na Automação do Azure, confira [Iniciar um Runbook na Automação do Azure](automation-starting-a-runbook.md)

