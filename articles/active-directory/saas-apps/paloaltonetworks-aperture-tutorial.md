---
title: 'Tutorial: Integração do Microsoft Azure Active Directory à Palo Alto Networks – Aperture | Microsoft Docs'
description: Saiba como configurar o logon único entre o Azure Active Directory e o Palo Alto Networks – Aperture.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a5ea18d3-3aaf-4bc6-957c-783e9371d0f1
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2018
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 61603ad5920b6242c3e36429173744125b9eb59e
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/13/2019
ms.locfileid: "56206729"
---
# <a name="tutorial-azure-active-directory-integration-with-palo-alto-networks---aperture"></a>Tutorial: Integração do Microsoft Azure Active Directory à Palo Alto Networks – Aperture

Neste tutorial, você aprenderá a integrar o Palo Alto Networks – Aperture ao Microsoft Azure AD.

A integração do Palo Alto Networks – Aperture ao Microsoft Azure AD oferece os seguintes benefícios:

- No Microsoft Azure AD, é possível controlar quem tem acesso ao Palo Alto Networks – Aperture.
- Você pode permitir que os usuários façam logon automaticamente no Palo Alto Networks – Aperture (logon único) com as respectivas contas do Microsoft Azure AD.
- Você pode gerenciar suas contas em um único local central – o portal do Azure.

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure Active Directory com o Palo Alto Networks – Aperture, os seguintes itens serão necessários:

- Uma assinatura do Azure AD
- Uma assinatura do Palo Alto Networks – Aperture habilitada para logon único

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.  O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionar o Palo Alto Networks – Aperture da galeria
1. configurar e testar o logon único do AD do Azure

## <a name="adding-palo-alto-networks---aperture-from-the-gallery"></a>Adicionar o Palo Alto Networks – Aperture da galeria
Para configurar a integração do Palo Alto Networks – Aperture com o Azure Active Directory, você precisará adicionar o Palo Alto Networks – Aperture da galeria à sua lista de aplicativos SaaS gerenciados.

**Para adicionar o Palo Alto Networks - Aperture da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![O botão Azure Active Directory][1]

1. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![A folha Aplicativos empresariais][2]
    
1. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![O botão Novo aplicativo][3]

