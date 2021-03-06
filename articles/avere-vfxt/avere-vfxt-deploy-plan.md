---
title: Planejar seu sistema Avere vFXT – Azure
description: Explica o planejamento a ser feito antes de implantar o Avere vFXT para o Azure
author: ekpgh
ms.service: avere-vfxt
ms.topic: conceptual
ms.date: 01/29/2019
ms.author: v-erkell
ms.openlocfilehash: a097110bac7dad630f9a85dd8b20678db0c739cf
ms.sourcegitcommit: 947b331c4d03f79adcb45f74d275ac160c4a2e83
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/05/2019
ms.locfileid: "55744649"
---
# <a name="plan-your-avere-vfxt-system"></a>Planejar seu sistema Avere vFXT

Este artigo explica como planejar um novo vFXT Avere para o cluster do Azure para garantir que o cluster que você cria seja posicionado e dimensionado adequadamente para as suas necessidades. 

Antes de passar para o Azure Marketplace ou criar qualquer VM, considere como o cluster vai interagir com outros elementos no Azure. Planeje o local em que os recursos de cluster estarão localizados em sua rede privada e sub-redes e decida qual será seu armazenamento de back-end. Certifique-se de que os nós de cluster que você cria sejam eficientes o suficiente para dar suporte ao seu fluxo de trabalho. 

Continue lendo para saber mais.

## <a name="resource-group-and-network-infrastructure"></a>Infraestrutura de rede e grupo de recursos

Considere o local em que os elementos de seu vFXT Avere para implantação do Azure estarão. O diagrama a seguir mostra uma possível disposição para o vFXT Avere para componentes do Azure:

![Diagrama mostrando o cluster de controlador e o cluster de VMs em uma sub-rede. Em torno da sub-rede limite há um limite de rede virtual. Dentro da vnet, há um hexágono que representa o ponto de extremidade de serviço de armazenamento; ele está conectado com uma seta tracejada para um Armazenamento de Blobs fora da rede virtual.](media/avere-vfxt-components-option.png)

Siga estas diretrizes ao planejar a infraestrutura de rede do seu sistema do Avere vFXT:

* Todos os elementos devem ser gerenciados com uma nova assinatura criada para a implantação do vFXT Avere. Os benefícios incluem: 
  * Acompanhamento de custo mais simples – exibir e auditar todos os custos de ciclos de recursos, infraestrutura e computação em uma assinatura de auditoria.
  * Limpeza mais fácil – você pode remover toda a assinatura quando tiver terminado o projeto.
  * Particionamento conveniente do recurso de cotas – proteger outras cargas de trabalho críticas contra possível limitação de recursos ao trazer o grande número de clientes usados para seu fluxo de trabalho de computação de alto desempenho isolando os clientes do Avere vFXT e do cluster em uma assinatura única.

* Localize seus sistemas de computação de cliente perto do cluster vFXT. O armazenamento de back-end pode ser mais remoto.  

* Para manter a simplicidade, localize o cluster vFXT e a VM do controlador de cluster na mesma rede virtual (vnet) e no mesmo grupo de recursos. Também devem usar a mesma conta de armazenamento. (O controlador de cluster cria o cluster e também pode ser usado para gerenciamento de cluster de linha de comando.)  

  > [!NOTE] 
  > O modelo de criação de cluster pode criar um novo grupo de recursos e uma nova conta de armazenamento para o cluster. Você pode especificar um grupo de recursos, mas ele deve estar vazio.

* O cluster deve estar localizado em sua própria sub-rede para evitar conflitos de endereço IP com clientes ou recursos de computação. 

## <a name="ip-address-requirements"></a>Requisitos de endereço IP 

Certifique-se de que a sub-rede do seu cluster tenha um intervalo de endereços IP grande o suficiente para dar suporte ao cluster. 

O cluster do Avere vFXT usa os seguintes endereços IP:

* Um endereço IP de gerenciamento de cluster. Esse endereço pode se mover de nó a nó no cluster, mas está sempre disponível para que você possa se conectar à ferramenta de configuração do Painel de Controle do Avere.
* Para cada nó de cluster:
  * Pelo menos um endereço IP voltado para o cliente. (Todos os endereços voltados ao cliente são gerenciados do *vserver* do cluster e você pode movê-los entre os nós conforme necessário.)
  * Um endereço IP para comunicação de cluster
  * Endereço IP de uma instância (atribuído à VM)

Se você usar o Armazenamento de Blobs do Azure, ele também poderá exigir endereços IP de rede de virtual do cluster:  

* Uma conta de Armazenamento de Blobs do Azure exige pelo menos cinco endereços IP. Lembre-se desse requisito se você localizar o Armazenamento de Blobs na mesma rede virtual do cluster.
* Se você usar um Armazenamento de Blobs do Azure que esteja fora da rede virtual para o cluster, deverá criar um ponto de extremidade de serviço de armazenamento dentro da vnet. Esse ponto de extremidade não usa um endereço IP.

Você tem a opção de localizar recursos de rede e Armazenamento de Blobs (se usado) em diferentes grupos de recursos do cluster.

## <a name="vfxt-node-sizes"></a>tamanhos de nó do vFXT 

As VMs que atuam como nós de cluster determinam a capacidade de armazenamento e a taxa de transferência de solicitação do seu cache. Você pode escolher entre dois tipos de instância, com diferentes características de memória, processador e armazenamento local. 

Cada nó vFXT será idêntico. Ou seja, se você criar um cluster de três nós, terá três VMs do mesmo tipo e tamanho. 

