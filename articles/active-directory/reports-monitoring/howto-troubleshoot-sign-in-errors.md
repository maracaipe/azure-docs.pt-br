---
title: Como solucionar erros de entrada usando relatórios do Active Directory Domain Services do Azure | Microsoft Docs
description: Aprenda a solucionar erros de login usando relatórios do Azure Active Directory Domain Services no portal do Azure
services: active-directory
documentationcenter: ''
author: priyamohanram
manager: daveba
editor: ''
ms.service: active-directory
ms.topic: conceptual
ms.workload: identity
ms.subservice: report-monitor
ms.date: 11/13/2018
ms.author: priyamo
ms.reviewer: dhanyahk
ms.collection: M365-identity-device-management
ms.openlocfilehash: 22126114f2d4fcb865485d9cebc69f0e35f70201
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/13/2019
ms.locfileid: "56198466"
---
# <a name="how-to-troubleshoot-sign-in-errors-using-azure-active-directory-reports"></a>Como: Solucionar problemas de erros de logon usando relatórios do Azure Active Directory Domain Services

O [relatório de logins](concept-sign-ins.md) no Azure AD (Azure Active Directory Domain Services) permite que você encontre respostas a perguntas sobre como gerenciar o acesso aos aplicativos em sua organização, incluindo:

- O que é o padrão de entrada de um usuário?
- Quantos usuários entraram em uma semana?
- Qual é o status dessas entradas?


Além disso, o relatório de logins também pode ajudar você a solucionar falhas de login para usuários em sua organização. Neste guia, você aprende como isolar uma falha de entrada no relatório de entrada e usá-la para reconhecer a causa raiz da falha.

## <a name="prerequisites"></a>Pré-requisitos

Você precisa de:

* Um locatário do Microsoft Azure Active Directory com uma licença premium (P1/P2). Consulte [Introdução ao Azure Active Directory Premium](../fundamentals/active-directory-get-started-premium.md) para fazer upgrade da edição do Azure Active Directory.
* Um usuário, que está na função de **administrador global**, **administrador de segurança**, **leitor de segurança** ou **leitor de relatório** para o locatário. Além disso, qualquer usuário pode acessar suas próprias entradas. 

## <a name="troubleshoot-sign-in-errors-using-the-sign-ins-report"></a>Solucionar problemas de erros de entrada usando o relatório de entradas

1. Navegue até o [portal do Azure](https://portal.azure.com) e selecione seu diretório.
2. Selecione **Azure Active Directory** e selecione **Entradas** na seção **Monitoramento**. 
3. Use os filtros fornecidos para restringir a falha, seja pelo nome de usuário ou identificador de objeto, nome do aplicativo ou data. Além disso, selecione **Falha** na lista suspensa **Status** para exibir apenas os logins com falha. 

    ![Resultados do filtro](./media/howto-troubleshoot-sign-in-errors/filters.png)
        
4. Identifique o login com falha que você deseja investigar e selecione-o. Isso abrirá a janela de detalhes adicionais com mais informações sobre o login com falha. Anote o **código de erro de login** e **motivo de falha**. 

    ![Selecione o registro](./media/howto-troubleshoot-sign-in-errors/sign-in-failures.png)
        
5. Você também pode encontrar essas informações na guia **Solução de problemas e suporte** na janela de detalhes.

    ![Solução de problemas e suporte](./media/howto-troubleshoot-sign-in-errors/troubleshooting-and-support.png)

6. O motivo da falha descreve o erro. Por exemplo, no cenário acima, o motivo da falha é **Nome de usuário ou senha inválidos ou Nome de usuário ou senha inválida no local**. Isso significa que o usuário digitou um nome de usuário ou senha incorreto para entrar no portal do Azure. A correção é simplesmente entrar novamente com o nome de usuário e a senha corretos.

7. Você pode obter informações adicionais, incluindo ideias para correção, pesquisando o código de erro **50126** neste exemplo, na referência de códigos de erro de [log-ins](reference-sign-ins-error-codes.md). 

8. Se tudo mais falhar ou se o problema persistir apesar de ter tomado as medidas recomendadas, [abra um tíquete de suporte](../fundamentals/active-directory-troubleshooting-support-howto.md) seguindo as etapas na guia **Solução de problemas e suporte**. 

## <a name="next-steps"></a>Próximas etapas

* [Códigos de erro de entradas de referência](reference-sign-ins-error-codes.md)
* [Visão geral do relatório de entradas](concept-sign-ins.md)
