---
title: Usando perfis de versão de API com o Python no Azure Stack | Microsoft Docs
description: Saiba mais sobre como usar perfis de versão de API com o Python no Azure Stack.
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2019
ms.author: sethm
ms.reviewer: sijuman
ms.lastreviewed: 01/05/2019
<!-- dev: viananth -->
ms.openlocfilehash: c7c23352cea4f9e79b371f38112fb66ac31ac849
ms.sourcegitcommit: 898b2936e3d6d3a8366cfcccc0fccfdb0fc781b4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/30/2019
ms.locfileid: "55242290"
---
# <a name="use-api-version-profiles-with-python-in-azure-stack"></a>Use perfis de versão de API com o Python no Azure Stack

*Aplica-se a: Integrados do Azure Stack, sistemas e o Kit de desenvolvimento do Azure Stack*

## <a name="python-and-api-version-profiles"></a>Perfis de versão da API e Python

O SDK do Python dá suporte a perfis de versão da API para direcionar diferentes plataformas de nuvem, como o Azure Stack e o Azure global. Você pode usar perfis de API na criação de soluções para uma nuvem híbrida. O SDK do Python dá suporte aos seguintes perfis de API:

- **latest**  
    Esse perfil tem como alvo as versões de API mais recentes para todos os provedores de serviço na plataforma do Azure.
- **2018-03-01-hybrid**     
    Esse perfil tem como alvo as versões de API mais recentes para todos os provedores de recursos na plataforma do Azure Stack.
- **2017-03-09-profile**  
    Esse perfil tem como alvo as versões de API mais compatível com provedores de recursos com suporte do Azure Stack.

   Para obter mais informações sobre perfis de API e o Azure Stack, consulte [perfis de versão da API de gerenciar no Azure Stack](azure-stack-version-profiles.md).

## <a name="install-the-azure-python-sdk"></a>Instalar o SDK do Python do Azure

