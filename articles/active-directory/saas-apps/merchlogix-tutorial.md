---
title: 'Tutorial: integração do Azure Active Directory com o Merchlogix | Microsoft Docs'
description: Saiba como configurar o logon único entre o Azure Active Directory e o Merchlogix.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.reviewer: joflore
ms.assetid: a1f49bb8-6b17-433d-8f25-9d26fb390e77
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: d4c2ea78643b0efbea30746d60d4c988e2108b5f
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/13/2019
ms.locfileid: "56204909"
---
# <a name="tutorial-azure-active-directory-integration-with-merchlogix"></a>Tutorial: integração do Azure Active Directory com o Merchlogix

Neste tutorial, você aprenderá a integrar o Merchlogix ao Azure Active Directory (Azure AD).

A integração do Merchlogix ao Azure AD oferece os seguintes benefícios:

- No Azure AD, é possível controlar quem tem acesso ao Merchlogix.
- Você pode permitir que seus usuários façam logon automaticamente no Merchlogix (logon único) com as contas do Azure AD deles.
- Você pode gerenciar suas contas em um único local central – o portal do Azure.

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD com o Merchlogix, você precisará dos seguintes itens:

- Uma assinatura do Azure AD
- Assinatura habilitada para logon único do Merchlogix

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.  O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionando Merchlogix a partir da galeria
1. configurar e testar o logon único do AD do Azure

## <a name="adding-merchlogix-from-the-gallery"></a>Adicionando Merchlogix a partir da galeria
Para configurar a integração do Merchlogix ao Azure AD, você precisará adicionar o Merchlogix a partir da galeria à sua lista de aplicativos SaaS gerenciados.

**Para adicionar o Merchlogix a partir da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![O botão Azure Active Directory][1]

1. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![A folha Aplicativos empresariais][2]
    
1. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![O botão Novo aplicativo][3]

1. Na caixa de pesquisa, digite **Merchlogix**, selecione **Merchlogix** no painel de resultados e, depois, clique no botão **Adicionar** para adicionar o aplicativo.

    ![Merchlogix na lista de resultados](./media/merchlogix-tutorial/tutorial_merchlogix_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configurará e testará o logon único do Azure AD com o Merchlogix, com base em um usuário de teste chamado “Brenda Fernandes”.

Para que o logon único funcione, o Azure AD precisa saber qual usuário do Merchlogix é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Merchlogix.

No Merchlogix, atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.

Para configurar e testar o logon único do Azure AD com o Merchlogix, você precisa concluir os seguintes blocos de construção:

1. **[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.
1. **[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.
1. **[Criar um usuário de teste do Merchlogix](#create-a-merchlogix-test-user)** – para ter um equivalente de Brenda Fernandes no Merchlogix que esteja vinculado à representação de usuário do Azure AD.
1. **[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.
1. **[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, você habilita o logon único do Azure AD no portal do Azure e configura o logon único no aplicativo Merchlogix.

**Para configurar o logon único do Azure AD com o Merchlogix, execute as seguintes etapas:**

1. No portal do Azure, na página de integração de aplicativos do **Merchlogix**, clique em **Logon único**.

    ![Link Configurar logon único][4]

1. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Caixa de diálogo Logon único](./media/merchlogix-tutorial/tutorial_merchlogix_samlbase.png)

1. Na seção **URLs e Domínio do Merchlogix**, execute as seguintes etapas:

    ![Informações de logon único em Domínio e URLs do Merchlogix](./media/merchlogix-tutorial/tutorial_merchlogix_url.png)

     a. Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<DOMAIN>/login.php?saml=true`

    b. Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<DOMAIN>/simplesaml/module.php/saml/sp/metadata.php/<SAML_NAME>`
    
    > [!NOTE]
    > Esses valores não são reais. Atualize esses valores com a URL de Entrada e o Identificador reais. Entre em contato com a [equipe de suporte do Merchlogix](https://www.merchlogix.com/contact/) para obter esses valores.

1. Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.

    ![O link de download do Certificado](./media/merchlogix-tutorial/tutorial_merchlogix_certificate.png) 

1. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/merchlogix-tutorial/tutorial_general_400.png)

1. Na seção **Configuração do Merchlogix**, clique em **Configurar o Merchlogix** para abrir a janela **Configurar logon**. Copie a **URL de Saída, a ID da Entidade SAML** e a **URL do Serviço de Logon Único SAML** da **seção Referência Rápida**.

    ![Configuração do Merchlogix](./media/merchlogix-tutorial/tutorial_merchlogix_configure.png) 

1. Para configurar o logon único no lado do **Merchlogix**, é necessário enviar o **Certificado (Base64)** baixado, a **URL de Saída, a ID da Entidade SAML e a URL do Serviço de Logon Único do SAML** para a [equipe de suporte do Merchlogix](https://www.merchlogix.com/contact/). Eles definem essa configuração para ter a conexão de SSO de SAML definida corretamente em ambos os lados.

> [!TIP]
> É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!  Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior. Saiba mais sobre o recurso de documentação inserida aqui: [Documentação inserida do Microsoft Azure Active Directory]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

   ![Criar um usuário de teste do Azure AD][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.

    ![O botão Azure Active Directory](./media/merchlogix-tutorial/create_aaduser_01.png)

1. Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/merchlogix-tutorial/create_aaduser_02.png)

1. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.

    ![O botão Adicionar](./media/merchlogix-tutorial/create_aaduser_03.png)

1. Na caixa de diálogo **Usuário**, execute as seguintes etapas:

    ![A caixa de diálogo Usuário](./media/merchlogix-tutorial/create_aaduser_04.png)

    a. Na caixa **Nome**, digite **BrendaFernandes**.

    b. Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.

    c. Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.

    d. Clique em **Criar**.
 
### <a name="create-a-merchlogix-test-user"></a>Criar um usuário de teste do Merchlogix

Nesta seção, você criará um usuário chamado Brenda Fernandes no Merchlogix. Trabalhe com a [equipe de suporte do Merchlogix](https://www.merchlogix.com/contact/) para adicionar os usuários na plataforma do Merchlogix.

### <a name="assign-the-azure-ad-test-user"></a>Atribuir o usuário de teste do Azure AD

Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Merchlogix.

![Atribuir a função de usuário][200] 

**Para atribuir Brenda Fernandes ao Merchlogix, execute as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

1. Na lista de aplicativos, escolha **Merchlogix**.

    ![O link do Merchlogix na lista de Aplicativos](./media/merchlogix-tutorial/tutorial_merchlogix_app.png)  

1. No menu à esquerda, clique em **usuários e grupos**.

    ![O link “Usuários e grupos”][202]

1. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![O painel Adicionar Atribuição][203]

1. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

1. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

1. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Quando você clica no bloco Merchlogix no Painel de Acesso, deve fazer logon automaticamente no seu aplicativo do Merchlogix.
Para saber mais sobre o Painel de Acesso, confira [Introdução ao Painel de Acesso](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/merchlogix-tutorial/tutorial_general_01.png
[2]: ./media/merchlogix-tutorial/tutorial_general_02.png
[3]: ./media/merchlogix-tutorial/tutorial_general_03.png
[4]: ./media/merchlogix-tutorial/tutorial_general_04.png

[100]: ./media/merchlogix-tutorial/tutorial_general_100.png

[200]: ./media/merchlogix-tutorial/tutorial_general_200.png
[201]: ./media/merchlogix-tutorial/tutorial_general_201.png
[202]: ./media/merchlogix-tutorial/tutorial_general_202.png
[203]: ./media/merchlogix-tutorial/tutorial_general_203.png

