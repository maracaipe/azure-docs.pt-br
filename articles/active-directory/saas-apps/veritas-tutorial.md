---
title: 'Tutorial: Integração do Azure Active Directory com Veritas Enterprise Vault.cloud SSO | Microsoft Docs'
description: Saiba como configurar o logon único entre o Azure Active Directory e o Veritas Enterprise Vault.cloud SSO.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/31/2017
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 70adbcd8c25b3acb4408447070d3b0397d258847
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/13/2019
ms.locfileid: "56167449"
---
# <a name="tutorial-azure-active-directory-integration-with-veritas-enterprise-vaultcloud-sso"></a>Tutorial: Integração do Azure Active Directory com Veritas Enterprise Vault.cloud SSO

Neste tutorial, você aprenderá como integrar o Veritas Enterprise Vault.cloud SSO ao Azure AD (Azure Active Directory).

A integração do Veritas Enterprise Vault.cloud SSO ao Azure AD oferece os seguintes benefícios:

- Você pode controlar no Azure AD quem tem acesso ao Veritas Enterprise Vault.cloud SSO
- Você pode habilitar seus usuários a fazerem logon automaticamente no Veritas Enterprise Vault.cloud SSO (Logon Único) com suas contas do Azure AD
- Você pode gerenciar suas contas em um única localização: o Portal do Azure

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD com o Veritas Enterprise Vault.cloud SSO, você precisará dos seguintes itens:

- Uma assinatura do Azure AD
- Uma assinatura do Veritas Enterprise Vault.cloud SSO habilitada para logon único

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.  O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adição do Veritas Enterprise Vault.cloud SSO da galeria
1. configurar e testar o logon único do AD do Azure

## <a name="adding-veritas-enterprise-vaultcloud-sso-from-the-gallery"></a>Adição do Veritas Enterprise Vault.cloud SSO da galeria
Para configurar a integração do Veritas Enterprise Vault.cloud SSO ao Azure AD, você precisará adicionar o Veritas Enterprise Vault.cloud SSO da galeria à sua lista de aplicativos SaaS gerenciados.

**Para adicionar o Veritas Enterprise Vault.cloud SSO por meio da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![Active Directory][1]

1. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![APLICATIVOS][2]
    
1. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![APLICATIVOS][3]

1. Na caixa de pesquisa, digite **Veritas Enterprise Vault.cloud SSO**.

    ![Criação de um usuário de teste do AD do Azure](./media/veritas-tutorial/tutorial_veritas_search.png)

