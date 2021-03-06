---
title: 'Tutorial: Integração do Azure Active Directory com o LogicMonitor | Microsoft Docs'
description: Saiba como configurar o logon único entre o Azure Active Directory e o LogicMonitor.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: 496156c3-0e22-4492-b36f-2c29c055e087
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2018
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: f3b6476fcedf849fb3305517ecfdcf29d07f545c
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/13/2019
ms.locfileid: "56181534"
---
# <a name="tutorial-azure-active-directory-integration-with-logicmonitor"></a>Tutorial: Integração do Azure Active Directory com o LogicMonitor

Neste tutorial, você aprenderá a integrar o LogicMonitor ao Azure AD (Azure Active Directory).

A integração do LogicMonitor ao Azure AD oferece os seguintes benefícios:

- Você pode controlar no Azure AD quem tem acesso ao LogicMonitor
- Você pode permitir que os usuários façam logon automaticamente no LogicMonitor (Logon Único) com suas contas do Azure AD
- Você pode gerenciar suas contas em um única localização: o Portal do Azure

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD ao LogicMonitor, você precisa dos seguintes itens:

- Uma assinatura do Azure AD
- Uma assinatura habilitada para logon único do LogicMonitor

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.  O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionar o LogicMonitor da galeria
1. configurar e testar o logon único do AD do Azure

## <a name="adding-logicmonitor-from-the-gallery"></a>Adicionar o LogicMonitor da galeria
Para configurar a integração do LogicMonitor ao Azure AD, você precisará adicionar o LogicMonitor da galeria à sua lista de aplicativos SaaS gerenciados.

**Para adicionar o LogicMonitor da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![Active Directory][1]

1. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![APLICATIVOS][2]
    
1. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![APLICATIVOS][3]

1. Na caixa de pesquisa, digite **LogicMonitor**.

    ![Criação de um usuário de teste do AD do Azure](./media/logicmonitor-tutorial/tutorial_logicmonitor_search.png)