| Tipo de instância | vCPUs | Memória  | Armazenamento SSD local  | Discos de dados máximos | Taxa de transferência de disco sem cache | NIC (contagem) |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_D16s_v3 | 16  | 64 GiB  | 128 GiB  | 32 | 25.600 IOPS <br/> 384 MBps | 8.000 MBps (8) |
| Standard_E32s_v3 | 32  | 256 GiB | 512 GiB  | 32 | 51.200 IOPS <br/> 768 MBps | 16.000 MBps (8)  |

O cache de disco por nó é configurável e pode variar de 1.000 GB a 8.000 GB. 1 TB por nó é o tamanho de cache recomendado para nós Standard_D16s_v3 e 4 TB por nó são recomendados para nós Standard_E32s_v3.

Para obter informações adicionais sobre essas VMs, leia os seguintes documentos do Microsoft Azure:

* [Tamanhos das máquinas virtuais de uso geral](https://docs.microsoft.com/azure/virtual-machines/windows/sizes-general)
* [Tamanhos de máquina virtual otimizada para memória](https://docs.microsoft.com/azure/virtual-machines/windows/sizes-memory)

## <a name="account-quota"></a>Cota da conta

Verifique se sua assinatura tem a capacidade para executar o cluster de do Avere vFXT, bem como todos os sistemas de computação ou cliente que estejam sendo usados. Leia [Cota para o cluster vFXT](avere-vfxt-prereqs.md#quota-for-the-vfxt-cluster) para obter detalhes.

## <a name="back-end-data-storage"></a>Armazenamento de dados de back-end

Em que local o cluster do Avere vFXT deve armazenar seus dados quando eles não estiverem em cache? Decida se seu conjunto de trabalho será armazenado a longo prazo em um novo contêiner de Blobs ou em um sistema de armazenamento de hardware ou de nuvem existente. 

Se você quiser usar o Armazenamento de Blobs do Azure para o back-end, deverá criar um novo contêiner como parte da criação do cluster vFXT. Essa opção cria e configura o novo contêiner para que ele esteja pronto para uso assim que o cluster estiver pronto. 

Leia [Criar o Avere vFXT para Azure](avere-vfxt-deploy.md#create-the-avere-vfxt-for-azure) para obter detalhes.

> [!NOTE]
> Somente contêineres de Armazenamento de Blobs vazios podem ser usados como arquivistas principais para o sistema de vFXT Avere. O vFXT deve ser capaz de gerenciar seu armazenamento de objeto sem necessidade de preservar os dados existentes. 
>
> Leia [Movimentação de dados para o cluster do vFXT](avere-vfxt-data-ingest.md) para aprender a copiar dados para o novo contêiner do cluster com eficiência usando computadores cliente e o cache do Avere vFXT.

Se você quiser usar um sistema de armazenamento local existente, adicione-o ao cluster vFXT após sua criação. Leia [Configurar armazenamento](avere-vfxt-add-storage.md) para obter instruções detalhadas sobre como adicionar um sistema de armazenamento ao cluster do Avere vFXT.

## <a name="cluster-access"></a>Acesso ao cluster 

O cluster do Avere vFXT para Azure está localizado em uma sub-rede privada e o cluster não tem um endereço IP público. Você deve ter algum método para acessar a sub-rede privada para conexões de cliente e administração de cluster. 

As opções de acesso incluem:

* Host de atalho – atribua um endereço IP público a uma VM separada na rede privada e use-o para criar um túnel SSL para os nós de cluster. 

  > [!TIP]
  > Se você definir um endereço IP público no controlador de cluster, poderá usá-lo como o host de atalho. Leia [Controlador de cluster como host de atalho](#cluster-controller-as-jump-host) para obter mais informações.

* VPN (rede virtual privada) – configure uma VPN ponto a site ou site a site para sua rede privada.

* Azure ExpressRoute – configure uma conexão privada por meio de um parceiro do ExpressRoute. 

Para obter detalhes sobre essas opções, leia a [Documentação da Rede Virtual do Azure sobre comunicação com a Internet](../virtual-network/virtual-networks-overview.md#communicate-with-the-internet).

### <a name="cluster-controller-as-jump-host"></a>Controlador de cluster como host de atalho

Se você definir um endereço IP público no controlador de cluster, poderá usá-lo como um host de atalho para contatar o cluster do Avere vFXT de fora da sub-rede privada. No entanto, como o controlador tem privilégios de acesso para modificar nós de cluster, isso cria um pequeno risco de segurança.  

Para maior segurança com um endereço IP público, use um grupo de segurança de rede para permitir acesso de entrada somente pela porta 22. Opcionalmente, você pode proteger ainda mais o sistema bloqueando o acesso a seu intervalo de endereços IP de origem, ou seja, permitir somente conexões de computadores que você pretende usar para acesso ao cluster.

Ao criar o cluster, você pode escolher se deseja ou não criar um endereço IP público no controlador de cluster. 

* Se você criar uma VNET ou uma nova sub-rede, o controlador de cluster receberá um endereço IP público.
* Se você selecionar uma VNET e uma sub-rede existentes, o controlador de cluster terá apenas os endereços IP privados. 

## <a name="next-step-understand-the-deployment-process"></a>Próxima etapa: Compreender o processo de implantação

A [Visão geral da implantação](avere-vfxt-deploy-overview.md) apresenta uma visão geral de todas as etapas necessárias para criar um Avere vFXT para o sistema do Azure e prepará-lo para veicular dados.  