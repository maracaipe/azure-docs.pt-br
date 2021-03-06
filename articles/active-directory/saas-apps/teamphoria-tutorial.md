---
title: 'Tutorial: Integração do Azure Active Directory ao Teamphoria | Microsoft Docs'
description: Saiba como configurar o logon único entre o Azure Active Directory e o Teamphoria.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: d569c705-6f0f-4ec1-b485-ba82526b5d32
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2018
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0f32a4ebd5a28c1054c19c578f3ba82e3b4951a9
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/13/2019
ms.locfileid: "56184101"
---
# <a name="tutorial-azure-active-directory-integration-with-teamphoria"></a>Tutorial: Integração do Azure Active Directory ao Teamphoria

Neste tutorial, você aprenderá a integrar o Teamphoria ao Azure AD (Azure Active Directory).

A integração do Teamphoria com o Azure AD oferece os seguintes benefícios:

- No Azure AD, é possível controlar quem tem acesso ao Teamphoria
- É possível permitir que seus usuários façam logon automaticamente no Teamphoria (logon único) com suas contas do Azure AD
- Você pode gerenciar suas contas em um único local: o portal do Azure

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD com o Teamphoria, você precisará dos seguintes itens:

- Uma assinatura do Azure AD
- Uma assinatura habilitada para logon único do Teamphoria

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.
 O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionar o Teamphoria da galeria
1. configurar e testar o logon único do AD do Azure

## <a name="adding-teamphoria-from-the-gallery"></a>Adicionar o Teamphoria da galeria
Para configurar a integração do Teamphoria com o Azure AD, você precisará adicionar o Teamphoria da galeria à sua lista de aplicativos SaaS gerenciados.

**Para adicionar o Teamphoria da galeria, realize as seguintes etapas:**