1. No painel de resultados, selecione **LogicMonitor** e clique no botão **Adicionar** para adicionar o aplicativo.

    ![Criação de um usuário de teste do AD do Azure](./media/logicmonitor-tutorial/tutorial_logicmonitor_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>configurar e testar o logon único do AD do Azure
Nesta seção, você configurará e testará o logon único do Azure AD com o LogicMonitor, com base em um usuário de teste chamado “Brenda Fernandes”.

Para que o logon único funcione, o Azure AD precisa saber qual usuário do LogicMonitor é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do LogicMonitor.

No LogicMonitor, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.

Para configurar e testar o logon único do Azure AD com o LogicMonitor, você precisará concluir os seguintes blocos de construção:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - para habilitar seus usuários a usar esse recurso.
1. **[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** – para testar o logon único do AD do Azure com Brenda Fernandes.
1. **[Criação de um usuário de teste do LogicMonitor](#creating-a-logicmonitor-test-user)** – para ter um equivalente de Brenda Fernandes no LogicMonitor que esteja vinculado à representação do usuário no Azure AD.
1. **[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do AD do Azure.
1. **[Teste do logon único](#testing-single-sign-on)** : para verificar se a configuração funciona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo LogicMonitor.

**Para configurar o logon único do Azure AD com o LogicMonitor, execute as seguintes etapas:**

1. No portal do Azure, na página de integração de aplicativos do **LogicMonitor**, clique em **Logon único**.

    ![Configurar o logon único][4]

1. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Configurar o logon único](./media/logicmonitor-tutorial/tutorial_logicmonitor_samlbase.png)

1. Na seção **Domínio e URLs do LogicMonitor**, execute as seguintes etapas:

    ![Configurar o logon único](./media/logicmonitor-tutorial/tutorial_logicmonitor_url.png)

    a. Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<companyname>.logicmonitor.com`

    b. Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<companyname>.logicmonitor.com`

    > [!NOTE] 
    > Esses valores não são reais. Atualize esses valores com a URL de Entrada e o Identificador reais. Entre em contato com a [equipe de suporte do cliente do LogicMonitor](https://www.logicmonitor.com/contact/) para obter esses valores. 
 


1. Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.

    ![Configurar o logon único](./media/logicmonitor-tutorial/tutorial_logicmonitor_certificate.png) 

1. Clique no botão **Salvar** .

    ![Configurar o logon único](./media/logicmonitor-tutorial/tutorial_general_400.png)

1. Faça logon em seu site de empresa do **LogicMonitor** como administrador.

1. No menu na parte superior, clique em **Configurações**.
   
    ![Configurações](./media/logicmonitor-tutorial/ic790052.png "Configurações")

1. Na guia de navegação à esquerda, clique em **Logon Único**
   
    ![Logon Único](./media/logicmonitor-tutorial/ic790053.png "Logon Único")

1. Na seção **Configurações de SSO (logon único)** , realize as seguintes etapas:
   
    ![Configurações de Logon Único](./media/logicmonitor-tutorial/ic790054.png "Configurações de Logon Único")
   
     a. Selecione **Habilitar Logon Único**.

    b. Para **Atribuição de Função Padrão**, selecione **readonly**.
   
    c. Abra o arquivo de metadados baixado no bloco de notas e cole o conteúdo do arquivo na caixa de texto **Metadados do Provedor de Identidade** .
   
    d. Clique em **Salvar Alterações**.

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

![Criar um usuário do AD do Azure][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.

    ![Criação de um usuário de teste do AD do Azure](./media/logicmonitor-tutorial/create_aaduser_01.png) 

1. Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/logicmonitor-tutorial/create_aaduser_02.png) 

1. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/logicmonitor-tutorial/create_aaduser_03.png) 

1. Na página do diálogo **Usuário**, execute as seguintes etapas:
 
    ![Criação de um usuário de teste do AD do Azure](./media/logicmonitor-tutorial/create_aaduser_04.png) 

    a. Na caixa de texto **Nome**, digite **Brenda Fernandes**.

    b. Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.

    c. Selecione **Mostrar senha** e anote o valor de **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-logicmonitor-test-user"></a>Criar um usuário de teste do LogicMonitor

Para usuários do Microsoft Azure Active Directory conseguirem efetuar logon, eles devem ser provisionados para o aplicativo LogicMonitor usando seus nomes de usuário do Active Directory do Azure.

**Para configurar o provisionamento de usuários, execute as seguintes etapas:**

1. Faça logon no site da sua empresa LogicMonitor como um administrador.

1. No menu na parte superior, clique em **Configurações** e em **Funções e Usuários**.
   
    ![Funções e Usuários](./media/logicmonitor-tutorial/ic790056.png "Funções e Usuários")

1. Clique em **Adicionar**.

1. Na seção **Adicionar uma conta** , realize as seguintes etapas:
   
    ![Adicionar uma conta](./media/logicmonitor-tutorial/ic790057.png "Adicionar uma conta")
   
     a. Digite os valores para **Nome de usuário**, **Email**, **Senha** e **Digitar senha novamente** do usuário do Azure Active Directory que você deseja provisionar nas caixas de texto relacionadas.
   
    b. Selecione **Funções**, **Exibir Permissões** e **Status**.
   
    c. Clique em **Enviar**.

>[!NOTE]
>Você pode usar qualquer outra ferramenta de criação da conta de usuário do LogicMonitor ou APIs fornecidas pelo LogicMonitor para provisionar as contas de usuário do Active Directory do Azure. 

### <a name="assigning-the-azure-ad-test-user"></a>Atribuição do usuário de teste do AD do Azure

Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao LogicMonitor.

![Atribuir usuário][200] 

**Para atribuir Brenda Fernandes ao LogicMonitor, execute as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

1. Na lista de aplicativos, selecione **LogicMonitor**.

    ![Configurar o logon único](./media/logicmonitor-tutorial/tutorial_logicmonitor_app.png) 

1. No menu à esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

1. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

1. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

1. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

1. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.
 
Ao clicar no bloco do LogicMonitor no Painel de Acesso, você deverá ser conectado automaticamente ao seu aplicativo LogicMonitor.
Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](../active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/logicmonitor-tutorial/tutorial_general_01.png
[2]: ./media/logicmonitor-tutorial/tutorial_general_02.png
[3]: ./media/logicmonitor-tutorial/tutorial_general_03.png
[4]: ./media/logicmonitor-tutorial/tutorial_general_04.png

[100]: ./media/logicmonitor-tutorial/tutorial_general_100.png

[200]: ./media/logicmonitor-tutorial/tutorial_general_200.png
[201]: ./media/logicmonitor-tutorial/tutorial_general_201.png
[202]: ./media/logicmonitor-tutorial/tutorial_general_202.png
[203]: ./media/logicmonitor-tutorial/tutorial_general_203.png

