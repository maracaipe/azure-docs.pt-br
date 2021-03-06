---
title: 'Tutorial: Integração do Azure Active Directory ao Perception United States (não UltiPro) | Microsoft Docs'
description: Saiba como configurar o logon único entre o Azure Active Directory e o Perception United States (não UltiPro).
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.reviewer: joflore
ms.assetid: b4a8f026-cb5f-41eb-9680-68eddc33565e
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: b9e208f899ff26135d3ce26bfa18096210513381
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/13/2019
ms.locfileid: "56192040"
---
# <a name="tutorial-azure-active-directory-integration-with-perception-united-states-non-ultipro"></a>Tutorial: Integração do Azure Active Directory ao Perception United States (não UltiPro)

Neste tutorial, você aprenderá a integrar o Perception United States (não UltiPro) ao Azure Active Directory (Azure AD).

A integração do Perception United States (não UltiPro) ao Azure AD oferece os seguintes benefícios:

- No Azure AD, você pode controlar quem tem acesso ao Perception United States (não UltiPro).
- Você pode permitir que seus usuários façam logon automaticamente no Perception United States (não UltiPro) (Logon Único) com suas contas do Azure AD.
- Você pode gerenciar suas contas em um único local central – o portal do Azure.

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD ao Perception United States (não UltiPro), você precisará dos seguintes itens:

- Uma assinatura do Azure AD
- Uma assinatura habilitada para logon único do Perception United States (não UltiPro)

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.  O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionar Perception United States (não UltiPro) pela galeria
1. configurar e testar o logon único do AD do Azure

## <a name="adding-perception-united-states-non-ultipro-from-the-gallery"></a>Adicionar Perception United States (não UltiPro) pela galeria
Para configurar a integração do Perception United States (não UltiPro) ao Azure AD, você precisará adicionar o Perception United States (não UltiPro) pela galeria à sua lista de aplicativos SaaS gerenciados.

**Para adicionar o Perception United States (não UltiPro) pela galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![O botão Azure Active Directory][1]

1. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![A folha Aplicativos empresariais][2]
    
1. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![O botão Novo aplicativo][3]

