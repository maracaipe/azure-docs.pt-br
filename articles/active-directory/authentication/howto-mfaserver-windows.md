---
title: Autenticação do Windows e servidor Azure MFA | Microsoft Docs
description: Implantação da Autenticação do Windows e Servidor de Autenticação Multifator do Azure.
services: multi-factor-authentication
ms.service: active-directory
ms.subservice: authentication
ms.topic: conceptual
ms.date: 07/11/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: daveba
ms.reviewer: michmcla
ms.collection: M365-identity-device-management
ms.openlocfilehash: 857e256b0fb2cd726e38232c96f7ce0750681245
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/13/2019
ms.locfileid: "56197191"
---
# <a name="windows-authentication-and-azure-multi-factor-authentication-server"></a>Autenticação do Windows e Servidor de Autenticação Multifator do Azure

Use a seção de autenticação do Windows do servidor de Autenticação Multifator do Azure para habilitar e configurar a autenticação do Windows para aplicativos. Antes de configurar a autenticação do Windows, lembre-se a lista a seguir:

* Após a instalação, reinicie a Autenticação Multifator do Azure para que os serviços de Terminal entrem em vigor.
* Se a opção 'Exigir correspondência de usuário da Autenticação Multifator do Azure' for marcada e você não estiver na lista de usuários, não será possível fazer logon no computador após a reinicialização.
* IPs confiáveis dependem de o aplicativo poder fornecer o IP do cliente com a autenticação. Atualmente, apenas os Serviços de Terminal têm suporte.  

> [!NOTE]
> Esse recurso não tem suporte para proteger os Serviços de Terminal no Windows Server 2012 R2.

## <a name="to-secure-an-application-with-windows-authentication-use-the-following-procedure"></a>Para proteger um aplicativo com a Autenticação do Windows, use o procedimento a seguir.
1. No Servidor de Autenticação Multifator do Azure, clique no ícone de Autenticação do Windows.
   ![Autenticação do Windows](./media/howto-mfaserver-windows/windowsauth.png)
2. Marque a caixa de seleção **Habilitar Autenticação do Windows**. Por padrão, essa caixa está desmarcada.
3. A guia Aplicativos permite que o administrador configure um ou mais aplicativos para Autenticação do Windows.
4. Selecione um servidor ou aplicativo — especifique se o servidor/aplicativo está habilitado. Clique em **OK**.
5. Clique em **Adicionar...**
6. A guia IPs Confiáveis permite que você ignore as sessões da Autenticação Multifator do Azure para Windows originadas de IPs específicos. Por exemplo, se os funcionários usarem o aplicativo no escritório e em casa, você pode decidir que não deseja que seus telefones toquem para a Autenticação Multifator do Azure enquanto estiverem no escritório. Para isso, você especifica a sub-rede do escritório como entrada de IPs Confiáveis.
7. Clique em **Adicionar...**
8. Selecione **IP Único** se desejar ignorar um único endereço IP.
9. Selecione o **Intervalo de IP** se desejar ignorar um intervalo inteiro de IP. Exemplo 10.63.193.1-10.63.193.100.
10. Selecione **Sub-rede** se desejar especificar um intervalo de IPs usando a notação de sub-rede. Insira o IP inicial da sub-rede e escolha a máscara de rede adequada na lista suspensa.
11. Clique em **OK**.

## <a name="next-steps"></a>Próximas etapas

- [Configure os dispositivos de VPN de terceiros para servidor Azure MFA](howto-mfaserver-nps-vpn.md)

- [Aumentar sua infraestrutura de autenticação atual com a extensão do NPS para o Azure MFA](howto-mfa-nps-extension.md)
