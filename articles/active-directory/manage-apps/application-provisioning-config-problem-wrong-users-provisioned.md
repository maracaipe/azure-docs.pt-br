---
title: O conjunto errado de usuários está sendo provisionado para um aplicativo da Galeria do Azure AD | Microsoft Docs
description: Descubra por que um conjunto diferente de usuários está sendo provisionado para um aplicativo em vez dos usuários esperados
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
ms.date: 09/20/2018
ms.author: celested
ms.reviewer: asteen
ms.collection: M365-identity-device-management
ms.openlocfilehash: b683abbba2013fef47f648c11a52d7767d7cdf08
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/13/2019
ms.locfileid: "56206320"
---
# <a name="wrong-set-of-users-are-being-provisioned-to-an-azure-ad-gallery-application"></a>O conjunto errado de usuários está sendo provisionado para um aplicativo da Galeria do Azure AD

Quais usuários são provisionados para o aplicativo é algo orientado principalmente por quais usuários e grupos foram **atribuídos** ao aplicativo.

Use os recursos a seguir para saber como verificar quais usuários e grupos foram atribuídos a um aplicativo no Azure Active Directory.

## <a name="assign-a-user-directly-as-an-administrator"></a>Atribuir um usuário diretamente como administrador

Para atribuir um ou mais usuários a um aplicativo diretamente, siga estas etapas:

1.  Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Abra a **Extensão do Azure Active Directory** clicando em **Todos os serviços** na parte superior do menu de navegação esquerdo principal.

3.  Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.

4.  clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.

5.  clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.

  * Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**

6.  Na lista, selecione o aplicativo ao qual deseja atribuir um usuário.

7.  Após o carregamento do aplicativo, clique em **Usuários e Grupos** no menu de navegação esquerdo do aplicativo.

8.  Abra o painel **Adicionar Atribuição** clique no botão **Adicionar** na parte superior da lista **Usuários e Grupos**.

9.  Clique no seletor **Usuários e grupos** do painel **Adicionar Atribuição**.

10. Digite o **nome completo** ou o **endereço de email** do usuário que você deseja atribuir na caixa de pesquisa **Pesquisar por nome ou endereço de email**.

11. Passe o mouse sobre o **usuário** na lista para mostrar uma **caixa de seleção**. Clique na caixa de seleção ao lado do logotipo ou da foto de perfil do usuário para adicioná-lo à lista **Selecionado**.

12. **Opcional:** Caso queira **adicionar mais de um usuário**, digite outro **nome completo** ou **endereço de email** na caixa de pesquisa **Pesquisar por nome ou endereço de email** e clique na caixa de seleção para adicionar esse usuário à lista **Selecionado**.

13. Ao concluir a seleção dos usuários, clique no botão **Selecionar** para adicioná-los à lista de usuários e grupos a serem atribuídos ao aplicativo.

14. **Opcional:** clique no seletor **Selecionar Função** no painel **Adicionar Atribuição** para selecionar uma função que será atribuída aos usuários selecionados.

15. Clique no botão **Atribuir** para atribuir o aplicativo aos usuários selecionados.

Se o provisionamento estiver configurado e em execução para um aplicativo, novos usuários deverão ser provisionados para um aplicativo em aproximadamente 10 minutos. Verifique os **Logs de auditoria** para obter detalhes.

## <a name="assign-a-group-directly-to-an-application-as-an-administrator"></a>Atribuir um grupo diretamente a um aplicativo como administrador

Para atribuir um ou mais usuários diretamente a um aplicativo, siga estas etapas:

1.  Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Abra a **Extensão do Azure Active Directory** clicando em **Todos os serviços** na parte superior do menu de navegação esquerdo principal.

3.  Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.

4.  clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.

5.  clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.

  * Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**

6.  Na lista, selecione o aplicativo ao qual deseja atribuir um usuário.

7.  Após o carregamento do aplicativo, clique em **Usuários e Grupos** no menu de navegação esquerdo do aplicativo.

8.  Abra o painel **Adicionar Atribuição** clique no botão **Adicionar** na parte superior da lista **Usuários e Grupos**.

9.  Clique no seletor **Usuários e grupos** do painel **Adicionar Atribuição**.

10. Digite o **nome completo do grupo** que você deseja atribuir na caixa de pesquisa **Pesquisar por nome ou endereço de email**.

11. Passe o mouse sobre o **grupo** na lista para mostrar uma **caixa de seleção**. Clique na caixa de seleção próxima ao logotipo ou ao perfil do grupo para adicionar o usuário na lista **Selecionado**.

12. **Opcional:** Caso queira **adicionar mais de um grupo**, digite outro **nome de grupo completo** na caixa de pesquisa **Pesquisar por nome ou endereço de email** e clique na caixa de seleção para adicionar esse grupo à lista **Selecionado**.

13. Ao concluir a seleção dos grupos, clique no botão **Selecionar** para adicioná-los à lista de usuários e grupos a serem atribuídos ao aplicativo.

14. **Opcional:** clique no seletor **Selecionar Função** no painel **Adicionar Atribuição** para selecionar uma função que será atribuída aos grupos selecionados.

15. Clique no botão **Atribuir** para atribuir o aplicativo aos grupos selecionados.

Se o provisionamento estiver configurado e em execução para um aplicativo, novos usuários contidos no grupo deverão ser provisionados para um aplicativo em aproximadamente 10 minutos. Verifique os **Logs de auditoria** para obter detalhes.

>[!IMPORTANT]
>Provisionamento do nome do grupo e dos detalhes do grupo, além dos membros, se houver suporte para alguns aplicativos. Você pode habilitar ou desabilitar essa funcionalidade, habilitando ou desabilitando o **Mapeamento** para objetos de grupo mostrados na guia **Provisionamento**. 
>
>

Se o provisionamento de grupos é habilitado, certifique-se de rever os mapeamentos de atributos para garantir que um campo apropriado está sendo usado para a "ID correspondente". Essa ID correspondente pode ser o nome de exibição ou o alias do email. O grupo e seus membros não serão provisionados se a propriedade correspondente estiver vazia ou não for populada para um grupo no Microsoft Azure AD.

## <a name="next-steps"></a>Próximas etapas
[Automatizar o provisionamento e desprovisionamento de usuários para aplicativos SaaS com o Azure Active Directory](user-provisioning.md)
