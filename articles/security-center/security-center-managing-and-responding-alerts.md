---
title: Gerenciar alertas de segurança na Central de Segurança do Azure | Microsoft Docs
description: Este documento ajuda você a usar recursos da Central de segurança do Azure para gerenciar e responder a alertas de segurança.
services: security-center
documentationcenter: na
author: rkarlin
manager: barbkess
editor: ''
ms.assetid: b88a8df7-6979-479b-8039-04da1b8737a7
ms.service: security-center
ms.topic: conceptual
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/22/2018
ms.author: rkarlin
ms.openlocfilehash: 28a9b90e23d0d182197450e6449b8d3296fe99d6
ms.sourcegitcommit: fec0e51a3af74b428d5cc23b6d0835ed0ac1e4d8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56112913"
---
# <a name="managing-and-responding-to-security-alerts-in-azure-security-center"></a>Gerenciando e respondendo a alertas de segurança na Central de segurança do Azure
Este documento ajuda você a usar a Central de Segurança do Azure para gerenciar e responder a alertas de segurança.

> [!NOTE]
> Para habilitar as detecções avançadas, atualize para o Padrão da Central de Segurança do Azure. Há uma avaliação gratuita disponível. Para atualizar, selecione a Camada de Preços na [Política de Segurança](tutorial-security-policy.md). Consulte [Preços da Central de Segurança do Azure](security-center-pricing.md) para saber mais.
>
>

## <a name="what-are-security-alerts"></a>O que são alertas de segurança?
A Central de segurança coleta, analisa e integra automaticamente os dados de registro de seus recursos do Azure, da rede e das soluções de parceiros conectados, como firewall e soluções de proteção de ponto de extremidade, a fim de detectar ameaças reais e reduzir os falsos positivos. Uma lista priorizada de alertas de segurança é exibida na Central de Segurança, junto com as informações necessárias para investigar rapidamente o problema, e recomendações sobre como corrigir um ataque.


> [!NOTE]
> Para saber mais sobre como funciona os recursos de detecção da Central de Segurança, leia [Recursos de detecção da Central de Segurança do Azure](security-center-detection-capabilities.md).
>
>

## <a name="managing-security-alerts"></a>Configurando alertas de segurança
Você pode examinar os alertas atuais observando o bloco **Alertas de segurança** . Execute as etapas abaixo para ver mais detalhes sobre cada alerta:

1. No painel Central de Segurança, você vê o bloco **Alertas de segurança** .

    ![Bloco Alertas de segurança na Central de Segurança](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig1-ga.png)

2. Clique no bloco para os **Alertas de segurança** e ver mais detalhes sobre os alertas.

   ![Os Alertas de segurança na Central de Segurança](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig2-ga.png)

Na parte inferior dessa página estão os detalhes de cada alerta. Para classificar, clique na coluna com base na qual você deseja classificar. A definição de cada coluna é mostrada abaixo:

* **Descrição**: Uma breve explicação sobre o alerta.
* **Contagem**: Uma lista de todos os alertas desse tipo específico que foram detectados em um dia específico.
* **Detectado por**: O serviço responsável por disparar o alerta.
* **Data**: A data na qual o evento ocorreu.
* **Estado**: O estado atual desse alerta. Há dois tipos de estado:
  * **Ativo**: O alerta de segurança foi detectado.
  * **Descartado**: O alerta de segurança foi fechado pelo usuário. Esse status costuma ser usado para alertas que foram investigados e que foram atenuados ou considerados como não sendo ataques reais.
* **Gravidade**: O nível de gravidade, que pode ser alta, média ou baixa.

> [!NOTE]
> Os alertas de segurança gerados pela Central de Segurança também serão exibida no Log de Atividades do Azure. Para saber mais sobre como acessar o Log de Atividades do Azure, leia [Exibir logs de atividades para auditar ações em recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-audit).
>


### <a name="alert-severity"></a>Severidade do alerta

> [!NOTE]
> A severidade do alerta é exibida diferente no portal e a API REST, as diferenças são indicadas na lista abaixo.

-   **Alta**: Há uma grande probabilidade de que o recurso seja comprometido. Você deve analisá-lo imediatamente. A Central de Segurança tem alta confiança em ambas as más intenções e em descobertas usadas para emitir o alerta. Por exemplo, um alerta que detecta a execução de uma ferramenta mal-intencionada conhecida como Mimikatz, uma ferramenta comum usada para roubo de credenciais. 
-   **Média (baixa na API REST)**: Isso provavelmente é uma atividade suspeita que pode indicar que um recurso está comprometido.
Confiança da Central de Segurança na análise ou localizar é médio e a confiança de más intenções é médio a alto. Normalmente, esses seriam machine learning ou detecções baseadas em anomalia. Por exemplo, uma tentativa de conexão de um local anômalo.
-   **Baixa (Informação na API REST)**: Isso pode ser um positivo benigno ou um ataque bloqueado. 
    - A Central de Segurança não está confiante o suficiente para que a intenção seja mal-intencionada e a atividade possa ser inocente. Por exemplo, limpar log é uma ação que pode acontecer quando um invasor tenta ocultar seus rastros, mas em muitos casos é uma operação de rotina executada por administradores.
    - A Central de Segurança geralmente não informa quando ataques foram bloqueados, a menos que seja um caso interessante que sugerimos que você examine. 
