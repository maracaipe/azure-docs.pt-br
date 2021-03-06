---
title: Solução de problemas do Azure Active Directory híbrido ingressado em dispositivos do Windows 10 e do Windows Server 2016 | Microsoft Docs
description: Solução de problemas do Azure Active Directory híbrido ingressado em dispositivos do Windows 10 e do Windows Server 2016.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: daveba
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.subservice: devices
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/08/2017
ms.author: markvi
ms.reviewer: jairoc
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4ee5620bfcd421dcb108ce330be3a21cb8ba4a43
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/13/2019
ms.locfileid: "56187161"
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-windows-10-and-windows-server-2016-devices"></a>Solução de problemas do Azure Active Directory híbrido ingressado em dispositivos do Windows 10 e do Windows Server 2016 

Este artigo se aplica aos seguintes clientes:

-   Windows 10
-   Windows Server 2016

Para outros clientes do Windows, consulte [Solução de problemas do Azure Active Directory híbrido ingressado em dispositivos de nível inferior](troubleshoot-hybrid-join-windows-legacy.md).

Este artigo pressupõe que você tenha [dispositivos configurados e ingressados no Azure Active Directory híbrido](hybrid-azuread-join-plan.md) para dar suporte aos seguintes cenários:

- Acesso condicional com base em dispositivo

- [Roaming corporativo de configurações](../active-directory-windows-enterprise-state-roaming-overview.md)

- [Configurar o Hello for Business](../active-directory-azureadjoin-passport-deployment.md)


Este documento fornece diretrizes de solução de problemas sobre como resolver os problemas potenciais. 


Para Windows 10 e Windows Server 2016, o ingresso do Azure Active Directory híbrido oferece suporte à atualização de 10 de novembro de 2015 e superior do Windows 10. Recomendamos usar a atualização de Aniversário.

## <a name="step-1-retrieve-the-join-status"></a>Etapa 1: Recuperar o status de ingresso 

**Para recuperar o status do ingresso:**

1. Abra o prompt de comando como administrador

2. Digite **dsregcmd /status**



    +----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+
    
        AzureAdJoined: YES
     EnterpriseJoined: NO DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Provedor de Criptografia de Plataforma Microsoft TpmProtected: YES KeySignTest: : DEVE Executar com privilégios elevados para testar.
                  Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO
    
    +----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+
    
                 NgcSet: YES
               NgcKeyId: {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined: NO
          WamDefaultSet: YES
    WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: SIM



## <a name="step-2-evaluate-the-join-status"></a>Etapa 2: Avaliar o status do ingresso 

Examine os seguintes campos e garanta que eles tenham os valores esperados:

### <a name="azureadjoined--yes"></a>AzureAdJoined : SIM  

Esse campo indica se o dispositivo ingressou no Azure AD. Se o valor for **NO**, a associação ao Azure AD ainda não terá sido concluída. 

**Possíveis causas:**

- Falha na autenticação do computador para um ingresso.

- Há um proxy HTTP na organização que não pode ser descoberto pelo computador

- O computador não pode alcançar o Azure AD para autenticação, ou o Azure DRS para registro

- O computador pode não estar na rede interna da organização ou em VPN com a linha de visão direta para um controlador de domínio do AD local.

- Se o computador tiver um TPM, poderá estar em um estado inválido.

- Pode haver um erro de configuração nos serviços, observado anteriormente no documento, que você precisará verificar novamente. Alguns exemplos comuns são:

    - O servidor de Federação não tem pontos de extremidade WS-Trust habilitados

    - O servidor de federação não permite a autenticação de entrada de computadores em sua rede usando a Autenticação Integrada do Windows.

    - Não há nenhum objeto de Ponto de Conexão de Serviço que aponta para o seu nome de domínio verificado no Azure AD na floresta do AD à qual o computador pertence

---

### <a name="domainjoined--yes"></a>DomainJoined : SIM  

Esse campo indica se o dispositivo ingressou em um Active Directory local ou não. Se o valor for **NO**, o dispositivo não poderá executar um ingresso do Azure AD híbrido.  

---

### <a name="workplacejoined--no"></a>WorkplaceJoined : NÃO  

Esse campo indica se o dispositivo está registrado no Azure AD como um dispositivo pessoal (marcado como *Ingressado no Espaço de Trabalho*). Esse valor deve ser **NO** para um computador ingressado no domínio, que também é ingressado no Azure AD híbrido. Se o valor for **YES**, uma conta corporativa ou de estudante terá sido adicionada antes da conclusão do ingresso do Azure AD híbrido. Nesse caso, a conta é ignorada ao usar a versão de Atualização de Aniversário do Windows 10 (1607).

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a>WamDefaultSet : YES e AzureADPrt: SIM
  
Esses campos indicam se o usuário foi autenticado com êxito no Azure AD ao se conectar ao dispositivo. Se os valores forem **NO**, talvez o motivo seja:

- STK (chave de armazenamento) inválida no TPM associada ao dispositivo no registro (verifique o KeySignTest durante a execução com privilégios elevados).

- ID de logon alternativo

- Proxy HTTP não encontrado

## <a name="next-steps"></a>Próximas etapas

Para perguntas, consulte as [Perguntas frequentes sobre o gerenciamento de dispositivos](faq.md) 