1. No **[portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone do **Azure Active Directory**.

    ![Active Directory][1]

1. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![APLICATIVOS][2]
    
1. Clique em **adicionar** botão na parte superior da caixa de diálogo.

    ![APLICATIVOS][3]

1. Na caixa de pesquisa, digite **Teamphoria**.

    ![Criação de um usuário de teste do AD do Azure](./media/teamphoria-tutorial/tutorial_teamphoria_search.png)

1. No painel de resultados, selecione **Teamphoria** e clique no botão **Adicionar** para adicionar o aplicativo.

    ![Criação de um usuário de teste do AD do Azure](./media/teamphoria-tutorial/tutorial_teamphoria_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Teamphoria, com base em um usuário de teste chamado “Brenda Fernandes”.

Para que o logon único funcione, o Azure AD precisa saber qual usuário do Teamphoria é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Teamphoria.

Para configurar e testar o logon único do Azure AD com o Teamphoria, você precisará concluir os seguintes blocos de construção:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - para habilitar seus usuários a usar esse recurso.
1. **[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** – para testar o logon único do AD do Azure com Brenda Fernandes.
1. **[Criação de um usuário de teste do Teamphoria](#creating-a-teamphoria-test-user)** – para ter um equivalente a Brenda Fernandes no Teamphoria que esteja vinculado à sua representação no Azure AD.
1. **[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do AD do Azure.
1. **[Teste do logon único](#testing-single-sign-on)** : para verificar se a configuração funciona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, você habilitará o logon único do Azure AD no portal do Azure e configurará o logon único no aplicativo Teamphoria.

**Para configurar o logon único do Azure AD com o Teamphoria, execute as seguintes etapas:**

1. No portal do Azure, na página de integração de aplicativos do **Teamphoria**, clique em **Logon único**.

    ![Configurar o logon único][4]

1. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.

    ![Configurar o logon único](./media/teamphoria-tutorial/tutorial_teamphoria_samlbase.png)

1. Na seção **URLs e Domínio do Teamphoria**, execute as seguintes etapas:

    ![Configurar o logon único](./media/teamphoria-tutorial/tutorial_teamphoria_url.png)

    Na caixa de texto **URL de Entrada**, digite a URL usando o seguinte padrão: `https://<sub-domain>.teamphoria.com/login`   

    > [!NOTE] 
    > O valor da URL de logon não é real. Você precisa atualizar esse valor com a URL de Entrada real. Entre em contato com a [Equipe de suporte do cliente do Teamphoria](https://www.teamphoria.com/) para obter a URL de Entrada.

1. Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o certificado em seu computador.

    ![Configurar o logon único](./media/teamphoria-tutorial/tutorial_teamphoria_certificate.png)

1. Clique no botão **Salvar** .

    ![Configurar o logon único](./media/teamphoria-tutorial/tutorial_general_400.png)

1. Na seção **Configuração do Teamphoria**, clique em **Configurar o Teamphoria** para abrir a janela **Configurar logon**. Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**

    ![Configurar o logon único](./media/teamphoria-tutorial/tutorial_teamphoria_configure.png)

1. Para configurar o logon único pelo **Teamphoria**, faça logon em seu aplicativo Teamphoria como administrador.

1. Vá até a opção **CONFIGURAÇÕES DE ADMINISTRAÇÃO** na barra de ferramentas à esquerda e, na guia Configurar, clique em **LOGON ÚNICO** para abrir a janela de configuração de SSO.

    ![Configurar o logon único](./media/teamphoria-tutorial/admin_sso_configure.png)

1. Clique na opção **ADICIONAR NOVO PROVEDOR DE IDENTIDADE** no canto superior direito para abrir o formulário para adicionar as configurações de SSO.

    ![Configurar o logon único](./media/teamphoria-tutorial/add_new_identity_provider.png)

1. Insira os detalhes nos campos conforme descrito abaixo:

    ![Configurar o logon único](./media/teamphoria-tutorial/Teamphoria_sso_save.png)

     a. **NOME DE EXIBIÇÃO**: insira o nome de exibição do plug-in na página de administração.

    b. **NOME DO BOTÃO**: o nome da guia que será exibida na página de logon para entrar usando SSO.

    c. **CERTIFICADO**: abra o certificado baixado anteriormente do portal do Azure no bloco de notas, copie o conteúdo e cole-o nesta caixa.

    d. **PONTO DE ENTRADA**: cole a **URL do Serviço de Logon Único SAML** copiada anteriormente do portal do Azure.

    e. Alterne a opção para **LIGADO** e clique em **SALVAR**.

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
O objetivo desta seção é criar um usuário de teste no portal do Azure chamado Brenda Fernandes.

![Criar um usuário do AD do Azure][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.

    ![Criação de um usuário de teste do AD do Azure](./media/teamphoria-tutorial/create_aaduser_01.png) 

1. Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.

    ![Criação de um usuário de teste do AD do Azure](./media/teamphoria-tutorial/create_aaduser_02.png) 

1. Na parte superior da caixa de diálogo clique **adicionar** para abrir o **usuário** caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/teamphoria-tutorial/create_aaduser_03.png)

1. Na página do diálogo **Usuário**, execute as seguintes etapas:
 
    ![Criação de um usuário de teste do AD do Azure](./media/teamphoria-tutorial/create_aaduser_04.png) 

    a. Na caixa de texto **Nome**, digite **Brenda Fernandes**.

    b. Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.

    c. Selecione **Mostrar senha** e anote o valor de **senha**.

    d. Clique em **Criar**.

### <a name="creating-a-teamphoria-test-user"></a>Criar um usuário de teste do Teamphoria

Para permitir que usuários do Azure AD façam logon no Teamphoria, eles deverão ser provisionados no Teamphoria. No caso do Teamphoria, o provisionamento é uma tarefa manual.

**Para provisionar uma conta de usuário, execute as seguintes etapas:**

1. Faça logon em seu site da empresa do Teamphoria como administrador.

1. Clique nas configurações de **ADMIN** na barra de ferramentas à esquerda e, na guia **GERENCIAR**, clique em **USUÁRIOS** para abrir a página de administração para usuários.

    ![Adicionar Funcionário](./media/teamphoria-tutorial/admin_manage_users.png)

1. Clique na opção **CONVITE MANUAL**.

    ![Convidar Pessoas](./media/teamphoria-tutorial/admin_manage_add_users.png)

1. Nessa página, realize a ação a seguir.
    
    ![Convidar Pessoas](./media/teamphoria-tutorial/manual_user_invite.png)

     a. Na caixa de texto **ENDEREÇO DE EMAIL**, digite o **endereço de email** de Brenda Fernandes.

    b. Na caixa de texto **NOME**, digite **Brenda**.

    c. Na caixa de texto **SOBRENOME**, digite **Fernandes**.

    d. Clique em **CONVIDAR 1 USUÁRIO**. O usuário deve aceitar o convite para ser criado no sistema.

### <a name="assigning-the-azure-ad-test-user"></a>Atribuição do usuário de teste do AD do Azure

Nesta seção, você habilitará Brenda Fernandes a usar o logon único do Azure concedendo a ela acesso ao Teamphoria.

![Atribuir usuário][200]

**Para atribuir Brenda Fernandes ao Teamphoria, execute as seguintes etapas:**

1. No portal do Azure, abra o modo de exibição de aplicativos e, em seguida, navegue até o modo de exibição de diretório e vá para **Aplicativos corporativos** e, em seguida, clique em **Todos os aplicativos**.

    ![Atribuir usuário][201]

1. Na lista de aplicativos, selecione **Teamphoria**.

    ![Configurar o logon único](./media/teamphoria-tutorial/tutorial_teamphoria_app.png) 

1. No menu à esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202]

1. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

1. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

1. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

1. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.

### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Se você quiser testar suas configurações de logon único, abra o Painel de Acesso. Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](../user-help/active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/teamphoria-tutorial/tutorial_general_01.png
[2]: ./media/teamphoria-tutorial/tutorial_general_02.png
[3]: ./media/teamphoria-tutorial/tutorial_general_03.png
[4]: ./media/teamphoria-tutorial/tutorial_general_04.png

[100]: ./media/teamphoria-tutorial/tutorial_general_100.png

[200]: ./media/teamphoria-tutorial/tutorial_general_200.png
[201]: ./media/teamphoria-tutorial/tutorial_general_201.png
[202]: ./media/teamphoria-tutorial/tutorial_general_202.png
[203]: ./media/teamphoria-tutorial/tutorial_general_203.png
