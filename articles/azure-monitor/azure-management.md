---
title: Gerenciamento do Azure e Operations Management Suite (OMS) | Microsoft Docs
description: Visão geral das áreas de gerenciamento de aplicativos do Azure e recursos com links para conteúdo sobre ferramentas de gerenciamento do Azure que foram anteriormente empacotadas como Operations Management Suite (OMS).
documentationcenter: ''
author: bwren
manager: carmonm
editor: tysonn
ms.service: monitoring
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/07/2018
ms.author: bwren
ms.openlocfilehash: e0ad6b212e328612d2934562e1292b5c36546478
ms.sourcegitcommit: e69fc381852ce8615ee318b5f77ae7c6123a744c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "55990241"
---
# <a name="azure-management---monitoring"></a>Gerenciamento do Azure - monitoramento

Monitoramento no Azure é um aspecto do Gerenciamento do Azure.  Este artigo descreve brevemente as diferentes áreas de gerenciamento necessários para implantar e manter seus aplicativos e recursos no Azure com links para documentação para você começar.

## <a name="management-in-azure"></a>Gerenciamento no Azure

Gerenciamento refere-se às tarefas e processos necessários para manter seus aplicativos de negócios e os recursos que dão suporte a eles.  O Azure tem vários serviços e ferramentas que funcionam em conjunto para fornecer gerenciamento completo para não apenas os aplicativos em execução no Azure, mas também em outras nuvens e locais.  Entender as noções básicas sobre as diferentes ferramentas disponíveis e como eles podem ser usados juntos para uma variedade de cenários de gerenciamento é a primeira etapa na criação de um ambiente de gerenciamento completo.

O diagrama a seguir ilustra as diferentes áreas de gerenciamento que são necessárias para manter qualquer aplicativo ou recurso.  Essas diferentes áreas podem ser consideradas em termos de um ciclo de vida em que cada um é necessário em sequência contínua ao longo do tempo de vida de um recurso.  Isso inicia com sua implantação inicial, por meio de sua operação contínua e, finalmente, quando ele é desativado.

![Recursos de gerenciamento](media/management-overview/management-capabilities.png)


As seções a seguir descrevem resumidamente as diferentes áreas de gerenciamento e fornecem links para conteúdo detalhado sobre os principais serviços do Azure destinados a abordá-las.

## <a name="monitor"></a>Monitoramento
O monitoramento é o ato de coletar e analisar dados para determinar o desempenho, a integridade e a disponibilidade do seu aplicativo de negócios e os recursos necessários. Uma estratégia de monitoramento efetiva irá ajudá-lo a entender a operação detalhada dos diferentes componentes do aplicativo e a aumentar o tempo de atividade, notificando-o proativamente sobre problemas críticos para que possa resolvê-los antes de se tornarem problemas. O monitoramento no Azure é fornecido principalmente pelo [Azure Monitor](../azure-monitor/overview.md), que fornece armazenamentos comuns para armazenar dados de monitoramento, diversas fontes de dados para coletar dados das diferentes camadas que dão suporte a seu aplicativo e recursos para analisar e responder a dados coletados.

## <a name="configure"></a>Configurar
Configurar refere-se à implantação inicial e à configuração de aplicativos e recursos, bem como sua manutenção contínua com patches e atualizações.  A automação dessas tarefas por meio de script e política permite que você elimine a redundância, minimizando o tempo e esforço e aumentando a precisão e a eficiência.  A [Automação do Azure](../automation/automation-intro.md) fornece a maior parte dos serviços para automatizar tarefas de configuração.  Além de runbooks para automatizar processos, ele fornece configuração e gerenciamento de atualizações, que auxiliam no gerenciamento de configuração por meio da política e na identificação e implantação de atualizações.

## <a name="govern"></a>Administrar
Governança fornece mecanismos e processos para manter controle sobre seus aplicativos e recursos no Azure.  Ela envolve planejar suas iniciativas e estabelecer prioridades estratégicas.  Governança no Azure é implementada principalmente com dois serviços.  O [Azure Policy](../governance/policy/overview.md) permite que você crie, atribua e gerencie definições de política que aplicam diferentes regras e ações sobre seus recursos para que esses recursos permaneçam em conformidade com seus padrões corporativos e contratos de nível de serviço. O [Gerenciamento de Custos do Azure pelo Cloudyn](../cost-management/overview.md) permite acompanhar o uso da nuvem e as despesas de seus recursos do Azure e de outros provedores de nuvem, incluindo AWS e Google.

## <a name="secure"></a>Segurança
Gerenciar segurança de aplicativos, recursos e dados envolve uma combinação de avaliação de ameaças, coletando e analisando dados de segurança e garante que seus aplicativos e recursos sejam criados e configurados de forma segura.  A [Central de Segurança do Azure](../security-center/security-center-intro.md) fornece monitoramento de segurança e análise de ameaças, que inclui o gerenciamento unificado de segurança e proteção avançada contra ameaças em cargas de trabalho de nuvem híbrida.  Leia também a [Introdução à segurança do Azure](../security/azure-security.md) para obter informações abrangentes sobre segurança no Azure e orientação sobre como configurar com segurança os recursos do Azure.


## <a name="protect"></a>Proteger
Proteção refere-se à garantia de que seus aplicativos e dados estão sempre disponíveis, mesmo no caso de interrupções além de seu controle.  A proteção no Azure é fornecida por dois serviços.  O [Backup do Azure](../backup/backup-introduction-to-azure-backup.md) fornece backup e recuperação de seus dados, tanto na nuvem como localmente.    O [Azure Site Recovery](../site-recovery/site-recovery-overview.md) garante a alta disponibilidade do seu aplicativo, fornecendo a continuidade dos negócios e recuperação imediata em caso de desastres.

## <a name="migrate"></a>Migrar 
Migração refere-se à transição de cargas de trabalho atualmente em execução localmente para a nuvem do Azure.  As [Migrações para Azure](../migrate/migrate-overview.md) são um serviço que ajuda a avaliar a adequação de migração, incluindo dimensionamento baseado em desempenho e estimativas de custo, de máquinas virtuais locais para o Azure.  O Azure Site Recovery pode ajudar você a executar a migração real de máquinas virtuais [do local](../site-recovery/migrate-tutorial-on-premises-azure.md) ou [do Amazon Web Services](../site-recovery/migrate-tutorial-aws-azure.md).  A [Migração de banco de dados do Azure](../dms/dms-overview.md) ajudará na migração de várias fontes de banco de dados para plataformas de dados do Azure.

