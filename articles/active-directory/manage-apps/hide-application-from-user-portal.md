---
title: Ocultar um aplicativo da experiência do usuário no Azure Active Directory | Microsoft Docs
description: Como ocultar um aplicativo da experiência do usuário em painéis de acesso do Microsoft Azure Active Directory ou inicializadores do Office 365.
services: active-directory
author: CelesteDG
manager: mtillman
ms.service: active-directory
ms.subservice: app-mgmt
ms.workload: identity
ms.topic: conceptual
ms.date: 11/12/2018
ms.author: celested
ms.reviewer: kasimpso
ms.collection: M365-identity-device-management
ms.openlocfilehash: 59c4fa0149b4a8f59dc4fa1e30936b35c1a5ac90
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/13/2019
ms.locfileid: "56191751"
---
# <a name="hide-applications-from-end-users-in-azure-active-directory"></a>Ocultar aplicativos de usuários finais no Azure Active Directory

Instruções sobre como ocultar aplicativos do painel MyApps dos usuários finais ou inicializador do Office 365. Quando um aplicativo estiver oculto, os usuários ainda terão permissões para o aplicativo. 

## <a name="prerequisites"></a>Pré-requisitos

Os privilégios de administrador do aplicativo são necessários para ocultar um aplicativo do painel MyApps e do inicializador do Office 365.

São necessários privilégios globais de administrador para ocultar todos os aplicativos do Office 365.


## <a name="hide-an-application-from-the-end-user"></a>Ocultar um aplicativo do usuário final
Use as etapas a seguir para ocultar um aplicativo do painel MyApps e do inicializador do aplicativo do Office 365.

1.  Entre no [portal do Azure](https://portal.azure.com) como o administrador global do diretório.
2.  Selecione **Azure Active Directory**.
3.  Selecione **Aplicativos empresariais**. A folha **Aplicativos empresariais - Todos os aplicativos** abre.
4.  Em **Tipo de Aplicativo**, selecione **Aplicativos Empresariais**, se já não estiver selecionado.
5.  Procure o aplicativo que você quer ocultar e clique no aplicativo.  A visão geral do aplicativo é aberta.
6.  Clique em **Propriedades**. 
7.  Para a pergunta **Visível para os usuários?**, clique em **Não**.
8.  Clique em **Salvar**.


## <a name="hide-office-365-applications-from-the-myapps-panel"></a>Ocultar aplicativos do Office 365 no painel MyApps

Use as seguintes etapas para ocultar todos os aplicativos do Office 365 no painel MyApps. Os aplicativos ainda estão visíveis no portal do Office 365.

1.  Entre no [Portal do Azure](https://portal.azure.com) como um administrador global do diretório.
2.  Selecione **Azure Active Directory**.
3.  Selecione **Configurações de usuário**.
4.  Em **Aplicativos empresariais**, clique em **Gerenciar como os usuários finais inicializam e exibem os aplicativos.**
5.  Para **Usuários só podem ver aplicativos do Office 365 no portal do Office 365**, clique em **Sim**.
6.  Clique em **Salvar**.


## <a name="next-steps"></a>Próximas etapas
* [Ver todos os meus grupos](../fundamentals/active-directory-groups-view-azure-portal.md)
* [Atribuir um usuário ou um grupo a um aplicativo empresarial](assign-user-or-group-access-portal.md)
* [Remover uma atribuição de usuário ou de grupo de um aplicativo empresarial](remove-user-or-group-access-portal.md)
* [Alterar o nome ou logotipo de um aplicativo empresarial](change-name-or-logo-portal.md)

