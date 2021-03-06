---
title: 'Tutorial: Integração do Azure Active Directory com o Gra-Pe | Microsoft Docs'
description: Saiba como configurar o logon único entre o Azure Active Directory e o Gra-Pe.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 073f8641-b64d-4754-b1a6-2b91c865b13d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/15/2018
ms.author: jeedes
ms.openlocfilehash: 5e642cba3354f4f8589e44d975c0cecf5692c5b5
ms.sourcegitcommit: 707bb4016e365723bc4ce59f32f3713edd387b39
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2018
ms.locfileid: "49432202"
---
# <a name="tutorial-azure-active-directory-integration-with-gra-pe"></a>Tutorial: Integração do Azure Active Directory ao Gra-Pe

Neste tutorial, você aprende a integrar o Gra-Pe ao Azure AD (Azure Active Directory).

A integração do Gra-Pe ao Azure AD oferece os seguintes benefícios:

- Você pode controlar no Azure AD quem terá acesso ao Gra-Pe.
- Você pode permitir que seus usuários entrem automaticamente no Gra-Pe (Logon Único) com suas contas do Azure AD.
- Você pode gerenciar suas contas em um único local central – o portal do Azure.

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD ao Gra-Pe, você precisa dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada para logon único do Gra-Pe

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste. O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Como adicionar Gra-Pe da galeria
2. configurar e testar o logon único do AD do Azure

## <a name="adding-gra-pe-from-the-gallery"></a>Como adicionar Gra-Pe da galeria
Para configurar a integração do Gra-Pe ao Azure AD, é necessário adicionar o Gra-Pe à lista de aplicativos SaaS gerenciados por meio da galeria.

**Para adicionar o Gra-Pe da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![image](./media/grape-tutorial/selectazuread.png)

2. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![image](./media/grape-tutorial/a_select_app.png)
    
3. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![image](./media/grape-tutorial/a_new_app.png)

4. Na caixa de pesquisa, digite **Gra-Pe**, selecione **Gra-Pe** no painel de resultados e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.

     ![image](./media/grape-tutorial/tutorial_grape_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configura e testa o logon único do Azure AD com o Gra-Pe, com base em um usuário de teste chamado “Brenda Fernandes”.

Para que o logon único funcione, o Azure AD precisa saber qual usuário do Gra-Pe é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Gra-Pe.

Para configurar e testar o logon único do Azure AD com o Gra-Pe, você precisa concluir os seguintes blocos de construção:

1. **[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.
2. **[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.
3. **[Criar um usuário de teste do Gra-Pe](#create-a-gra-pe-test-user)** – para ter um equivalente de Brenda Fernandes no Gra-Pe que esteja vinculado à representação de usuário do Azure AD.
4. **[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.
5. **[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único no aplicativo Gra-Pe.

**Para configurar o logon único do Azure AD com o Gra-Pe, execute as seguintes etapas:**

1. No [Portal do Azure](https://portal.azure.com/), na página de integração d aplicativo **Gra-Pe**, selecione **Logon único**.

    ![image](./media/grape-tutorial/b1_b2_select_sso.png)

2. No diálogo **Selecionar um método de logon único**, clique em **Selecionar** do modo **SAML** para habilitar o logon único.

    ![image](./media/grape-tutorial/b1_b2_saml_sso.png)

3. Na página **Definir logon único com SAML**, clique no botão **Editar** para abrir a caixa de diálogo **Configuração básica de SAML**.

    ![image](./media/grape-tutorial/b1-domains_and_urlsedit.png)

4. Sobre o **básicas de configuração de SAML** , realize as seguintes etapas:

    Na caixa de texto **URL de logon**, digite uma URL como:  `https://btm.tts.co.jp/portal/apl/SSOLogin.aspx`

    ![image](./media/grape-tutorial/tutorial_grape_url.png)

5. Na página **Configurar logon único com SAML**, na seção **Certificado de assinatura SAML**, clique em **Download** para fazer o download do **Certificado (Base64)** e salve no seu computador.

    ![image](./media/grape-tutorial/tutorial_grape_certficate.png)

6. Na seção **Configurar o Gra-Pe**, copie a URL apropriada, de acordo com suas necessidades.

    a. URL de logon

    b. Identificador do Azure AD

    c. URL de logoff

    ![image](./media/grape-tutorial/d1_samlsonfigure.png) 

7. Para configurar o logon único no lado do **Gra-Pe**, você precisa enviar o **Certificado (Base64)** baixado e a **URL de logon, Identificador do Azure AD, URL de logout** para a [Equipe de suporte ao cliente do Gra-Pe](https://www.toppantravel.com/inquiry/). Eles definem essa configuração para ter a conexão de SSO de SAML definida corretamente em ambos os lados.

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

1. No Portal do Azure, no painel esquerdo, selecione **Azure Active Directory**, selecione **Usuários** e, em seguida, **Todos os usuários**.

    ![image](./media/grape-tutorial/d_users_and_groups.png)

2. Selecione **Novo usuário** na parte superior da tela.

    ![image](./media/grape-tutorial/d_adduser.png)

3. Nas Propriedades do usuário, execute as etapas a seguir.

    ![image](./media/grape-tutorial/d_userproperties.png)

    a. No campo **Nome**, insira **BrendaFernandes**.
  
    b. No campo **Nome de usuário**, digite **brittasimon@yourcompanydomain.extension**  
    Por exemplo, BrittaSimon@contoso.com

    c. Selecione **Propriedades**, marque a caixa de seleção **Mostrar senha** e, em seguida, anote o valor exibido na caixa Senha.

    d. Selecione **Criar**.
 
### <a name="create-a-gra-pe-test-user"></a>Criar um usuário de teste do Gra-Pe

Nesta seção, você criará um usuário chamado Britta Simon no Gra-Pe. Trabalhe com a [Equipe de suporte do Gra-Pe](https://www.toppantravel.com/inquiry/) para adicionar os usuários na plataforma Gra-Pe. Os usuários devem ser criados e ativados antes de usar o logon único.

### <a name="assign-the-azure-ad-test-user"></a>Atribuir o usuário de teste do Azure AD

Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Gra-Pe.

1. No Portal do Azure, selecione **Aplicativos Empresariais**, selecione **Todos os aplicativos**.

    ![image](./media/grape-tutorial/d_all_applications.png)

2. Na lista de aplicativos, selecione **Gra-Pe**.

    ![image](./media/grape-tutorial/tutorial_grape_app.png)

3. No menu à esquerda, selecione **Usuários e grupos**.

    ![image](./media/grape-tutorial/d_leftpaneusers.png)

4. Selecione o botão **Adicionar** e, em seguida, selecione **Usuários e grupos** no diálogo **Adicionar Atribuição**.

    ![image](./media/grape-tutorial/d_assign_user.png)

4. Na caixa de diálogo **Usuários e grupos**, selecione **Brenda Fernandes** na lista Usuários e clique no botão **Selecionar** na parte inferior da tela.

5. Na caixa de diálogo **Adicionar Atribuição** selecione o botão **Atribuir**.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Quando você clicar no bloco do Gra-Pe no Painel de Acesso, deverá fazer logon automaticamente em seu aplicativo do Gra-Pe.
Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](../active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)


