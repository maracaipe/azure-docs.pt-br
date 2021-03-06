---
title: 'Tutorial: Integração do Azure Active Directory com o Leapsome | Microsoft Docs'
description: Saiba como configurar o logon único entre o Active Directory do Azure e o Leapsome.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: cb523e97-add8-4289-b106-927bf1a02188
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2018
ms.author: jeedes
ms.openlocfilehash: 898d7cf6cdded08cd09c4b1f1f845473af1650a3
ms.sourcegitcommit: 8899e76afb51f0d507c4f786f28eb46ada060b8d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51823989"
---
# <a name="tutorial-azure-active-directory-integration-with-leapsome"></a>Tutorial: Integração do Azure Active Directory com o Leapsome

Neste tutorial, você aprenderá a integrar o Leapsome ao Azure AD (Azure Active Directory).

A integração do Leapsome ao Azure AD oferece os seguintes benefícios:

- Você pode controlar no Azure AD quem tem acesso ao Leapsome.
- Você pode permitir que seus usuários façam logon automaticamente em Leapsome (logon único) com as contas do Azure AD.
- Você pode gerenciar suas contas em um único local central – o portal do Azure.

Para conhecer mais detalhadamente a integração de aplicativos de SaaS ao Azure AD, consulte [o que é o acesso a aplicativos e logon único com o Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Pré-requisitos

Para configurar a integração do Azure AD ao Leapsome, você precisará dos seguintes itens:

- Uma assinatura do AD do Azure
- Uma assinatura habilitada Leapsome para logon único

> [!NOTE]
> Para testar as etapas deste tutorial, nós não recomendamos o uso de um ambiente de produção.

Para testar as etapas deste tutorial, você deve seguir estas recomendações:

- Não use o ambiente de produção, a menos que seja necessário.
- Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrição do cenário
Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.  O cenário descrito neste tutorial consiste em dois blocos de construção principais:

1. Adicionando o Leapsome da galeria
1. configurar e testar o logon único do AD do Azure

## <a name="adding-leapsome-from-the-gallery"></a>Adicionando o Leapsome da galeria
Para configurar a integração do Leapsome ao Azure AD, você precisa adicionar o Leapsome da galeria à sua lista de aplicativos SaaS gerenciados.

**Para adicionar o Leapsome da galeria, execute as seguintes etapas:**

1. No **[Portal do Azure](https://portal.azure.com)**, no painel navegação à esquerda, clique no ícone **Azure Active Directory**. 

    ![O botão Azure Active Directory][1]

1. Navegue até **aplicativos empresariais**. Em seguida, vá para **todos os aplicativos**.

    ![A folha Aplicativos empresariais][2]
    
1. Clique no botão **Novo aplicativo** na parte superior da caixa de diálogo para adicionar o novo aplicativo.

    ![O botão Novo aplicativo][3]

1. Na caixa de pesquisa, digite **Leapsome**, selecione **Leapsome** no painel de resultados e, em seguida, clique no botão **Adicionar** para adicionar o aplicativo.

    ![Leapsome na lista de resultados](./media/leapsome-tutorial/tutorial_leapsome_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurar e testar logon único do Azure AD

Nesta seção, você configurará e testará o logon único do Azure AD com o Leapsome, com base em um usuário de teste chamado “Brenda Fernandes”.

Para que o logon único funcione, o Azure AD precisa saber qual usuário do Leapsome é equivalente a um usuário do Azure AD. Em outras palavras, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado no Leapsome.

Para configurar e testar o logon único do AD do Azure com o Leapsome, você precisa concluir os seguintes blocos de construção:

1. **[Configurar o logon único do Azure AD](#configure-azure-ad-single-sign-on)** – para habilitar seus usuários a usar esse recurso.
1. **[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** – para testar o logon único do Azure AD com Brenda Fernandes.
1. **[Criar de um usuário de teste do Leapsome](#create-a-leapsome-test-user)** – para ter um equivalente de Brenda Fernandes no Leapsome vinculado à representação do usuário no Azure AD.
1. **[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que Brenda Fernandes use o logon único do Azure AD.
1. **[Teste o logon único](#test-single-sign-on)** – para verificar se a configuração funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurar o logon único do Azure AD

Nesta seção, você habilitará o logon único do Azure AD no Portal do Azure e configurará o logon único no aplicativo Leapsome.

**Para configurar o logon único do Azure AD com o Leapsome, execute as seguintes etapas:**

1. No portal do Azure, na página de integração do aplicativo **Leapsome**, clique em **Logon único**.

    ![Link Configurar logon único][4]

1. Na caixa de diálogo **Logon único**, selecione **Modo** como **Logon baseado em SAML** para habilitar o logon único.
 
    ![Caixa de diálogo Logon único](./media/leapsome-tutorial/tutorial_leapsome_samlbase.png)

1. Na seção **Domínio e URLs do Leapsome**, realize as seguintes etapas se desejar configurar o aplicativo no modo iniciado pelo **IDP**:

    ![Informações de logon único de Domínio e URLs do Leapsome](./media/leapsome-tutorial/tutorial_leapsome_url.png)

     a. Na caixa de texto **Identificador**, digite uma URL: `https://www.leapsome.com`

    b. Na caixa de texto **URL de resposta**, digite uma URL no seguinte padrão: `https://www.leapsome.com/api/users/auth/saml/<CLIENTID>/assert`

1. Marque **Mostrar configurações avançadas de URL** e realize a seguinte etapa se quiser configurar o aplicativo no modo iniciado pelo **SP**:

    ![Informações de logon único de Domínio e URLs do Leapsome](./media/leapsome-tutorial/tutorial_leapsome_url1.png)

    Na caixa de texto **URL de Logon**, digite uma URL usando o seguinte padrão: `https://www.leapsome.com/api/users/auth/saml/<CLIENTID>/login`
     
    > [!NOTE] 
    > Os valores da URL de Resposta e URL de Entrada anteriores não são valores reais. Você atualizará os valores com valores reais, que é explicado no tutorial posteriormente.

1. O aplicativo Leapsome espera que as declarações SAML estejam em um formato específico. Configure as declarações a seguir para este aplicativo. Você pode gerenciar os valores desses atributos da seção **Atributos de Usuário** na página de integração de aplicativos. A captura de tela a seguir mostra um exemplo.
    
    ![Configurar o logon único](./media/leapsome-tutorial/tutorial_Leapsome_attribute.png)

1. Na seção **Atributos do usuário**, na caixa de diálogo **Logon único**, configure o atributo do token SAML na imagem acima e siga as etapas abaixo:
    
    | Nome do atributo | Valor do atributo | Namespace |
    | ---------------| --------------- | --------- |   
    | nome | user.givenname | http://schemas.xmlsoap.org/ws/2005/05/identity/claims |
    | sobrenome | user.surname | http://schemas.xmlsoap.org/ws/2005/05/identity/claims |
    | título | user.jobtitle | http://schemas.xmlsoap.org/ws/2005/05/identity/claims |
    | picture | URL para a imagem do funcionário | http://schemas.xmlsoap.org/ws/2005/05/identity/claims |

    > [!Note]
    > O valor do atributo de imagem não é real. Atualize esse valor com a URL da imagem real. Para obter esse valor, entre em contato com a  [equipe de suporte do Cliente Leapsome](mailto:support@leapsome.com).
    
     a. Clique em **Adicionar atributo** para abrir o diálogo **Adicionar Atributo**.

    ![Configurar o logon único](./media/leapsome-tutorial/tutorial_attribute_04.png)

    ![Configurar o logon único](./media/leapsome-tutorial/tutorial_attribute_05.png)
    
    b. Na caixa de texto **Nome** , digite o nome do atributo mostrado para essa linha.
    
    c. Na lista **Valor**, digite o valor do atributo mostrado para essa linha.

    d. Na caixa de texto **Namespace**, digite a uri de namespace para essa linha.
    
    e. Clique em **Ok**

1. Na seção **Certificado de Autenticação SAML**, clique em **Certificado (Base64)** e, em seguida, salve o arquivo do certificado em seu computador.

    ![O link de download do Certificado](./media/leapsome-tutorial/tutorial_leapsome_certificate.png) 

1. Clique no botão **Salvar** .

    ![Botão Salvar em Configurar Logon Único](./media/leapsome-tutorial/tutorial_general_400.png)
    
1. Na seção **Configuração do Leapsome**, clique em **Configurar o Leapsome** para abrir a janela **Configurar logon**. Copie a **URL de serviço de logon único SAML** da **seção de Referência Rápida.**

    ![Configuração Leapsome](./media/leapsome-tutorial/tutorial_leapsome_configure.png)

1. Em outra janela do navegador da Web, faça logon no Leapsome como Administrador de Segurança.

1. No canto superior direito, clique no logotipo de configurações e, em seguida, clique em **configurações do administrador**. 

    ![Conjunto de Leapsome](./media/leapsome-tutorial/tutorial_leapsome_admin.png)

1. Na barra de menus à esquerda, clique em **logon único (SSO)** e na **baseado no SAML-logon único (SSO)** página execute as seguintes etapas:
    
    ![saml de Leapsome](./media/leapsome-tutorial/tutorial_leapsome_samlsettings.png)

     a. Selecione **Habilitar Logon único baseado em SAML**.

    b. Copie o **URL de logon (ponto de seus usuários aqui para iniciar o logon)** valor e cole-o no **URL de logon** textbox em **Leapsome domínio e URLs** seção no portal do Azure.

    c. Copie o **valor URL de resposta (recebe a resposta do seu provedor de identidade)** e cole-o na caixa de texto **URL de resposta** na seção **Domínio e URLs Leapsome** no portal do Azure.

    d. Na caixa de texto **URL de Logon SSO (fornecida pelo provedor de identidade)**, cole o valor da **URL do Serviço de Logon Único SAML** copiado do Portal do Azure.

    e. Copie o certificado que você baixou do portal do Azure sem - BEGIN CERTIFICATE e END certificado, comentários e cole-o no **certificado (fornecido pelo provedor de identidade)** caixa de texto.

    f. Clique em **ATUALIZAR CONFIGURAÇÕES SSO**.
    
### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

O objetivo desta seção é criar um usuário de teste no Portal do Azure chamado Brenda Fernandes.

   ![Criar um usuário de teste do Azure AD][100]

**Para criar um usuário de teste no AD do Azure, execute as seguintes etapas:**

1. No portal do Azure, no painel esquerdo, clique no botão **Azure Active Directory**.

    ![O botão Azure Active Directory](./media/leapsome-tutorial/create_aaduser_01.png)

1. Para exibir a lista de usuários, acesse **Usuários e grupos** e, depois, clique em **Todos os usuários**.

    ![Os links “Usuários e grupos” e “Todos os usuários”](./media/leapsome-tutorial/create_aaduser_02.png)

1. Para abrir a caixa de diálogo **Usuário**, clique em **Adicionar** na parte superior da caixa de diálogo **Todos os Usuários**.

    ![O botão Adicionar](./media/leapsome-tutorial/create_aaduser_03.png)

1. Na caixa de diálogo **Usuário**, execute as seguintes etapas:

    ![A caixa de diálogo Usuário](./media/leapsome-tutorial/create_aaduser_04.png)

    a. Na caixa **Nome**, digite **BrendaFernandes**.

    b. Na caixa **Nome de usuário**, digite o endereço de email do usuário Brenda Fernandes.

    c. Marque a caixa de seleção **Mostrar Senha** e, em seguida, anote o valor exibido na caixa **Senha**.

    d. Clique em **Criar**.
 
### <a name="create-a-leapsome-test-user"></a>Criar um usuário de teste Leapsome

Nesta seção, você criará uma usuária chamada Brenda Fernandes no Leapsome. Trabalhe com a  [Equipe de suporte do Cliente Leapsome](mailto:support@leapsome.com) para adicionar os usuários ou o domínio, que precisa estar na lista de permissões na plataforma Leapsome. Se o domínio for adicionado pela equipe, os usuários serão automaticamente provisionados à plataforma Leapsome. Os usuários devem ser criados e ativados antes de usar o logon único. 

### <a name="assign-the-azure-ad-test-user"></a>Atribuir o usuário de teste do Azure AD

Nesta seção, você permitirá que Brenda Fernandes use o logon único do Azure concedendo-lhe acesso ao Leapsome.

![Atribuir a função de usuário][200] 

**Para atribuir Brenda Fernandes ao Leapsome, execute as seguintes etapas:**

1. No Portal do Azure, abra a exibição de aplicativos e, em seguida, navegue até a exibição de diretório e vá para **Aplicativos Empresariais** e clique em **Todos os aplicativos**.

    ![Atribuir usuário][201] 

1. Na lista de aplicativos, selecione **Leapsome**.

    ![O link do Leapsome na lista de Aplicativos](./media/leapsome-tutorial/tutorial_leapsome_app.png)  

1. No menu à esquerda, clique em **usuários e grupos**.

    ![O link “Usuários e grupos”][202]

1. Clique no botão **Adicionar**. Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.

    ![O painel Adicionar Atribuição][203]

1. Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários.

1. Clique em **selecione** botão **usuários e grupos** caixa de diálogo.

1. Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.
    
### <a name="test-single-sign-on"></a>Testar logon único

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Quando você clicar no bloco Leapsome no Painel de Acesso, deverá ser automaticamente conectado ao seu aplicativo Leapsome.
Para saber mais sobre o Painel de Acesso, confira [Introdução ao Painel de Acesso](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionais

* [Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure](tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/leapsome-tutorial/tutorial_general_01.png
[2]: ./media/leapsome-tutorial/tutorial_general_02.png
[3]: ./media/leapsome-tutorial/tutorial_general_03.png
[4]: ./media/leapsome-tutorial/tutorial_general_04.png

[100]: ./media/leapsome-tutorial/tutorial_general_100.png

[200]: ./media/leapsome-tutorial/tutorial_general_200.png
[201]: ./media/leapsome-tutorial/tutorial_general_201.png
[202]: ./media/leapsome-tutorial/tutorial_general_202.png
[203]: ./media/leapsome-tutorial/tutorial_general_203.png

