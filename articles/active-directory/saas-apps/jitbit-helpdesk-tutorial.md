---
title: 'Tutorial: Integração do Azure Active Directory com o Jitbit Helpdesk | Microsoft Docs'
description: Saiba como configurar o logon único entre o Azure Active Directory e o Jitbit Helpdesk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: 15ce27d4-0621-4103-8a34-e72c98d72ec3
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7cb752a6b598c9fe7f146cd6ce96182405fc0dc6
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/13/2019
ms.locfileid: "56167670"
---
# <a name="tutorial-azure-active-directory-integration-with-jitbit-helpdesk"></a>Tutorial: Integração do Azure Active Directory com o Jitbit Helpdesk

Neste tutorial, você aprenderá a integrar o Jitbit Helpdesk ao Azure AD (Azure Active Directory).

A integração do Jitbit Helpdesk ao Azure AD oferece os seguintes benefícios:

- No Azure AD, é possível controlar quem tem acesso ao Jitbit Helpdesk
- Você pode permitir que seus usuários façam logon automaticamente no Jitbit Helpdesk (Logon Único) com suas contas do Azure AD
- Você pode gerenciar suas contas em um única localização: o Portal do Azure

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD ao Jitbit Helpdesk, você precisará dos seguintes itens:

- Uma assinatura do Azure AD
- Uma assinatura habilitada para logon único do Jitbit Helpdesk

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.  O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionando Jitbit Helpdesk da galeria
1. configurar e testar o logon único do AD do Azure

## <a name="adding-jitbit-helpdesk-from-the-gallery"></a>Adicionando Jitbit Helpdesk da galeria
Para configurar a integração do Jitbit Helpdesk ao Azure AD, você precisará adicionar o Jitbit Helpdesk da galeria à sua lista de aplicativos SaaS gerenciados.

**Para adicionar o Jitbit Helpdesk por meio da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![Active Directory][1]

1. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![APLICATIVOS][2]
    
1. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![APLICATIVOS][3]

1. Na caixa de pesquisa, digite **Jitbit Helpdesk**.

    ![Criação de um usuário de teste do AD do Azure](./media/jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_search.png)