1. Instale o Git [o site oficial do](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
2. Para obter instruções sobre como instalar o SDK do Python, consulte [do Azure para desenvolvedores de Python](/python/azure/python-sdk-azure-install?view=azure-python).
3. Se não estiver disponível, crie uma assinatura e salve a ID da assinatura para uso posterior. Para obter instruções sobre como criar uma assinatura, consulte [criar assinaturas de ofertas no Azure Stack](../azure-stack-subscribe-plan-provision-vm.md).
4. Crie uma entidade de serviço e salve sua ID e o segredo. Para obter instruções sobre como criar uma entidade de serviço para o Azure Stack, consulte [fornecer acesso a aplicativos para o Azure Stack](../azure-stack-create-service-principals.md).
5. Verifique se que a entidade de serviço tem a função de proprietário/Colaborador em sua assinatura. Para obter instruções sobre como atribuir a função à entidade de serviço, consulte [fornecer acesso a aplicativos para o Azure Stack](../azure-stack-create-service-principals.md).

## <a name="prerequisites"></a>Pré-requisitos

Para usar o SDK do Python do Azure com o Azure Stack, você deve fornecer os seguintes valores e, em seguida, definir valores com variáveis de ambiente. Consulte as instruções após a tabela para seu sistema operacional sobre como definir as variáveis de ambiente.

| Valor | Variáveis de ambiente | DESCRIÇÃO |
|---------------------------|-----------------------|-------------------------------------------------------------------------------------------------------------------------|
| ID do locatário | AZURE_TENANT_ID | O valor do Azure Stack [ID do locatário](../azure-stack-identity-overview.md). |
| ID do cliente | AZURE_CLIENT_ID | O serviço de ID do aplicativo principal salvo quando a entidade de serviço foi criada na seção anterior deste artigo. |
| ID da assinatura | AZURE_SUBSCRIPTION_ID | O [ID da assinatura](../azure-stack-plan-offer-quota-overview.md#subscriptions) é como você pode acessar ofertas no Azure Stack. |
| Segredo do cliente | AZURE_CLIENT_SECRET | O segredo do aplicativo principal do serviço salvo quando a entidade de serviço foi criada. |
| Ponto de extremidade do Gerenciador de recursos | ARM_ENDPOINT | Consulte a [ponto de extremidade de Gerenciador de recursos do Azure Stack](azure-stack-version-profiles-ruby.md#the-azure-stack-resource-manager-endpoint). |
| Local do recurso | AZURE_RESOURCE_LOCATION | A localização de recursos do seu ambiente de pilha do Azure.

## <a name="python-samples-for-azure-stack"></a>Exemplos de Python para o Azure Stack

Estes são alguns dos exemplos de código disponíveis para o Azure Stack usando o SDK do Python:

- [Gerenciar recursos e grupos de recursos](https://azure.microsoft.com/resources/samples/hybrid-resourcemanager-python-manage-resources/).
- [Gerenciar conta de armazenamento](https://azure.microsoft.com/resources/samples/hybrid-storage-python-manage-storage-account/).
- [Gerenciar máquinas virtuais](https://azure.microsoft.com/resources/samples/hybrid-compute-python-manage-vm/).

## <a name="python-manage-virtual-machine-sample"></a>Exemplo de máquina virtual de gerenciar do Python

Você pode usar o exemplo de código a seguir para executar tarefas comuns de gerenciamento para máquinas virtuais no Azure Stack. O exemplo de código mostra a você como:

- Crie máquinas virtuais:
  - Criar uma máquina virtual Linux
  - Criar uma máquina virtual do Windows
- Atualize uma máquina virtual:
  - Expandir uma unidade
  - Marque uma máquina virtual
  - Anexar discos de dados
  - Desanexar discos de dados
- Opere uma máquina virtual:
  - Iniciar uma máquina virtual
  - Parar uma máquina virtual
  - Reiniciar uma máquina virtual
- Listar máquinas virtuais
- Excluir uma máquina virtual

Para examinar o código que executa essas operações, consulte o **run_example()** função no script do Python **example.py** no repositório GitHub [híbrida-Compute-Python-gerenciar-VM](https://github.com/Azure-Samples/Hybrid-Compute-Python-Manage-VM).

Cada operação é claramente rotulada com um comentário e uma função de impressão. Os exemplos não são necessariamente na ordem mostrada nessa lista.

## <a name="run-the-python-sample"></a>Executar o exemplo de Python

1. Se você ainda não tiver [instalar o Python](https://www.python.org/downloads/). Este exemplo (e o SDK) são compatível com o Python 2.7, 3.4, 3.5 e 3.6.

2. A recomendação geral para o desenvolvimento do Python é usar um ambiente Virtual. Para obter mais informações, consulte o [documentação do Python](https://docs.python.org/3/tutorial/venv.html).

3. Instalar e inicializar o ambiente virtual com o módulo de "venv" no Python 3 (você deve instalar [virtualenv](https://pypi.python.org/pypi/virtualenv) para Python 2.7):

    ```bash
    python -m venv mytestenv # Might be "python3" or "py -3.6" depending on your Python installation
    cd mytestenv
    source bin/activate      # Linux shell (Bash, ZSH, etc.) only
    ./scripts/activate       # PowerShell only
    ./scripts/activate.bat   # Windows CMD only
    ```

4. Clone o repositório:

    ```bash
    git clone https://github.com/Azure-Samples/Hybrid-Compute-Python-Manage-VM.git
    ```

5. Instale as dependências usando o pip:

    ```bash
    cd Hybrid-Compute-Python-Manage-VM
    pip install -r requirements.txt
    ```

6. Criar uma [entidade de serviço](../azure-stack-create-service-principals.md) para trabalhar com o Azure Stack. Certifique-se a entidade de serviço tenha [função de Colaborador/proprietário](../azure-stack-create-service-principals.md#assign-a-role) em sua assinatura.

7. Defina as seguintes variáveis e exportar essas variáveis de ambiente em seu shell atual:

    ```bash
    export AZURE_TENANT_ID={your tenant id}
    export AZURE_CLIENT_ID={your client id}
    export AZURE_CLIENT_SECRET={your client secret}
    export AZURE_SUBSCRIPTION_ID={your subscription id}
    export ARM_ENDPOINT={your AzureStack Resource Manager Endpoint}
    export AZURE_RESOURCE_LOCATION={your AzureStack Resource location}
    ```

8. Para executar este exemplo, Ubuntu 16.04-LTS e imagens do Windows Server 2012-R2-Datacenter devem estar presentes no marketplace do Azure Stack. Eles podem ser qualquer um [baixado do Azure](../azure-stack-download-azure-marketplace-item.md), ou adicionado para o [repositório de imagens de plataforma](../azure-stack-add-vm-image.md).

9. Execute o exemplo:

    ```python
    python example.py
    ```


## <a name="next-steps"></a>Próximas etapas

- [Centro de desenvolvimento do Python do Azure](https://azure.microsoft.com/develop/python/)
- [Documentação de máquinas virtuais do Azure](https://azure.microsoft.com/services/virtual-machines/)
- [Roteiro de aprendizagem para máquinas virtuais](/learn/paths/deploy-a-website-with-azure-virtual-machines/)
- Se você não tiver uma assinatura do Microsoft Azure, você pode obter uma conta de avaliação gratuita [aqui](https://go.microsoft.com/fwlink/?LinkId=330212).
