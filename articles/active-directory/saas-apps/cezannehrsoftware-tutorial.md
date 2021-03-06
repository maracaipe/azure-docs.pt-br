---
title: 'Tutorial: Integração do Azure Active Directory ao software Cezanne HR | Microsoft Docs'
description: Saiba como configurar o logon único entre o Azure Active Directory e o Cezanne HR Software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.reviewer: joflore
ms.assetid: 62b42e15-c282-492d-823a-a7c1c539f2cc
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2017
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: fb6fb443440ce9af26a3152f7dcc536c4e881cd9
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/13/2019
ms.locfileid: "56165426"
---
# <a name="tutorial-azure-active-directory-integration-with-cezanne-hr-software"></a>Tutorial: Integração do Azure Active Directory ao software Cezanne HR

Neste tutorial, você aprende a integrar o Cezanne HR Software ao Azure AD (Azure Active Directory).

A integração do Cezanne HR Software ao Azure AD oferece os seguintes benefícios:

- Você pode controlar, no Azure Active Directory, quem tem acesso ao Cezanne HR Software.
- Você pode habilitar seus usuários a fazerem logon automaticamente no Cezanne HR Software (logon único) com suas contas do Azure Active Directory.
- Você pode gerenciar suas contas em um único local central – o portal do Azure.

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD com o Cezanne HR Software, você precisa dos seguintes itens:

- Uma assinatura do Azure AD
- Uma assinatura do Cezanne HR Software habilitada para logon único

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.  O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adição do Cezanne HR Software da galeria
1. configurar e testar o logon único do AD do Azure

## <a name="adding-cezanne-hr-software-from-the-gallery"></a>Adição do Cezanne HR Software da galeria
Para configurar a integração do Cezanne HR Software com o Azure AD, você precisa adicionar o Cezanne HR Software, por meio da galeria, à sua lista de aplicativos de SaaS gerenciados.

**Para adicionar o Cezanne HR Software por meio da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![O botão Azure Active Directory][1]

1. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![A folha Aplicativos empresariais][2]
    
1. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![O botão Novo aplicativo][3]

