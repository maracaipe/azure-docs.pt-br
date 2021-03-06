---
title: 'Tutorial: integração do Azure Active Directory com o ThirdLight | Microsoft Docs'
description: Saiba como configurar o logon único entre o Azure Active Directory e o ThirdLight.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: 168aae9a-54ee-4c2b-ab12-650a2c62b901
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: f01c870316a4e7c9424bd63766fec0fed1dce7a3
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/13/2019
ms.locfileid: "56167177"
---
# <a name="tutorial-azure-active-directory-integration-with-thirdlight"></a>Tutorial: integração do Azure Active Directory com o ThirdLight

Neste tutorial, você aprenderá como integrar o ThirdLight com o Azure AD (Azure Active Directory).

A integração do ThirdLight com o Azure AD oferece os seguintes benefícios:

- No Azure AD, é possível controlar quem tem acesso ao ThirdLight
- Você pode habilitar os usuários a entrarem automaticamente no ThirdLight (Logon Único) com suas contas do Azure AD
- Você pode gerenciar suas contas em um única localização: o Portal do Azure

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao AD do Azure, consulte [O que é o acesso a aplicativos e logon único com o Active Directory do Azure](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD com o ThirdLight, você precisará dos seguintes itens:

- Uma assinatura do Azure AD
- Uma assinatura habilitada para logon único do ThirdLight

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.  O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionando o ThirdLight da Galeria
1. configurar e testar o logon único do AD do Azure

## <a name="adding-thirdlight-from-the-gallery"></a>Adicionando o ThirdLight da Galeria
Para configurar a integração do ThirdLight ao Azure AD, você precisará adicionar o ThirdLight da galeria à sua lista de aplicativos SaaS gerenciados.

**Para adicionar o ThirdLight da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![Active Directory][1]

1. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![APLICATIVOS][2]
    
1. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![APLICATIVOS][3]

1. Na caixa de pesquisa, digite **ThirdLight**.

    ![Criação de um usuário de teste do AD do Azure](./media/thirdlight-tutorial/tutorial_thirdlight_search.png)

1. No painel de resultados, selecione **ThirdLight** e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.

    ![Criação de um usuário de teste do AD do Azure](./media/thirdlight-tutorial/tutorial_thirdlight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o ThirdLight, com base em uma usuária de teste chamada "Brenda Fernandes".

Para que o logon único funcione, o Azure AD precisa saber qual usuário do ThirdLight é equivalente a um usuário no Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no ThirdLight.

Essa relação de vínculo é estabelecida por meio da atribuição do valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** no ThirdLight.

Para configurar e testar o logon único do Azure AD com o ThirdLight, você precisará concluir os seguintes blocos de construção:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - para habilitar seus usuários a usar esse recurso.
1. **[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** – para testar o logon único do AD do Azure com Brenda Fernandes.
1. **[Criação de um usuário de teste do ThirdLight](#creating-a-thirdlight-test-user)** – para ter um equivalente de Brenda Fernandes no ThirdLight que seja vinculado à representação de usuário do Azure AD.
1. **[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do AD do Azure.
1. **[Teste do logon único](#testing-single-sign-on)** : para verificar se a configuração funciona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único em seu aplicativo ThirdLight.

**Para configurar o logon único do Azure AD com o ThirdLight, realize as seguintes etapas:**

1. No Portal do Azure, na página de integração de aplicativos do **ThirdLight**, clique em **Logon único**.

    ![Configurar o logon único][4]

1. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Configurar o logon único](./media/thirdlight-tutorial/tutorial_thirdlight_samlbase.png)

1. Na seção **URLs e Domínio do ThirdLight**, realize as seguintes etapas:

    ![Configurar o logon único](./media/thirdlight-tutorial/tutorial_thirdlight_url.png)

    a. Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<subdomain>.thirdlight.com/`

    b. Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<subdomain>.thirdlight.com/saml/sp`

    > [!NOTE] 
    > Esses valores não são reais. Atualize esses valores com a URL de Entrada e o Identificador reais. Contate a [equipe de suporte ao cliente do ThirdLight](https://www.thirdlight.com/support) para obter esses valores. 
 
1. Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo XML em seu computador.

    ![Configurar o logon único](./media/thirdlight-tutorial/tutorial_thirdlight_certificate.png) 

1. Clique no botão **Salvar** .

    ![Configurar o logon único](./media/thirdlight-tutorial/tutorial_general_400.png)

1. Em outra janela do navegador da Web, faça logon em seu site de empresa ThirdLight como um administrador.

1. Vá para **Configuração \> Administração do Sistema** e clique em **SAML2**.
   
    ![Administração do Sistema](./media/thirdlight-tutorial/ic805843.png "Administração do Sistema")

1. Na seção de configuração do SAML2, execute as seguintes etapas:
   
    ![Logon Único do SAML](./media/thirdlight-tutorial/ic805844.png "Logon Único do SAML")   

      a. Selecione **Habilitar Logon Único do SAML2**.
 
     b. Como **Fonte de metadados do IdP**, selecione **Carregar Metadados do IdP do XML**.
 
     c. Abra o arquivo de metadados baixado, copie o conteúdo e cole-o na caixa de texto **XML de Metadados do IdP** . 
     
     d. Clique em **Salvar configurações do SAML2**.

> [!TIP]
> É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!  Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior. Saiba mais sobre o recurso de documentação inserida aqui: [Documentação inserida do Microsoft Azure Active Directory]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

![Criar um usuário do AD do Azure][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.

    ![Criação de um usuário de teste do AD do Azure](./media/thirdlight-tutorial/create_aaduser_01.png) 

1. Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/thirdlight-tutorial/create_aaduser_02.png) 

1. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/thirdlight-tutorial/create_aaduser_03.png) 

1. Na página do diálogo **Usuário**, execute as seguintes etapas:
 
    ![Criação de um usuário de teste do AD do Azure](./media/thirdlight-tutorial/create_aaduser_04.png) 

    a. Na caixa de texto **Nome**, digite **Brenda Fernandes**.

    b. Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.

    c. Selecione **Mostrar senha** e anote o valor de **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-thirdlight-test-user"></a>Criação de um usuário de teste do ThirdLight

Para permitir que os usuários do Azure AD façam logon no ThirdLight, eles devem ser provisionados no ThirdLight.  
No caso do ThirdLight, o provisionamento é uma tarefa manual.

**Para provisionar uma conta de usuário, execute as seguintes etapas:**

1. Faça logon em seu site de empresa do **ThirdLight** como um administrador.

1. Vá para a guia **Usuários** .

1. Selecione **Usuários e Grupos**.

1. Clique no botão **Adicionar novo Usuário** .

1. Digite os valores de **Nome de usuário, Nome ou Descrição, Email, Escolher uma Predefinição ou Grupo de Novos Membros** de uma conta válida do AAD que você deseja provisionar.

1. Clique em **Criar**.

>[!NOTE]
>É possível usar qualquer outra ferramenta de criação da conta de usuário do Thirdlight ou as APIs fornecidas pelo Thirdlight para provisionar as contas de usuário do AAD. 

### <a name="assigning-the-azure-ad-test-user"></a>Atribuição do usuário de teste do AD do Azure

Nesta seção, você habilita a Brenda Fernandes a usar o logon único do Azure através da concessão de acesso ao ThirdLight.

![Atribuir usuário][200] 

**Para atribuir Brenda Fernandes ao ThirdLight, realize as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

1. Na lista de aplicativos, selecione **ThirdLight**.

    ![Configurar o logon único](./media/thirdlight-tutorial/tutorial_thirdlight_app.png) 

1. No menu à esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

1. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

1. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

1. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

1. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Ao clicar no bloco ThirdLight no Painel de Acesso, você deve ser conectado automaticamente ao aplicativo ThirdLight.
Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/thirdlight-tutorial/tutorial_general_01.png
[2]: ./media/thirdlight-tutorial/tutorial_general_02.png
[3]: ./media/thirdlight-tutorial/tutorial_general_03.png
[4]: ./media/thirdlight-tutorial/tutorial_general_04.png

[100]: ./media/thirdlight-tutorial/tutorial_general_100.png

[200]: ./media/thirdlight-tutorial/tutorial_general_200.png
[201]: ./media/thirdlight-tutorial/tutorial_general_201.png
[202]: ./media/thirdlight-tutorial/tutorial_general_202.png
[203]: ./media/thirdlight-tutorial/tutorial_general_203.png

