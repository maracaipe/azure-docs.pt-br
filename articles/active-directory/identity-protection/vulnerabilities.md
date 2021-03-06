---
title: Vulnerabilidades detectadas pelo Azure Active Directory Identity Protection | Microsoft Docs
description: Visão geral das vulnerabilidades detectadas pelo Azure Active Directory Identity Protection.
services: active-directory
keywords: azure active directory identity protection, cloud discovery, gerenciando aplicativos, segurança, risco, nível de risco, vulnerabilidade, política de segurança
documentationcenter: ''
author: MarkusVi
manager: daveba
ms.assetid: 92233a5b-cb34-4d28-88cc-d5d29c0f3256
ms.service: active-directory
ms.subservice: identity-protection
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2018
ms.author: markvi
ms.reviewer: nigu
ms.collection: M365-identity-device-management
ms.openlocfilehash: b5968731981e9ba602a27b6b66a53e7b67e8fa7f
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/13/2019
ms.locfileid: "56187314"
---
# <a name="vulnerabilities-detected-by-azure-active-directory-identity-protection"></a>Vulnerabilidades detectadas pelo Azure Active Directory Identity Protection
Vulnerabilidades são pontos fracos no seu ambiente que podem ser explorados por um invasor. É recomendável resolver essas vulnerabilidades para melhorar a postura de segurança de sua organização e impedir que invasores possam explorá-las.


![vulnerabilidades](./media/vulnerabilities/101.png "vulnerabilidades")



As seções a seguir fornecem uma visão geral das vulnerabilidades relatadas pelo Identity Protection.

## <a name="multi-factor-authentication-registration-not-configured"></a>Registro de autenticação multifator não configurado
Essa vulnerabilidade ajuda a controlar a implantação da Autenticação Multifator do Azure na sua organização. 

A Azure Multi-Factor Authentication fornece uma segunda camada de segurança para a autenticação do usuário. Ela ajuda a proteger o acesso a dados e aplicativos ao mesmo tempo que atende à demanda dos usuários para um processo de entrada simples. Ele fornece autenticação forte por meio de uma variedade de opções fáceis de verificação – chamada telefônica, mensagem de texto, notificação de aplicativo móvel ou código de verificação e tokens OATH de terceiros.

Recomendamos exigir a Autenticação Multifator do Azure para entradas de usuário. A autenticação multifator desempenha um papel fundamental nas políticas de acesso condicional baseadas em risco disponíveis por meio do Identity Protection.

Para obter mais informações, consulte [O que é Autenticação Multifator do Microsoft Azure?](../authentication/multi-factor-authentication.md)

## <a name="unmanaged-cloud-apps"></a>Aplicativos de nuvem não gerenciados
Essa vulnerabilidade ajuda a identificar aplicativos de nuvem não gerenciados na sua organização.

Nas empresas modernas, os departamentos de TI geralmente não estão cientes de todos os aplicativos de nuvem que os membros da sua organização usam para realizar seu trabalho. É fácil ver por que os administradores teriam preocupações sobre acesso não autorizado a dados corporativos, perda de dados e outros riscos de segurança. 

Recomendamos a implantação do Cloud Discovery para descobrir aplicativos de nuvem não gerenciados e gerenciar esses aplicativos usando o Azure Active Directory.

Para obter mais informações, confira [Cloud Discovery](/cloud-app-security/set-up-cloud-discovery).

## <a name="security-alerts-from-privileged-identity-management"></a>Alertas de Segurança do Privileged Identity Management
Essa vulnerabilidade ajuda você a descobrir e resolver alertas sobre identidades com privilégios na sua organização.  

Para permitir que os usuários executem operações com privilégios, as organizações precisam oferecer aos usuários acesso privilegiado temporário ou permanente ao Azure AD, a recursos do Azure ou do Office 365 ou a outros aplicativos SaaS. Cada um desses usuários privilegiados aumenta a superfície de ataque da sua organização. Essa vulnerabilidade ajuda você a identificar os usuários com acesso privilegiado desnecessário e tomar as devidas providências para reduzir ou eliminar o risco que eles representam. 

Recomendamos que sua organização use o Azure AD Privileged Identity Management para gerenciar, controlar e monitorar as identidades com privilégios e o acesso delas a recursos no Azure AD e em outros serviços online da Microsoft como o Office 365 ou o Microsoft Intune.

Para obter mais informações, confira [Azure AD Privileged Identity Management](../privileged-identity-management/pim-configure.md). 

## <a name="see-also"></a>Consulte também

[Azure Active Directory Identity Protection](../active-directory-identityprotection.md)