1. Na caixa de pesquisa, digite **Cezanne HR Software**, selecione **Cezanne HR Software** no painel de resultados e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.

    ![Software de RH Cezanne na lista de resultados](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configura e testa o logon único do Azure AD com o Cezanne HR Software, com base em um usuário de teste chamado “Brenda Fernandes”.

Para que o logon único funcione, o Azure AD precisa saber qual usuário do Cezanne HR Software é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Cezanne HR Software.

No Cezanne HR Software, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.

Para configurar e testar o logon único do Azure AD com o Cezanne HR Software, você precisa concluir os seguintes blocos de construção:

1. **[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.
1. **[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.
1. **Criar um usuário de teste do Cezanne HR Software** – para ter um equivalente de Brenda Fernandes no Cezanne HR Software que esteja vinculado à sua representação no Azure AD.
1. **[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.
1. **[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, você habilitará o logon único do Azure AD no portal do Azure e configurará o logon único em seu aplicativo Cezanne HR Software.

**Para configurar o logon único do Azure AD com o Cezanne HR Software, execute as seguintes etapas:**

1. No portal do Azure, na página de integração de aplicativo do **Cezanne HR Software**, clique em **Logon único**.

    ![Link Configurar logon único][4]

1. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Caixa de diálogo Logon único](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_samlbase.png)

1. Na seção **URLs e Domínio do Cezanne HR Software**, execute as seguintes etapas:

    ![Informações de logon único de Domínio e URLs do Cezanne HR Software](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_url.png)

     a. Na caixa de texto **URL de Logon**, digite a URL: `https://w3.cezanneondemand.com/CezanneOnDemand/-/<tenantidentifier>`

    b. Na caixa de texto **Identificador**, digite a URL: `https://w3.cezanneondemand.com/CezanneOnDemand/`

    c. Na caixa de texto **URL de Resposta**, digite a URL: `https://w3.cezanneondemand.com:443/cezanneondemand/-/<tenantidentifier>/Saml/samlp`
    
    > [!NOTE]
    > Esses valores não são reais. Atualize esses valores com a URL de Resposta e a URL de Logon reais. Para obter esses valores, entre em contato com a [equipe de suporte ao cliente do Cezanne HR Software](https://cezannehr.com/services/support/).

1. Na seção **Certificado de Autenticação do SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado no computador.

    ![O link de download do Certificado](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_certificate.png) 

1. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/cezannehrsoftware-tutorial/tutorial_general_400.png)

1. Na seção **Configuração do Cezanne HR Software**, clique em **Configurar o Cezanne HR Software** para abrir a janela **Configurar logon**.

    ![Configuração do Software Cezanne HR](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_configure.png)

1. Role para baixo até a seção **Referência rápida**. Copie a **URL do Serviço de Logon Único SAML e ID da Entidade SAML** da **seção de Referência Rápida.**

    ![Configuração do Software Cezanne HR](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_configure1.png)

1. Em uma janela diferente do navegador da Web, faça logon em seu locatário do Cezanne HR Software como um administrador.

1. No painel de navegação esquerdo, clique em **Configuração do Sistema**. Vá para **Configurações de Segurança**. Em seguida, navegue até **Configuração de Logon Único**.

    ![Configurar o logon único no lado do aplicativo](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_000.png)

1. No painel **Permitir que os usuários façam logon usando o SSO (Serviço de Logon Único)** a seguir, marque a caixa **SAML 2.0** e selecione a opção **Configuração Avançada**.

    ![Configurar o logon único no lado do aplicativo](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_001.png)

1. Clique no botão **Adicionar Novo** .

    ![Configurar o logon único no lado do aplicativo](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_002.png)

1. Execute as etapas a seguir na seção **PROVEDORES DE IDENTIDADE DO SAML 2.0** .

    ![Configurar o logon único no lado do aplicativo](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_003.png)
    
     a. Insira o nome do seu Provedor de Identidade como o **Nome de Exibição**.

    b. Na caixa de texto **Identificador de Entidade**, cole o valor da **ID da Entidade do SAML** que você copiou do portal do Azure. 

    c. Altere a **Associação SAML** para 'POST'.

    d. Na caixa de texto **Ponto de Extremidade do Serviço de Token de Segurança**, cole o valor da **URL do Serviço de Logon Único do SAML** que foi copiado do Portal do Azure.

    e. Na caixa de texto "Nome do atributo de ID de usuário", digite `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.
    
    f. Clique no ícone **Carregar** para carregar o certificado baixado do Portal do Azure.
    
    g. Clique no botão **Ok** . 

1. Clique no botão **Salvar** .

    ![Configurar o logon único no lado do aplicativo](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_004.png)

> [!TIP]
> É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!  Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior. Saiba mais sobre o recurso de documentação inserida aqui: [Documentação inserida do Microsoft Azure Active Directory]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

   ![Criar um usuário de teste do Azure AD][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.

    ![O botão Azure Active Directory](./media/cezannehrsoftware-tutorial/create_aaduser_01.png)

1. Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/cezannehrsoftware-tutorial/create_aaduser_02.png)

1. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.

    ![O botão Adicionar](./media/cezannehrsoftware-tutorial/create_aaduser_03.png)

1. Na caixa de diálogo **Usuário**, execute as seguintes etapas:

    ![A caixa de diálogo Usuário](./media/cezannehrsoftware-tutorial/create_aaduser_04.png)

    a. Na caixa **Nome**, digite **BrendaFernandes**.

    b. Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.

    c. Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.

    d. Clique em **Criar**.
 
### <a name="create-a-cezanne-hr-software-test-user"></a>Criar um usuário de teste do Cezanne HR Software

Para habilitar usuários do AD do Azure a fazer logon no Cezanne HR Software, eles devem ser provisionados no Cezanne HR Software. No caso do Cezanne HR Software, o provisionamento é uma tarefa manual.

**Para provisionar uma conta de usuário, execute as seguintes etapas:**

1.  Faça logon no site da empresa Cezanne HR Software como um administrador.

1.  No painel de navegação esquerdo, clique em **Configuração do Sistema**. Vá para **Gerenciar Usuários**. Em seguida, navegue até **Add New User**.

    ![Novo Usuário](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "Novo Usuário")

1.  Na seção **Person Details** , execute etapas abaixo:

    ![Novo Usuário](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "Novo Usuário")
    
     a. Defina **Internal User** como OFF.
    
    b. Na caixa de texto **Nome**, digite o Nome do usuário, como **Brenda**.  
 
    c. Na caixa de texto **Sobrenome**, digite o Sobrenome do usuário, como **Fernandes**.
    
    d. Na caixa de texto **Email**, digite o endereço de email do usuário, como Brittasimon@contoso.com.

1.  Na seção **Informações da Conta** , execute as etapas abaixo:

    ![Novo Usuário](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "Novo Usuário")
    
     a. Na caixa de texto **Nome de usuário**, digite o email do usuário, como Brittasimon@contoso.com.
    
    b. Na caixa de texto **Senha**, digite a senha do usuário.
    
    c. Selecione **Profissional de RH** como **Função de Segurança**.
    
    d. Clique em **OK**.

1. Navegue até a guia **Logon Único** e selecione **Adicionar Novo** na área **Identificadores SAML 2.0**.

    ![Usuário](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "Usuário")

1. Escolha o **Provedor de Identidade** para o Provedor de Identidade e, na caixa de texto de **Identificador do Usuário**, insira o endereço de email da conta de Brenda Fernandes.

    ![Usuário](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "Usuário")
    
1. Clique no botão **Salvar** .

    ![Usuário](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "Usuário")

### <a name="assign-the-azure-ad-test-user"></a>Atribuir o usuário de teste do Azure AD

Nesta seção, você permite que Brenda Fernandes use o logon único do Azure concedendo a ela acesso ao Cezanne HR Software.

![Atribuir a função de usuário][200] 

**Para atribuir Brenda Fernandes ao Cezanne HR Software, execute as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

1. Na lista de aplicativos, selecione **Cezanne HR Software**.

    ![O link Cezanne HR Software na lista de Aplicativos](./media/cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_app.png)  

1. No menu à esquerda, clique em **usuários e grupos**.

    ![O link “Usuários e grupos”][202]

1. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![O painel Adicionar Atribuição][203]

1. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

1. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

1. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Quando clicar no bloco Cezanne HR Software no Painel de Acesso, você deverá fazer logon automaticamente no seu aplicativo Cezanne HR Software.
Para saber mais sobre o Painel de Acesso, confira [Introdução ao Painel de Acesso](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/cezannehrsoftware-tutorial/tutorial_general_01.png
[2]: ./media/cezannehrsoftware-tutorial/tutorial_general_02.png
[3]: ./media/cezannehrsoftware-tutorial/tutorial_general_03.png
[4]: ./media/cezannehrsoftware-tutorial/tutorial_general_04.png

[100]: ./media/cezannehrsoftware-tutorial/tutorial_general_100.png

[200]: ./media/cezannehrsoftware-tutorial/tutorial_general_200.png
[201]: ./media/cezannehrsoftware-tutorial/tutorial_general_201.png
[202]: ./media/cezannehrsoftware-tutorial/tutorial_general_202.png
[203]: ./media/cezannehrsoftware-tutorial/tutorial_general_203.png

