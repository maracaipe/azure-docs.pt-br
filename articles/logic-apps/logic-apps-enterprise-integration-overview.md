---
title: Visão geral de Enterprise Integration B2B – Aplicativos Lógicos do Azure | Microsoft Docs
description: Criar fluxos de trabalho B2B automatizados para soluções de integração empresarial com os Aplicativos Lógicos do Azure e o Enterprise Integration Pack
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: divyaswarnkar
ms.author: divswa
ms.reviewer: jonfan, estfan, LADocs
ms.topic: article
ms.assetid: dd517c4d-1701-4247-b83c-183c4d8d8aae
ms.date: 09/08/2016
ms.openlocfilehash: d37d5cb2b89b82bd9741dee0946b3a77d456b22a
ms.sourcegitcommit: 07a09da0a6cda6bec823259561c601335041e2b9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2018
ms.locfileid: "49405745"
---
# <a name="overview-b2b-enterprise-integration-scenarios-in-azure-logic-apps-with-enterprise-integration-pack"></a>Visão geral: cenários de Enterprise Integration B2B nos Aplicativos Lógicos do Azure com o Enterprise Integration Pack

Para fluxos de trabalho entre empresas (B2B) e comunicação direta com os Aplicativos Lógicos do Azure, você pode habilitar cenários de integração corporativa com a solução baseada em nuvem da Microsoft, o Enterprise Integration Pack. Organizações podem trocar mensagens eletronicamente, mesmo usando diferentes protocolos e formatos. O pacote transforma diferentes formatos em um formato que os sistemas das organizações podem interpretar e processar. As organizações podem trocar mensagens por meio de protocolos padrão da indústria, incluindo [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md) e [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md). Também é possível proteger mensagens com criptografia e assinaturas digitais.

Se você estiver familiarizado com o BizTalk Server ou os Serviços BizTalk do Microsoft Azure, os recursos do Enterprise Integration serão fáceis de usar, pois a maioria dos conceitos é semelhante. A principal diferença é que o Enterprise Integration usa contas de integração para simplificar o armazenamento e o gerenciamento de artefatos usados em comunicações B2B. 

Em termos de arquitetura, o Enterprise Integration Pack se baseia em "contas de integração". Essas contas são contêineres baseados em nuvem que armazenam todos os artefatos, como esquemas, parceiros, certificados, mapas e contratos. É possível utilizar esses artefatos para projetar, implantar e manter seus aplicativos B2B, bem como criar fluxos de trabalho B2B para aplicativos lógicos. Porém, antes de usar esses artefatos, é necessário vincular sua conta de integração ao aplicativo lógico. Depois disso, o aplicativo lógico poderá acessar os artefatos da sua conta de integração.

## <a name="why-should-you-use-enterprise-integration"></a>Por que você deve usar a integração corporativa?

* Com a integração corporativa, é possível armazenar todos os artefatos em um único local: sua conta de integração.
* É possível criar fluxos de trabalho B2B e integrá-los a aplicativos SaaS (software como serviço) de terceiros, locais e personalizados por meio do mecanismo dos Aplicativos Lógicos do Azure e todos seus conectores.
* Você pode criar código personalizado para seus aplicativos lógicos com o Azure Functions.

## <a name="how-to-get-started-with-enterprise-integration"></a>Como começar a usar a integração corporativa?

É possível criar e gerenciar aplicativos B2B com o Enterprise Integration Pack por meio do Designer de Aplicativos Lógicos no **Portal do Azure**. Também é possível gerenciar aplicativos lógicos com o [PowerShell](https://docs.microsoft.com/powershell/module/azurerm.logicapp "PowerShell para aplicativos lógicos").

Confira as etapas de alto nível necessárias para criar aplicativos no Portal do Azure:

![imagem da visão geral](media/logic-apps-enterprise-integration-overview/overview-0.png)  

## <a name="what-are-some-common-scenarios"></a>Quais são os cenários comuns?

O Enterprise Integration oferece suporte a estes padrões do setor:

* EDI - Intercâmbio Eletrônico de Dados
* EAI - Integração de Aplicativos Empresariais

## <a name="heres-what-you-need-to-get-started"></a>Para começar, você precisa do seguinte

* Uma assinatura do Azure com uma conta de integração
* Visual Studio 2015 para criar esquemas e mapas
* [Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0 (Ferramentas de integração corporativa do Aplicativo Lógico do Microsoft Azure para Visual Studio 2015)](https://aka.ms/vsmapsandschemas)  

## <a name="try-it-now"></a>Teste agora

[Implante um exemplo de aplicativo lógico de envio e recebimento AS2 totalmente operacional](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) que usa os recursos B2B do Aplicativo Lógico do Azure.

## <a name="learn-more"></a>Saiba mais
* [Contratos](../logic-apps/logic-apps-enterprise-integration-agreements.md "Saiba mais sobre contratos de integração corporativa")
* [Cenários B2B (Entre empresas)](../logic-apps/logic-apps-enterprise-integration-b2b.md "Aprenda a criar Aplicativos lógicos com recursos de B2B")  
* [Certificados](logic-apps-enterprise-integration-certificates.md "Saiba mais sobre certificados da integração corporativa")
* [Codificação/decodificação de arquivo simples](logic-apps-enterprise-integration-flatfile.md "Aprenda a codificar e decodificar o conteúdo de arquivo simples")  
* [Integration accounts](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn about contas de integração")
* [Mapas](../logic-apps/logic-apps-enterprise-integration-maps.md "Saiba mais sobre mapas da integração corporativa")
* [Parceiros](logic-apps-enterprise-integration-partners.md "Saiba mais sobre parceiros da integração corporativa")
* [Esquemas](logic-apps-enterprise-integration-schemas.md "Saiba mais sobre esquemas de integração corporativa")
* [Validação de mensagem XML](logic-apps-enterprise-integration-xml.md "Aprenda a validar mensagens XML com Aplicativos lógicos")
* [Transformação de XML](logic-apps-enterprise-integration-transform.md "Saiba mais sobre mapas da integração corporativa")
* [Conectores de integração Enterprise](../connectors/apis-list.md "Saiba mais sobre os conectores do enterprise integration pack")
* [Metadados da conta de integração](../logic-apps/logic-apps-enterprise-integration-metadata.md "Saiba mais sobre os metadados da conta de integração")
* [Monitorar mensagens B2B](logic-apps-monitor-b2b-message.md "Saiba mais sobre o monitoramento de mensagens B2B")
* [Rastrear mensagens B2B no Azure Log Analytics](logic-apps-track-b2b-messages-omsportal.md "Saiba mais sobre como rastrear mensagens B2B no Azure Log Analytics")