1. Na caixa de pesquisa, digite **Palo Alto Networks – Aperture**, selecione **Palo Alto Networks – Aperture** no painel de resultados e clique no botão **Adicionar** para adicionar o aplicativo.

    ![Palo Alto Networks - Aperture na lista de resultados](./media/paloaltonetworks-aperture-tutorial/tutorial_paloaltonetwork_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configurará e testará o logon único do Azure Active Directory com o Palo Alto Networks – Aperture, com base em uma usuária de teste chamada "Brenda Fernandes".

Para que o logon único funcione, o Azure Active Directory precisa saber qual usuário no Palo Alto Networks – Aperture é equivalente a um usuário do Azure Active Directory. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure Active Directory e o usuário relacionado do Palo Alto Networks – Aperture.

Para configurar e testar o logon único do Azure Active Directory com o Palo Alto Networks – Aperture, você precisará concluir os seguintes blocos de construção:

1. **[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.
1. **[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.
1. **[Criar um usuário de teste do Palo Alto Networks – Aperture](#create-a-palo-alto-networks---aperture-test-user)** – para ter um equivalente de Brenda Fernandes no Palo Alto Networks – Aperture vinculado à representação do usuário no Azure Active Directory.
1. **[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.
1. **[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, você habilitará o logon único do Azure Active Directory no Portal do Azure e configurará o logon único no aplicativo Palo Alto Networks – Aperture.

**Para configurar o logon único do Azure Active Directory com o Palo Alto Networks – Aperture, execute as seguintes etapas:**

1. No Portal do Azure, na página de integração de aplicativo **Palo Alto Networks – Aperture**, clique em **Logon Único**.

    ![Link Configurar logon único][4]

1. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Caixa de diálogo Logon único](./media/paloaltonetworks-aperture-tutorial/tutorial_paloaltonetwork_samlbase.png)

1. Na seção **Domínio e URLs do Palo Alto Networks - Aperture**, execute as seguintes etapas se desejar configurar o aplicativo no modo iniciado pelo **IDP**:

    ![Informações de logon único de Domínio e URLs do Palo Alto Networks – Aperture](./media/paloaltonetworks-aperture-tutorial/tutorial_paloaltonetwork_url.png)

     a. Na caixa de texto **Identificador**, digite uma URL usando o seguinte padrão: `https://<subdomain>.aperture.paloaltonetworks.com/d/users/saml/metadata`

    b. Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://<subdomain>.aperture.paloaltonetworks.com/d/users/saml/auth`

1. Marque **Mostrar configurações avançadas de URL** e realize a seguinte etapa se quiser configurar o aplicativo no modo iniciado pelo **SP**:

    ![Informações de logon único de Domínio e URLs do Palo Alto Networks – Aperture](./media/paloaltonetworks-aperture-tutorial/tutorial_paloaltonetwork_url1.png)

    Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://<subdomain>.aperture.paloaltonetworks.com/d/users/saml/sign_in`
     
    > [!NOTE] 
    > Esses valores não são reais. Atualize esses valores com o Identificador real, a URL de Resposta e a URL de Entrada. Entre em contato com a [equipe de suporte ao cliente do Palo Alto Networks – Aperture](https://live.paloaltonetworks.com/t5/custom/page/page-id/Support) para obter esses valores. 

1. Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.

    ![O link de download do Certificado](./media/paloaltonetworks-aperture-tutorial/tutorial_paloaltonetwork_certificate.png) 

1. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/paloaltonetworks-aperture-tutorial/tutorial_general_400.png)


1. Na seção **Configuração do Palo Alto Networks - Aperture**, clique em **Configure Palo Alto Networks - Aperture** para abrir a janela **Configurar logon**. Copie a **ID da Entidade SAML e a URL do Serviço de Logon Único SAML** da **seção Referência Rápida.**

    ![Link de configuração](./media/paloaltonetworks-aperture-tutorial/tutorial_paloaltonetwork_configure.png)

1. Em outra janela do navegador da Web, entre no Palo Alto Networks - Aperture como Administrador.

1. Na barra de menu superior, clique em **CONFIGURAÇÕES**.

    ![Guia de configurações](./media/paloaltonetworks-aperture-tutorial/tutorial_paloaltonetwork_settings.png)

1. Navegue para a seção **APLICAÇÃO** e clique em **Autenticação** no lado esquerdo do menu.

    ![Guia de Autenticação](./media/paloaltonetworks-aperture-tutorial/tutorial_paloaltonetwork_auth.png)
    
1. Na página **Autenticação**, execute as seguintes etapas:
    
    ![Guia de autenticação](./media/paloaltonetworks-aperture-tutorial/tutorial_paloaltonetwork_singlesignon.png)

     a. Verifique **Habilitar Logon Único (Provedores SSP com suporte são Okta, Onelogin)** do campo **Logon Único**.

    b. Na caixa de texto **ID do Provedor de Identidade**, cole o valor da **ID da Identidade SAML**, que você copiou do Portal do Azure.

    c. Clique em **Escolher Arquivo** para fazer upload do Certificado baixado do Azure Active Directory no campo **Certificado do Provedor de Identidade**.

    d. Na caixa de texto **URL do SSO do Provedor de Identidade**, cole o valor da **URL de Serviço de Logon Único do SAML** que você copiou do Portal do Azure.

    e. Analise as informações IdP na seção **Aperture Info** e baixe o certificado do campo **Aperture Key**.

    f. Clique em **Salvar**.

> [!TIP]
> É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!  Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior. Saiba mais sobre o recurso de documentação inserida aqui: [Documentação inserida do Microsoft Azure Active Directory]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

   ![Criar um usuário de teste do Azure AD][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.

    ![O botão Azure Active Directory](./media/paloaltonetworks-aperture-tutorial/create_aaduser_01.png)

1. Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/paloaltonetworks-aperture-tutorial/create_aaduser_02.png)

1. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.

    ![O botão Adicionar](./media/paloaltonetworks-aperture-tutorial/create_aaduser_03.png)

1. Na caixa de diálogo **Usuário**, execute as seguintes etapas:

    ![A caixa de diálogo Usuário](./media/paloaltonetworks-aperture-tutorial/create_aaduser_04.png)

    a. Na caixa **Nome**, digite **BrendaFernandes**.

    b. Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.

    c. Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.

    d. Clique em **Criar**.
 
### <a name="create-a-palo-alto-networks---aperture-test-user"></a>Criar um usuário de teste do Palo Alto Networks - Aperture

Nesta seção, você criará uma usuária chamada Brenda Fernandes no Palo Alto Networks - Aperture. Trabalhe com a [equipe de suporte ao cliente da Palo Alto Networks – Aperture](https://live.paloaltonetworks.com/t5/custom/page/page-id/Support) para adicionar os usuários à plataforma da Palo Alto Networks – Aperture. Os usuários devem ser criados e ativados antes de usar o logon único. 

### <a name="assign-the-azure-ad-test-user"></a>Atribuir o usuário de teste do Azure AD

Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Palo Alto Networks – Aperture.

![Atribuir a função de usuário][200] 

**Para atribuir Brenda Fernandes ao Palo Alto Networks – Aperture, execute as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

1. Na lista de aplicativos, selecione **Palo Alto Networks – Aperture**.

    ![O link Palo Alto Networks – Aperture na lista de Aplicativos](./media/paloaltonetworks-aperture-tutorial/tutorial_paloaltonetwork_app.png)  

1. No menu à esquerda, clique em **usuários e grupos**.

    ![O link “Usuários e grupos”][202]

1. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![O painel Adicionar Atribuição][203]

1. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

1. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

1. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Quando você clica no bloco Palo Alto Networks – Aperture no painel de acesso, seu logon deve ser realizado automaticamente no seu aplicativo Palo Alto Networks – Aperture.
Para saber mais sobre o Painel de Acesso, confira [Introdução ao Painel de Acesso](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/paloaltonetworks-aperture-tutorial/tutorial_general_01.png
[2]: ./media/paloaltonetworks-aperture-tutorial/tutorial_general_02.png
[3]: ./media/paloaltonetworks-aperture-tutorial/tutorial_general_03.png
[4]: ./media/paloaltonetworks-aperture-tutorial/tutorial_general_04.png

[100]: ./media/paloaltonetworks-aperture-tutorial/tutorial_general_100.png

[200]: ./media/paloaltonetworks-aperture-tutorial/tutorial_general_200.png
[201]: ./media/paloaltonetworks-aperture-tutorial/tutorial_general_201.png
[202]: ./media/paloaltonetworks-aperture-tutorial/tutorial_general_202.png
[203]: ./media/paloaltonetworks-aperture-tutorial/tutorial_general_203.png

