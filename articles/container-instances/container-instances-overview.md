---
title: O que são as Instâncias de Contêiner do Azure?
description: O serviço das Instâncias de Contêiner do Azure oferece a maneira mais rápida e mais simples de executar contêineres isolados no Azure, sem a necessidade de gerenciar máquinas virtuais nem adotar um orquestrador de nível superior.
services: container-instances
author: seanmck
manager: jeconnoc
ms.service: container-instances
ms.topic: overview
ms.date: 11/30/2018
ms.author: seanmck
ms.custom: seodec18, mvc
ms.openlocfilehash: ba454965ff2bb78ebe526e71d9280200b1f4b08b
ms.sourcegitcommit: 5b869779fb99d51c1c288bc7122429a3d22a0363
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2018
ms.locfileid: "53187187"
---
# <a name="what-is-azure-container-instances"></a>O que são as Instâncias de Contêiner do Azure?

Os contêineres estão se tornando o modo preferido para empacotar, implantar e gerenciar aplicativos de nuvem. As Instâncias de Contêiner do Azure oferecem a maneira mais rápida e simples para executar um contêiner no Azure, sem a necessidade de gerenciar máquinas virtuais nem adotar um serviço de nível superior.

As Instâncias de Contêiner do Azure são uma ótima solução para qualquer cenário que possa ser usado em contêineres isolados, incluindo aplicativos simples, automação de tarefas e criação de trabalhos. Para cenários em que você precisa de orquestração de contêineres completa, incluindo descoberta do serviço em vários contêineres, dimensionamento automático e atualizações de aplicativo coordenadas, recomendamos o [AKS (Serviço de Kubernetes do Azure)](../aks/index.yml).

## <a name="fast-startup-times"></a>Inicialização mais rápida

Os contêineres oferecem vantagens significativas de inicialização em relação às VMs (máquinas virtuais). As Instâncias de Contêiner do Azure podem iniciar contêineres no Azure em segundos, sem a necessidade de provisionar nem gerenciar VMs.

## <a name="public-ip-connectivity-and-dns-name"></a>Conectividade de IP público e nome DNS

As Instâncias de Contêiner do Azure permitem expor seus contêineres diretamente à Internet com um endereço IP e um FQDN (nome de domínio totalmente qualificado). Quando você cria uma instância de contêiner, pode especificar uma etiqueta de nome de DNS personalizado para que o seu aplicativo seja acessível em *customlabel*.*azureregion*.azurecontainer.io.

## <a name="hypervisor-level-security"></a>Segurança em nível de hipervisor

Historicamente, os contêineres ofereciam isolamento de dependência de aplicativo e governança de recursos, mas não eram considerados suficientemente protegidos para uso com vários locatários hostis. As Instâncias de Contêiner do Azure garantem que seu aplicativo fique tão isolado em um contêiner quanto ficaria em uma VM.

## <a name="custom-sizes"></a>Tamanhos personalizados

Os contêineres normalmente são otimizados para executar apenas um único aplicativo, mas as necessidades exatas desses aplicativos podem variar significativamente. As Instâncias de Contêiner do Azure fornecem uma utilização ideal ao permitirem especificações exatas de núcleos e memória da CPU. Você paga com base no que precisar e é cobrado por segundo, assim, é possível ajustar seus gastos eficientemente com base em suas necessidades reais.

Para trabalhos de computação intensiva, como o aprendizado de máquina, as Instâncias de Contêiner do Azure podem agendar contêineres do Linux para usar os [recursos da GPU](container-instances-gpu.md) da NVIDIA Tesla (versão prévia).

## <a name="persistent-storage"></a>Armazenamento persistente

Para recuperar e persistir estados com as Instâncias de Contêiner do Azure, nós oferecemos a [montagem direta de compartilhamentos de arquivos do Azure](container-instances-mounting-azure-files-volume.md).

## <a name="linux-and-windows-containers"></a>Contêineres do Windows e do Linux

As Instâncias de Contêiner do Azure podem agendar contêineres do Windows e do Linux com a mesma API. Basta especificar o tipo de sistema operacional ao criar seus [grupos de contêiner](container-instances-container-groups.md).

Alguns recursos são atualmente restritos a contêineres do Linux. Enquanto trabalhamos para trazer paridade de recursos para contêineres do Windows, você pode encontrar diferenças da plataforma atual em [Cotas e disponibilidade de região para Instâncias de Contêiner do Azure](container-instances-quotas.md).

As Instâncias de Contêiner do Azure dão suporte a imagens do Windows com base nas versões de Canal de Manutenção de Longo Prazo (LTSC). Versões do Canal Semestral (SAC) do Windows como 1709 e 1803 não são suportadas.

## <a name="co-scheduled-groups"></a>Grupos coagendados

As Instâncias de Contêiner do Azure são compatíveis com a programação de [grupos com vários contêineres](container-instances-container-groups.md) que compartilham um computador host, uma rede local, um armazenamento e um ciclo de vida. Isso permite que você combine seu aplicativo principal com outros contêineres com função de suporte, como sidecars de log.

## <a name="virtual-network-deployment-preview"></a>Implantação da rede virtual (versão prévia)

Atualmente em versão prévia, esse recurso de Instâncias de Contêiner do Azure permite [implantação de instâncias de contêiner em uma Rede Virtual do Azure](container-instances-vnet.md). Ao implantar instâncias de contêiner em uma sub-rede em sua rede virtual, elas podem se comunicar com segurança com outros recursos na rede virtual, incluindo os que são locais (por meio do [Gateway de VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md) ou do [ExpressRoute](../expressroute/expressroute-introduction.md)).

> [!IMPORTANT]
> Determinados recursos de Instâncias de Contêiner do Azure estão em visualização e algumas [limitações se aplicam](container-instances-vnet.md#preview-limitations). As versões prévias são disponibilizadas com a condição de que você concorde com os [termos de uso complementares][terms-of-use]. Alguns aspectos desses recursos podem ser alterados antes da disponibilidade geral (GA).

## <a name="next-steps"></a>Próximas etapas

Tente implantar um contêiner no Azure com um único comando usando nosso guia de início rápido:

> [!div class="nextstepaction"]
> [Início Rápido de Instâncias de Contêiner do Azure](container-instances-quickstart.md)

<!-- LINKS - External -->
[terms-of-use]: https://azure.microsoft.com/support/legal/preview-supplemental-terms/