1. Na caixa de pesquisa, digite **Perception United States (não UltiPro)**, selecione **Perception United States (não UltiPro)** no painel de resultados e clique no botão **Adicionar** para adicionar o aplicativo.

    ![Perception United States (não UltiPro) na lista de resultados](./media/perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configura e testa o logon único do Azure AD com o Perception United States (não UltiPro) com base em uma usuária de teste chamada “Brenda Fernandes”.

Para que o logon único funcione, o Azure AD precisa saber qual usuário do Perception United States (não UltiPro) é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do Perception United States (não UltiPro).

No Perception United States (não UltiPro), atribua o valor do **nome de usuário** no Azure AD como o valor do **Nome de usuário** para estabelecer a relação de vínculo.

Para configurar e testar o logon único do Azure AD com o Perception United States (não UltiPro), você precisa concluir os seguintes blocos de construção:

1. **[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.
1. **[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.
1. **[Criar um usuário de teste do Perception United States (não UltiPro)](#create-a-perception-united-states-non-ultipro-test-user)** - para ter um equivalente de Brenda Fernandes no Perception United States (não UltiPro) que esteja vinculado à representação do usuário do Azure AD.
1. **[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.
1. **[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo Perception United States (não UltiPro).

**Para configurar o logon único do Azure AD com o Perception United States (não UltiPro), execute as seguintes etapas:**

1. No portal do Azure, na página de integração de aplicativos do **Perception United States (não UltiPro)**, clique em **Logon único**.

    ![Link Configurar logon único][4]

1. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Caixa de diálogo Logon único](./media/perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_samlbase.png)

1. Na seção **Domínio e URLs do Perception United States (não UltiPro)**, execute as seguintes etapas:

    ![Informações sobre logon único de domínio e URLs do Perception United States (não UltiPro)](./media/perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_url.png)

     a. Na caixa de texto **Identificador**, digite a URL: `https://perception.kanjoya.com/sp`

    b. Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://perception.kanjoya.com/sso?idp=<entity_id>`

    > [!NOTE] 
    > O valor não é real. Você atualizará o valor com a URL de Resposta real, que é explicada no tutorial posteriormente.
 
1. Na seção **Certificado de Autenticação SAML**, clique em **Metadados XML** e, em seguida, salve o arquivo de metadados em seu computador.

    ![O link de download do Certificado](./media/perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_certificate.png) 

1. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/perceptionunitedstates-tutorial/tutorial_general_400.png)

1. Na seção **Configuração do Perception United States (não UltiPro)**, clique em **Configurar Perception United States (não UltiPro)** para abrir a janela **Configurar logon**. Copie a **ID da Entidade SAML** da **seção Referência Rápida.**

     a. O aplicativo **Perception United States (não UltiPro)** exige que o valor da **ID da Entidade SAML**, que você copiou, seja codificado em URI. Para obter o valor codificado em URI, use o seguinte link:**http://www.url-encode-decode.com/**.

    b. Depois de obter o valor codificado em URI, combine-o com a **URL de resposta** conforme mencionado abaixo -

    `https://perception.kanjoya.com/sso?idp=<URI encooded entity_id>`
    
    c. Cole o valor acima na caixa de texto **URL de resposta** em na seção **Domínio e URLs do Perception United States (não UltiPro)**.

    ![Configuração do Perception United States (não UltiPro)](./media/perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_configure.png) 

1. Em outra janela do navegador, entre no seu site empresarial em Perception United States (não UltiPro) como administrador.

1. Na barra de ferramentas principal, clique em **Configurações de conta**.

    ![Usuário do Perception United States (não UltiPro)](./media/perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_user.png)

1. Na página **Configurações de conta**, execute as seguintes etapas:

    ![Usuário do Perception United States (não UltiPro)](./media/perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_account.png)

     a. Na caixa de texto **Nome da empresa**, digite o nome da **Empresa**.
    
    b. Na caixa de texto **Nome da conta**, digite o nome da **Conta**.

    c. Na caixa de texto **Email de resposta padrão**, digite um **Email** válido.

    d. Selecione **Provedor de identidade SSO** como **SAML 2.0**.

1. Na página **Configuração do SSO**, realize as seguintes etapas:

    ![SSOConfig do Perception United States (não UltiPro)](./media/perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_ssoconfig.png)

     a. Selecione **Tipo de SAML NameID** como **EMAIL**.

    b. Na caixa de texto **Nome da configuração de SSO**, digite o nome da sua **Configuração**.
    
    c. Na caixa de texto **Nome do Provedor de Identidade**, cole o valor da **ID de Entidade do SAML** que você copiou do Portal do Azure. 

    d. Na **caixa de texto Domínio de SAML**, digite o domínio como **@contoso.com**.

    e. Clique em **Carregar novamente** para carregar o arquivo **XML de metadados**.

    f. Clique em **Atualizar**.


> [!TIP]
> É possível ler uma versão concisa dessas instruções no [Portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo!  Depois de adicionar esse aplicativo da seção **Active Directory > Aplicativos Empresariais**, basta clicar na guia **Logon Único** e acessar a documentação inserida por meio da seção **Configuração** na parte inferior. Saiba mais sobre o recurso de documentação inserida aqui: [Documentação inserida do Microsoft Azure Active Directory]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

   ![Criar um usuário de teste do Azure AD][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.

    ![O botão Azure Active Directory](./media/perceptionunitedstates-tutorial/create_aaduser_01.png)

1. Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/perceptionunitedstates-tutorial/create_aaduser_02.png)

1. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.

    ![O botão Adicionar](./media/perceptionunitedstates-tutorial/create_aaduser_03.png)

1. Na caixa de diálogo **Usuário**, execute as seguintes etapas:

    ![A caixa de diálogo Usuário](./media/perceptionunitedstates-tutorial/create_aaduser_04.png)

    a. Na caixa **Nome**, digite **BrendaFernandes**.

    b. Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.

    c. Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.

    d. Clique em **Criar**.
  
### <a name="create-a-perception-united-states-non-ultipro-test-user"></a>Criar um usuário de teste do Perception United States (não UltiPro)

Nesta seção, você criará uma usuária chamada Brenda Fernandes no Perception United States (não UltiPro). Trabalhe com a [equipe de suporte do Perception United States (não UltiPro)](https://www.ultimatesoftware.com/Contact/ContactUs) para adicionar os usuários na plataforma do Perception United States (não UltiPro).

### <a name="assign-the-azure-ad-test-user"></a>Atribuir o usuário de teste do Azure AD

Nesta seção, você habilitará Brenda Fernandes a usar o logon único do Azure, concedendo acesso ao Perception United States (não UltiPro).

![Atribuir a função de usuário][200] 

**Para atribuir Brenda Fernandes ao Perception United States (não UltiPro), execute as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

1. Na lista de aplicativos, selecione **Perception United States (não UltiPro)**.

    ![O link do Perception United States (não UltiPro) na lista de aplicativos](./media/perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_app.png)  

1. No menu à esquerda, clique em **usuários e grupos**.

    ![O link “Usuários e grupos”][202]

1. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![O painel Adicionar Atribuição][203]

1. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

1. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

1. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Quando você clicar no bloco Perception United States (não UltiPro) no Painel de Acesso, deverá ser conectado automaticamente ao seu aplicativo Perception United States (não UltiPro).
Para saber mais sobre o Painel de Acesso, confira [Introdução ao Painel de Acesso](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/perceptionunitedstates-tutorial/tutorial_general_01.png
[2]: ./media/perceptionunitedstates-tutorial/tutorial_general_02.png
[3]: ./media/perceptionunitedstates-tutorial/tutorial_general_03.png
[4]: ./media/perceptionunitedstates-tutorial/tutorial_general_04.png

[100]: ./media/perceptionunitedstates-tutorial/tutorial_general_100.png

[200]: ./media/perceptionunitedstates-tutorial/tutorial_general_200.png
[201]: ./media/perceptionunitedstates-tutorial/tutorial_general_201.png
[202]: ./media/perceptionunitedstates-tutorial/tutorial_general_202.png
[203]: ./media/perceptionunitedstates-tutorial/tutorial_general_203.png

