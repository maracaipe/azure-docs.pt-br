---
title: 'Tutorial: Integração do Azure Active Directory ao Jostle | Microsoft Docs'
description: Saiba como configurar o logon único entre o Azure Active Directory e o Jostle.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: 9ca4ca1f-8f68-4225-81a6-1666b486d6a8
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 214cd2ac20207e32d862086f82f6e3c775d88721
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/13/2019
ms.locfileid: "56210434"
---
# <a name="tutorial-azure-active-directory-integration-with-jostle"></a>Tutorial: Integração do Azure Active Directory ao Jostle

Neste tutorial, você aprenderá a integrar o Jostle ao Azure AD (Azure Active Directory).

A integração do Jostle ao Azure AD oferece os seguintes benefícios:

- Você pode controlar no Azure AD quem terá acesso ao Jostle
- Você pode permitir que seus usuários faça logon automaticamente no Jostle (Logon Único) com suas contas do Azure AD
- Você pode gerenciar suas contas em um única localização: o Portal do Azure

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD ao Jostle, você precisará dos seguintes itens:

- Uma assinatura do Azure AD
- Uma assinatura habilitada para logon único do Jostle

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.
 O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adição do Jostle da galeria
1. configurar e testar o logon único do AD do Azure

## <a name="adding-jostle-from-the-gallery"></a>Adição do Jostle da galeria
Para configurar a integração do Jostle ao Azure AD, você precisará adicionar o Jostle da galeria à sua lista de aplicativos SaaS gerenciados.

**Para adicionar o Jostle por meio da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**.

    ![Active Directory][1]

1. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![APLICATIVOS][2]

1. Clique em **Adicionar** na parte superior da janela.

    ![add_01](./media/jostle-tutorial/add_01.png)

1. Na caixa de pesquisa em **Adicionar um aplicativo**, digite **Jostle**.

    ![add_02](./media/jostle-tutorial/add_02.png)

1. No painel de resultados, selecione **Jostle** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.

    ![Criação de um usuário de teste do AD do Azure](./media/jostle-tutorial/tutorial_jostle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Jostle, com base em um usuário de teste chamado “Brenda Fernandes”.

Para que o logon único funcione, o Azure AD precisa saber qual usuário do Jostle é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Jostle.

No Jostle, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.

Para configurar e testar o logon único do Azure AD com o Jostle, você precisa concluir os seguintes blocos de construção:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - para habilitar seus usuários a usar esse recurso.
1. **[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** – para testar o logon único do AD do Azure com Brenda Fernandes.
1. **[Criação de um usuário de teste do Jostle](#creating-a-jostle-test-user)**: para ter um equivalente de Brenda Fernandes no Jostle que esteja vinculado à representação do usuário no Azure AD.
1. **[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do AD do Azure.
1. **[Teste do logon único](#testing-single-sign-on)** : para verificar se a configuração funciona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Jostle.

**Para configurar o logon único do Azure AD com o Jostle, execute as seguintes etapas:**

1. No Portal do Azure, na página de integração de aplicativos do **Jostle**, clique em **Logon único**.

    ![Configurar o logon único][4]

1. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.

    ![Configurar o logon único](./media/jostle-tutorial/tutorial_jostle_samlbase.png)

1. Na seção **URLs e Domínio do Jostle**, execute as seguintes etapas:

    ![url_01](./media/jostle-tutorial/url_01.png)

     a. Na caixa de texto **URL de Logon**, insira: `https://login-prod.jostle.us`

    b. Na caixa de texto **Identificador**, insira: `https://jostle.us`

    c. Marque a caixa ao lado de **Mostrar configurações de URL avançadas**

    d. Na caixa de texto **URL de Resposta**, insira: `https://login-prod.jostle.us/saml/SSO/alias/newjostle.us`

1. Na seção **Atributos do Usuário**, no campo **Identificador do Usuário**, insira: `user.userprincipalname`

    ![url_02](./media/jostle-tutorial/url_02.png)

1. Clique em **Salvar** na parte superior da janela.

1. Acesse **Certificado de Autenticação SAML** e verifique se ele está definido como **Ativo**. Em seguida, clique em **XML de Metadados** para baixar o arquivo de metadados.

    ![url_03](./media/jostle-tutorial/url_03.png)

1. Para configurar o logon único no lado do Jostle, é necessário enviar o XML de metadados baixado para a [equipe de suporte do Jostle](mailto:support@jostle.me). Eles definem essa configuração para ter a conexão de SSO de SAML definida corretamente em ambos os lados.

> [!TIP]
> É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!  Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior. Saiba mais sobre o recurso de documentação inserida aqui: [Documentação inserida do Microsoft Azure Active Directory]( https://go.microsoft.com/fwlink/?linkid=845985)
>

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

![Criar um usuário do AD do Azure][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.

    ![Criação de um usuário de teste do AD do Azure](./media/jostle-tutorial/create_aaduser_01.png)

1. Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.

    ![Criação de um usuário de teste do AD do Azure](./media/jostle-tutorial/create_aaduser_02.png)

1. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.

    ![Criação de um usuário de teste do AD do Azure](./media/jostle-tutorial/create_aaduser_03.png)

1. Na página do diálogo **Usuário**, execute as seguintes etapas:

    ![Criação de um usuário de teste do AD do Azure](./media/jostle-tutorial/create_aaduser_04.png)

    a. Na caixa de texto **Nome**, digite **Brenda Fernandes**.

    b. Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.

    c. Selecione **Mostrar senha** e anote o valor de **senha**.

    d. Clique em **Criar**.

### <a name="creating-a-jostle-test-user"></a>Criação de um usuário de teste do Jostle

Nesta seção, você criará um usuário chamado Brenda Fernandes no Jostle. Se você não souber como adicionar Brenda Fernandes ao Jostle, entre em contato com a [equipe de suporte do Jostle](mailto:support@jostle.me) para adicionar o usuário de teste e habilitar o SSO.

> [!NOTE]
> O titular da conta do Azure Active Directory receberá um email e seguirá um link para confirmar a conta antes que ela se torne ativa.

### <a name="assigning-the-azure-ad-test-user"></a>Atribuição do usuário de teste do AD do Azure

Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure ao conceder acesso ao Jostle.

![Atribuir usuário][200]

**Para atribuir Brenda Fernandes ao Jostle, execute as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201]

1. Na lista de aplicativos, escolha **Jostle**.

    ![Configurar o logon único](./media/jostle-tutorial/tutorial_jostle_app.png)

1. No menu à esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202]

1. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

1. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

1. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

1. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.

### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Ao clicar no bloco Jostle no Painel de Acesso, você deverá ser conectado automaticamente à página de logon do aplicativo de Jostle.
Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](../user-help/active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/jostle-tutorial/tutorial_general_01.png
[2]: ./media/jostle-tutorial/tutorial_general_02.png
[3]: ./media/jostle-tutorial/tutorial_general_03.png
[4]: ./media/jostle-tutorial/tutorial_general_04.png

[100]: ./media/jostle-tutorial/tutorial_general_100.png

[200]: ./media/jostle-tutorial/tutorial_general_200.png
[201]: ./media/jostle-tutorial/tutorial_general_201.png
[202]: ./media/jostle-tutorial/tutorial_general_202.png
[203]: ./media/jostle-tutorial/tutorial_general_203.png