1. No painel de resultados, selecione **Veritas Enterprise Vault.cloud SSO** e clique no botão **Adicionar** para adicionar o aplicativo.

    ![Criação de um usuário de teste do AD do Azure](./media/veritas-tutorial/tutorial_veritas_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o Veritas Enterprise Vault.cloud SSO, com base em uma usuária de teste chamada “Brenda Fernandes”.

Para que o logon único funcione, o Azure AD precisa saber qual usuário do Veritas Enterprise Vault.cloud SSO é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Veritas Enterprise Vault.cloud SSO.

No Veritas Enterprise Vault.cloud SSO, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.

Para configurar e testar o logon único do Azure AD com o Veritas Enterprise Vault.cloud SSO, você precisa concluir os seguintes blocos de construção:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - para habilitar seus usuários a usar esse recurso.
1. **[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** – para testar o logon único do AD do Azure com Brenda Fernandes.
1. **[Criando um usuário de teste do Veritas Enterprise Vault.cloud SSO](#creating-a-veritas-enterprise-vaultcloud-sso-test-user)**: para ter um equivalente de Brenda Fernandes no Veritas Enterprise Vault.cloud SSO que esteja vinculado à representação do usuário no Azure AD.
1. **[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do AD do Azure.
1. **[Teste do logon único](#testing-single-sign-on)** : para verificar se a configuração funciona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, você habilitará o logon único do Azure AD no portal do Azure e configurará o logon único no aplicativo do Veritas Enterprise Vault.cloud SSO.

**Para configurar o logon único do Azure AD com o Veritas Enterprise Vault.cloud SSO, execute as seguintes etapas:**

1. No portal do Azure, na página de integração de aplicativos do **Veritas Enterprise Vault.cloud SSO**, clique em **Logon único**.

    ![Configurar o logon único][4]

1. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Configurar o logon único](./media/veritas-tutorial/tutorial_veritas_samlbase.png)

1. Na seção **URLs e Domínio do Veritas Enterprise Vault.cloud SSO**, execute as seguintes etapas:

    ![Configurar o logon único](./media/veritas-tutorial/tutorial_veritas_url.png)

    a. Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://personal.ap.archive.veritas.com/CID=<CUSTOMERID>`

    b. Na caixa de texto **Identificador**, use a URL de acordo com o datacenter

    | Datacenter| URL |
    |----------|----|
    | América do Norte| `https://auth.lax.archivecloud.net` |
    | Europa | `https://auth.ams.archivecloud.net` |
    | Pacífico Asiático| `https://auth.syd.archivecloud.net`|

    c. Na caixa de texto **URL de resposta**, use a URL de acordo com o datacenter

    | Datacenter| URL |
    |----------|----|
    | América do Norte| `https://auth.lax.archivecloud.net` |
    | Europa | `https://auth.ams.archivecloud.net` |
    | Pacífico Asiático| `https://auth.syd.archivecloud.net`|
    
    > [!NOTE] 
    > Esse valor não é real. Atualize esse valor com a URL de Logon real. Entre em contato com a [equipe de suporte do Cliente do Veritas Enterprise Vault.cloud SSO](https://www.veritas.com/support/.html) para obter esse valor. 

1. Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.

    ![Configurar o logon único](./media/veritas-tutorial/tutorial_veritas_certificate.png) 

1. Clique no botão **Salvar** .

    ![Configurar o logon único](./media/veritas-tutorial/tutorial_general_400.png)

1. Na seção **Configuração do Veritas Enterprise Vault.cloud SSO**, clique em **Configurar Veritas Enterprise Vault.cloud SSO** para abrir a janela **Configurar logon**. Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**

    ![Configurar o logon único](./media/veritas-tutorial/tutorial_veritas_configure.png) 

1. Para configurar o logon único no lado do **Veritas Enterprise Vault.cloud SSO**, é necessário enviar o **Certificado (Base64)** baixado e a **URL do Serviço de Logon Único SAML** para a [equipe de suporte do Veritas Enterprise Vault.cloud SSO](https://www.veritas.com/support/.html).

> [!TIP]
> É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!  Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior. Saiba mais sobre o recurso de documentação inserida aqui: [Documentação inserida do Microsoft Azure Active Directory]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

![Criar um usuário do AD do Azure][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.

    ![Criação de um usuário de teste do AD do Azure](./media/veritas-tutorial/create_aaduser_01.png) 

1. Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/veritas-tutorial/create_aaduser_02.png) 

1. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/veritas-tutorial/create_aaduser_03.png) 

1. Na página do diálogo **Usuário**, execute as seguintes etapas:
 
    ![Criação de um usuário de teste do AD do Azure](./media/veritas-tutorial/create_aaduser_04.png) 

    a. Na caixa de texto **Nome**, digite **Brenda Fernandes**.

    b. Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.

    c. Selecione **Mostrar senha** e anote o valor de **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-veritas-enterprise-vaultcloud-sso-test-user"></a>Criando um usuário de teste do Veritas Enterprise Vault.cloud SSO

Nesta seção, você criará uma usuária chamada Brenda Fernandes no Enterprise Vault.cloud SSO. Trabalhe com a  [equipe de suporte do Veritas Enterprise Vault.cloud SSO](https://www.veritas.com/support/.html)  para adicionar os usuários à plataforma do Enterprise Vault.cloud SSO. Os usuários devem ser criados e ativados antes de usar o logon único.

### <a name="assigning-the-azure-ad-test-user"></a>Atribuição do usuário de teste do AD do Azure

Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo acesso ao Veritas Enterprise Vault.cloud SSO.

![Atribuir usuário][200] 

**Para atribuir Brenda Fernandes ao Veritas Enterprise Vault.cloud SSO, execute as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

1. Na lista de aplicativos, selecione **Veritas Enterprise Vault.cloud SSO**.

    ![Configurar o logon único](./media/veritas-tutorial/tutorial_veritas_app.png) 

1. No menu à esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

1. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

1. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

1. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

1. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Ao clicar no bloco do Veritas Enterprise Vault.cloud SSO no Painel de Acesso, você deverá ser fazer logon automaticamente no aplicativo do Veritas Enterprise Vault.cloud SSO.

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/veritas-tutorial/tutorial_general_01.png
[2]: ./media/veritas-tutorial/tutorial_general_02.png
[3]: ./media/veritas-tutorial/tutorial_general_03.png
[4]: ./media/veritas-tutorial/tutorial_general_04.png

[100]: ./media/veritas-tutorial/tutorial_general_100.png

[200]: ./media/veritas-tutorial/tutorial_general_200.png
[201]: ./media/veritas-tutorial/tutorial_general_201.png
[202]: ./media/veritas-tutorial/tutorial_general_202.png
[203]: ./media/veritas-tutorial/tutorial_general_203.png

