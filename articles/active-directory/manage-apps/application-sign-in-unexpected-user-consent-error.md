---
title: Erro inesperado ao executar o consentimento para um aplicativo | Microsoft Docs
description: Discute os erros que podem ocorrer durante o processo de consentimento para um aplicativo e o que é possível fazer
services: active-directory
documentationcenter: ''
author: CelesteDG
manager: mtillman
ms.assetid: ''
ms.service: active-directory
ms.subservice: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 07/11/2017
ms.author: celested
ms.reviewer: asteen
ms.collection: M365-identity-device-management
ms.openlocfilehash: 89c01202e0d7d7ca0f37b89d5473f96873c52606
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/13/2019
ms.locfileid: "56210893"
---
# <a name="unexpected-error-when-performing-consent-to-an-application"></a>Erro inesperado ao executar o consentimento para um aplicativo

Este artigo discute os erros que podem ocorrer durante o processo de consentimento para um aplicativo. Se você estiver solucionando problemas de prompts de consentimento inesperado que não contenham mensagens de erro, consulte [ Cenários de autenticação do Azure AD ](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios).

Muitos aplicativos que se integram com o Azure Active Directory exigem permissões para acessar outros recursos para serem executados. Quando esses recursos também são integrados com o Azure Active Directory, as permissões para acessá-los são solicitadas usando a estrutura de consentimento comum. Um prompt de consentimento é exibido, o que geralmente ocorre na primeira vez que um aplicativo é usado, mas também pode ocorrer em um uso subseqüente do aplicativo.

Determinadas condições devem ser verdadeiras para que um usuário conceda as permissões exigidas por um aplicativo. Se essas condições não forem atendidas, os seguintes erros podem ocorrer.

## <a name="requesting-not-authorized-permissions-error"></a>Solicitação de erro de permissão não autorizada
* O **AADSTS90093:** &lt;clientAppDisplayName&gt; está solicitando uma ou mais permissões que você não está autorizado a conceder. Contate um administrador que pode consentir pedido em seu nome.

Esse erro ocorre quando um usuário que não é um administrador de empresa tenta usar um aplicativo que está solicitando permissões, as quais somente um administrador pode conceder. Esse erro pode ser resolvido por um administrador concedendo acesso ao aplicativo em nome de sua organização.

## <a name="policy-prevents-granting-permissions-error"></a>Política impede concessão de permissões de erro
* **AADSTS90093:** um administrador do &lt;tenantDisplayName&gt; definiu uma política que impede que você conceda ao &lt;nome do aplicativo&gt; as permissões solicitadas. Contate um administrador de &lt;Nome Exibiçãolocatário&gt; que pode conceder permissões para esse aplicativo em seu nome.

Esse erro ocorre quando um administrador da empresa desativa a capacidade de consentimento dos usuários para aplicativos e, em seguida, um usuário não administrador tenta usar um aplicativo que exige consentimento. Esse erro pode ser resolvido por um administrador concedendo acesso ao aplicativo em nome de sua organização.

## <a name="intermittent-problem-error"></a>Erro de problema intermitente
* **AADSTS90090:** parece que o processo de login encontrou um problema intermitente registrando as permissões que você tentou conceder a &lt;clientAppDisplayName&gt;. tente novamente mais tarde.

Esse erro indica que ocorreu um erro de serviço intermitente. Ele pode ser resolvido tentando consentir ao aplicativo novamente.

## <a name="resource-not-available-error"></a>Erro de recurso não disponível
* **AADSTS65005:** o aplicativo &lt;clientAppDisplayName&gt; solicitou permissões para acessar um recurso&lt;resourceAppDisplayName&gt; que não está disponível. 

Contate o desenvolvedor do aplicativo.

##  <a name="resource-not-available-in-tenant-error"></a>Recurso não disponível no erro do locatário
* **AADSTS65005:** &lt;NomeExibiçãoAplicativoCliente&gt; está solicitando acesso a um recurso &lt;NomeExibiçãoAplicativoRecurso&gt; que não está disponível em sua organização &lt;NomeExibiçãoLocatário&gt;. 

Certifique-se de que esse recurso está disponível ou contate o administrador de &lt;NomeExibiçãoLocatário&gt;.

## <a name="permissions-mismatch-error"></a>Erro de incompatibilidade de permissões
* **AADSTS65005:** o aplicativo solicitou consentimento para acessar o recurso &lt;resourceAppDisplayName&gt;. A solicitação falhou porque não corresponde como o aplicativo configurado previamente durante o registro do aplicativo. Contate o fornecedor do aplicativo.**

Esses erros ocorrem quando o aplicativo que um usuário está tentando consentir está solicitando permissões para acessar um aplicativo de recurso que não pode ser localizado no diretório da organização (locatário). Essa situação pode ocorrer por vários motivos:

-   O desenvolvedor do aplicativo cliente configurou seu aplicativo incorretamente, fazendo com que solicite acesso a um recurso inválido. Nesse caso, o desenvolvedor do aplicativo deve atualizar a configuração do aplicativo cliente para resolver esse problema.

-   Uma Entidade de Serviço que representa o aplicativo de recurso de destino não existe na organização ou existiu no passado mas foi removido. Para resolver esse problema, uma Entidade de Serviço para o aplicativo de recurso deve ser provisionada na organização para que o aplicativo cliente possa solicitar-lhe permissões. O Service Principal pode ser provisionado de várias maneiras, dependendo do tipo de aplicativo, incluindo:

    -   Adquirir uma assinatura para o aplicativo de recursos (aplicativos publicados pela Microsoft)

    -   Consentimento para a aplicação de recursos

    -   Conceder as permissões de aplicação através do Azure Portal

    -   Adicionar o aplicativo a partir da Galeria do Aplicativo Azure AD

## <a name="next-steps"></a>Próximas etapas 

[Aplicativos, permissões e consentimento no Azure Active Directory (ponto de extremidade v1)](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)<br>

[Escopos, permissões e consentimento no Azure Active Directory (ponto de extremidade v2.0)](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