1. No painel de resultados, selecione **Jitbit Helpdesk** e clique no botão **Adicionar** para adicionar o aplicativo.

    ![Criação de um usuário de teste do AD do Azure](./media/jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>configurar e testar o logon único do AD do Azure
Nesta seção, você vai configurar e testar o logon único do Azure AD com o Jitbit Helpdesk, com base em um usuário de teste chamado "Brenda Fernandes".

Para que o logon único funcione, o Azure AD precisa saber qual usuário do Jitbit Helpdesk é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Jitbit Helpdesk.

No Jitbit Helpdesk, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.

Para configurar e testar o logon único do Azure AD com o Jitbit Helpdesk, você precisa concluir os seguintes blocos de construção:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - para habilitar seus usuários a usar esse recurso.
1. **[Criação de um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)** – para testar o logon único do AD do Azure com Brenda Fernandes.
1. **[Criação de um usuário de teste do Jitbit Helpdesk](#creating-a-jitbit-helpdesk-test-user)**: para ter um equivalente da Brenda Fernandes no Jitbit Helpdesk que está vinculado à representação do usuário no Azure AD.
1. **[Atribuição do usuário de teste do AD do Azure](#assigning-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do AD do Azure.
1. **[Teste do logon único](#testing-single-sign-on)** : para verificar se a configuração funciona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuração do logon único do Azure AD

Nesta seção, você habilita o logon único do Azure AD no Portal do Azure e configura o logon único em seu aplicativo Jitbit Helpdesk.

**Para configurar o logon único do Azure AD com o Jitbit Helpdesk, realize as seguintes etapas:**

1. No portal do Azure, na página de integração de aplicativos do **Jitbit Helpdesk**, clique em **Logon único**.

    ![Configurar o logon único][4]

1. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Configurar o logon único](./media/jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_samlbase.png)

1. Na seção **URLs e Domínio do Jitbit Helpdesk**, execute as seguintes etapas:

    ![Configurar o logon único](./media/jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_url.png)

     a. Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: 
    | |     
    | ----------------------------------------|
    | `https://<hostname>/helpdesk/User/Login`|
    | `https://<tenant-name>.Jitbit.com`|
    | |
    
    > [!NOTE] 
    > Esse valor não é real. Atualize esse valor com a URL de Logon real. Para obter esse valor, entre em contato com a [equipe de suporte do cliente Jitbit Helpdesk](https://www.jitbit.com/support/). 
    
    b.  Na caixa de texto **Identificador**, digite uma URL conforme a seguir: `https://www.jitbit.com/web-helpdesk/`

    
 


1. Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.

    ![Configurar o logon único](./media/jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_certificate.png) 

1. Clique no botão **Salvar** .

    ![Configurar o logon único](./media/jitbit-helpdesk-tutorial/tutorial_general_400.png)

1. Na seção **Configuração do Jitbit Helpdesk**, clique em **Configurar Jitbit Helpdesk** para abrir a janela **Configurar logon**. Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**

    ![Configurar o logon único](./media/jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_configure.png) 

1. Em uma janela diferente do navegador da Web, faça logon no site da sua empresa do Jitbit Helpdesk como administrador.

1. Na barra de ferramentas na parte superior, clique em **Administração**.
   
    ![Administração](./media/jitbit-helpdesk-tutorial/ic777681.png "Administração")

1. Clique em **Configurações gerais**.
   
    ![Usuários, empresas e permissões](./media/jitbit-helpdesk-tutorial/ic777680.png "Usuários, empresas e permissões")

1. Na seção de configuração **Configurações de autenticação** , realize as seguintes etapas:
   
    ![Configurações de autenticação](./media/jitbit-helpdesk-tutorial/ic777683.png "Configurações de autenticação")
    
     a. Selecione **Habilitar logon único SAML 2.0** para entrar usando SSO (Logon Único) com **OneLogin**.

    b. Na caixa de texto **URL do Ponto de Extremidade**, cole o valor da **URL de Serviço de Logon Único do SAML** que você copiou do Portal do Azure.

    c. Abra seu certificado codificado em **base 64** no bloco de notas, copie o conteúdo dele na área de transferência e cole-o na caixa de texto **Certificado X.509**

    d. Clique em **Salvar alterações**.

> [!TIP]
> É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!  Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior. Saiba mais sobre o recurso de documentação inserida aqui: [Documentação inserida do Microsoft Azure Active Directory]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Criação de um usuário de teste do AD do Azure
O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

![Criar um usuário do AD do Azure][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No **Portal do Azure**, no painel de navegação esquerdo, clique no ícone **Azure Active Directory**.

    ![Criação de um usuário de teste do AD do Azure](./media/jitbit-helpdesk-tutorial/create_aaduser_01.png) 

1. Vá para **Usuários e grupos** e clique em **Todos os usuários** para exibir a lista de usuários.
    
    ![Criação de um usuário de teste do AD do Azure](./media/jitbit-helpdesk-tutorial/create_aaduser_02.png) 

1. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo.
 
    ![Criação de um usuário de teste do AD do Azure](./media/jitbit-helpdesk-tutorial/create_aaduser_03.png) 

1. Na página do diálogo **Usuário**, execute as seguintes etapas:
 
    ![Criação de um usuário de teste do AD do Azure](./media/jitbit-helpdesk-tutorial/create_aaduser_04.png) 

     a. Na caixa de texto **Nome**, digite **BrendaFernandes**.

    b. Na caixa de texto **Nome de usuário**, digite o **endereço de email** da conta de Brenda Fernandes.

    c. Selecione **Mostrar senha** e anote o valor de **senha**.

    d. Clique em **Criar**.
 
### <a name="creating-a-jitbit-helpdesk-test-user"></a>Criação de um usuário de teste do Jitbit Helpdesk

Para permitir que os usuários do AD do Azure façam logon no Jitbit Helpdesk, eles devem ser provisionados no Helpdesk.  No caso do Jitbit Helpdesk, o provisionamento é uma tarefa manual.

**Para provisionar uma conta de usuário, execute as seguintes etapas:**

1. Faça logon em seu locatário do **Jitbit Helpdesk** .

1. No menu na parte superior, clique em **Administração**.
   
    ![Administração](./media/jitbit-helpdesk-tutorial/ic777681.png "Administração")

1. Clique em **Usuários, empresas e permissões**.
   
    ![Usuários, empresas e permissões](./media/jitbit-helpdesk-tutorial/ic777682.png "Usuários, empresas e permissões")

1. Clique em **Adicionar usuário**.
   
    ![Adicionar Usuário](./media/jitbit-helpdesk-tutorial/ic777685.png "Adicionar Usuário")
   
1. Na seção Criar, digite os dados da conta do Azure AD que deseja provisionar da seguinte maneira:

    ![Criar](./media/jitbit-helpdesk-tutorial/ic777686.png "Criar")
   
    a. Na caixa de texto **Nome de Usuário**, digite **BrendaFernandes**, o nome de usuário como no portal do Azure.

   b. Na caixa de texto **Email**, digite o email do usuário como **BrittaSimon@contoso.com**.

   c. Na caixa de texto **Nome**, digite o nome do usuário, como **Brenda**.

   d. Na caixa de texto **Sobrenome**, digite o sobrenome do usuário, como **Fernandes**.
   
   e. Clique em **Criar**.

>[!NOTE]
>É possível usar qualquer outra ferramenta de criação da conta de usuário do Jitbit Helpdesk ou APIs fornecidas pelo Jitbit Helpdesk para provisionar as contas de usuário do Azure AD.
> 
        

### <a name="assigning-the-azure-ad-test-user"></a>Atribuição do usuário de teste do AD do Azure

Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure ao conceder acesso ao Jitbit Helpdesk.

![Atribuir usuário][200] 

**Para atribuir Brenda Fernandes ao Jitbit Helpdesk, realize as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

1. Na lista de aplicativos, selecione **Jitbit Helpdesk**.

    ![Configurar o logon único](./media/jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_app.png) 

1. No menu à esquerda, clique em **usuários e grupos**.

    ![Atribuir usuário][202] 

1. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![Atribuir usuário][203]

1. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

1. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

1. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="testing-single-sign-on"></a>Teste do logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Ao clicar no bloco Jitbit Helpdesk no Painel de Acesso, você deve acessar a página de logon do aplicativo Jitbit Helpdesk.
Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](../user-help/active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/jitbit-helpdesk-tutorial/tutorial_general_01.png
[2]: ./media/jitbit-helpdesk-tutorial/tutorial_general_02.png
[3]: ./media/jitbit-helpdesk-tutorial/tutorial_general_03.png
[4]: ./media/jitbit-helpdesk-tutorial/tutorial_general_04.png

[100]: ./media/jitbit-helpdesk-tutorial/tutorial_general_100.png

[200]: ./media/jitbit-helpdesk-tutorial/tutorial_general_200.png
[201]: ./media/jitbit-helpdesk-tutorial/tutorial_general_201.png
[202]: ./media/jitbit-helpdesk-tutorial/tutorial_general_202.png
[203]: ./media/jitbit-helpdesk-tutorial/tutorial_general_203.png