-   **Informativo (Silencioso na API REST)**: Você só verá alertas informativos ao fazer busca detalhada em um incidente de segurança ou se você usar a API REST com uma determinada ID de alerta. Um incidente geralmente é composto de um número de alertas, alguns dos quais podem aparecer por conta própria e são apenas informativo, mas no contexto de outros alertas podem ser dignos de uma análise mais detalhada. 

### <a name="filtering-alerts"></a>Filtragem de alertas
Você pode filtrar com base na data, no estado e na gravidade dos alertas. A filtragem de alertas pode ser útil para cenários em que é necessário restringir o escopo da exibição de alertas de segurança. Por exemplo, convém lidar com os alertas de segurança que ocorreram nas últimas 24 horas, pois você está investigando uma possível falha no sistema.

1. Clique em **Filtrar** em **Alertas de Segurança**. O **Filtro** é aberto e você seleciona os valores de data, estado e gravidade que deseja ver.

    ![Filtragem de alertas na Central de Segurança](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig3-2017.png)

### <a name="respond-to-security-alerts"></a>Responder a alertas de segurança
Selecione um alerta de segurança para saber mais sobre o evento que disparou o alerta e, se houver, as etapas necessárias para corrigir um ataque. Os alertas de segurança são agrupados por tipo e data. Clicar em um alerta de segurança abre uma página que contém uma lista dos alertas agrupados.

![Responder aos alertas de segurança na Central de Segurança do Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig5-ga.png)

Nesse caso, os alertas disparados referem-se à atividade suspeita do protocolo RDP (Protocolo de Área de Trabalho Remota). A primeira coluna mostra quais recursos foram atacados; a segunda mostra quantas vezes o recurso foi atacado; a terceira mostra o horário do ataque; a quarta mostra o estado do alerta e a quarta mostra gravidade do ataque. Depois de revisar essas informações, clique no recurso que foi atacado.

![Sugestões sobre o que fazer com relação aos alertas de segurança na Central de Segurança do Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig6-ga.png)

No campo **Descrição**, você encontrará mais detalhes sobre esse evento. Esses detalhes adicionais oferecem informações sobre o que disparou o alerta de segurança, o recurso de destino e, quando aplicável, o endereço IP de origem e as recomendações sobre como corrigir.  Em alguns casos, o endereço IP de origem ficará vazio (não disponível) porque nem todos os logs de eventos de segurança do Windows incluem o endereço IP.

A correção sugerida pela Central de Segurança varia de acordo com o alerta de segurança. Em alguns casos, talvez seja necessário usar outros recursos do Azure para implementar a correção recomendada. Por exemplo, a correção para esse ataque é colocar o endereço IP que está gerando esse ataque em uma lista de contatos bloqueados usando uma [ACL de rede](../virtual-network/virtual-networks-acl.md) ou uma regra de [grupo de segurança de rede](../virtual-network/security-overview.md#security-rules). Para saber mais sobre os tipos diferentes de alertas, leia [Alertas de segurança por tipo na Central de segurança do Azure](security-center-alerts-type.md).

> [!NOTE]
> A Central de Segurança foi lançada para visualização limitada de um novo conjunto de detecções que aproveitam os registros de auditoria, uma estrutura de auditoria comum, para detectar comportamentos mal-intencionados em máquinas Linux. Envie-[nos](mailto:ASC_linuxdetections@microsoft.com) um email com suas IDs de assinatura para ingressar na versão prévia.


## <a name="see-also"></a>Consulte também
Neste documento, você aprendeu a configurar políticas de segurança na Central de Segurança. Para saber mais sobre a Central de Segurança, confira o seguinte:

* [Manipulação de incidente de segurança na Central de Segurança do Azure](security-center-incident.md)
* [Recursos de detecção da Central de Segurança do Azure](security-center-detection-capabilities.md)
* [Guia de planejamento e operações da Central de Segurança do Azure](security-center-planning-and-operations-guide.md)
* [Perguntas frequentes sobre a Central de Segurança do Azure](security-center-faq.md) – encontre as perguntas frequentes sobre como usar o serviço de localização.
* [Blog de Segurança do Azure](https://blogs.msdn.com/b/azuresecurity/) : encontre postagens no blog sobre conformidade e segurança do Azure.
