---
title: Histórico de lançamento de versão do agente de Proteção de Senha do Azure AD local
description: Lançamento de versão de documentos e o comportamento de histórico de alterações
services: active-directory
ms.service: active-directory
ms.subservice: authentication
ms.topic: article
ms.date: 02/01/2019
ms.author: joflore
author: MicrosoftGuyJFlo
manager: daveba
ms.reviewer: jsimmons
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8897651c963b0036bc2ac3d8cdb06a52d6f52ba1
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/13/2019
ms.locfileid: "56188028"
---
# <a name="preview--azure-ad-password-protection-agent-version-history"></a>Visualização:  Histórico de versão do agente de Proteção de Senha do Azure AD

|     |
| --- |
| A Proteção de Senha do Azure AD é uma versão prévia pública do recurso do Azure Active Directory. Para obter mais informações sobre versões prévias, consulte os [Termos de Uso Complementares para Visualizações do Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)|
|     |

## <a name="12650"></a>1.2.65.0

Data de lançamento: 1/2/2019

Alterações:

* Agora há compatibilidade com o serviço de agente e proxy do DC no Server Core. Os requisitos de sistema operacional mínimos são os mesmos de antes: Windows Server 2012 para agentes do DC e Windows Server 2012 R2 para proxies.
* Os cmdlets Register-AzureADPasswordProtectionProxy e Register-AzureADPasswordProtectionForest agora são compatíveis com os modos de autenticação do Azure baseados em código.
* O cmdlet Get-AzureADPasswordProtectionDCAgent ignorará os pontos de conexão de serviço inválidos e/ou danificados. Isso corrige o bug em que os controladores de domínio, às vezes, apareciam várias vezes na saída.
* O cmdlet Get-AzureADPasswordProtectionSummaryReport ignorará os pontos de conexão de serviço inválidos e/ou danificados. Isso corrige o bug em que os controladores de domínio, às vezes, apareciam várias vezes na saída.
* O módulo do PowerShell Proxy agora é registrado de %ProgramFiles%\WindowsPowerShell\Modules. A variável de ambiente PSModulePath do computador não é mais modificada.
* Foi adicionado um novo cmdlet Get-AzureADPasswordProtectionProxy para auxiliar na descoberta de proxies registrados em um domínio ou floresta.
* O agente do DC usa uma nova pasta no compartilhamento sysvol para replicar políticas de senha e outros arquivos.

   Localização da pasta antiga:

   `\\<domain>\sysvol\<domain fqdn>\Policies\{4A9AB66B-4365-4C2A-996C-58ED9927332D}`

   Nova localização da pasta:

   `\\<domain>\sysvol\<domain fqdn>\AzureADPasswordProtection`

   (Essa alteração foi feita para evitar avisos de “GPO órfão” falso-positivos.)

   > [!NOTE]
   > Nenhuma migração ou compartilhamento de dados será feita entre a pasta antiga e a nova pasta. As versões mais antigas do agente do DC continuarão a usar o local antigo até serem atualizadas para esta versão ou posterior. Depois que todos os agentes do DC estiverem executando a versão 1.2.65.0 ou posterior, a pasta sysvol antiga poderá ser excluída manualmente.

* O serviço de proxy e do agente do DC agora detectarão e excluirão cópias danificadas de seus respectivos pontos de conexão de serviço.
* Cada agente do DC excluirá periodicamente pontos de conexão de serviço danificado e obsoletos em seu domínio, para pontos de conexão do serviço de proxy e do agente do DC. Os pontos de conexão do serviço de proxy e do agente do DC são considerados obsoletos caso seu carimbo de data/hora de pulsação tenha mais de sete dias.
* O agente do DC agora renovará o certificado da floresta conforme necessário.
* O serviço de proxy agora renovará o certificado de proxy conforme necessário.
* Atualizações para o algoritmo de validação de senha: a lista de senhas banidas global e a lista de senhas banidas específicas do cliente (se configuradas) são combinadas antes de validações de senha. Uma determinada senha agora pode ser rejeitada (falha ou somente auditoria) se ele contiver tokens na lista global e na específica do cliente. A documentação do log de eventos foi atualizada para refletir isso. Consulte [Monitorar Proteção de Senha do Azure AD](howto-password-ban-bad-on-premises-monitor.md).
* Correções de desempenho e robustez
* Log aprimorado

> [!WARNING]
> Funcionalidade de tempo limitado: o serviço de agente do DC nesta versão (1.2.65.0) parará o processamento de solicitações de validação de senha a partir de 1º de setembro de 2019.  Serviços de agente do DC em versões anteriores (consulte a lista abaixo) parará de processar a partir de 1º de julho de 2019. O serviço de agente do DC em todas as versões registrará 10021 eventos para o log de eventos do administrador nos dois meses anteriores a esses prazos. Todas as restrições de limite de tempo serão removidas na próxima versão com disponibilidade geral. O serviço de agente de Proxy não tem limitação de tempo em nenhuma versão, mas ainda deve ser atualizada para a versão mais recente para aproveitar todas as correções de bug subsequentes e outras melhorias.

## <a name="12250"></a>1.2.25.0

Data de lançamento: 01/11/2018

Correções:

* Serviço de agente e o proxy do controlador de domínio não deve falhar devido a falhas de relação de confiança de certificado.
* Serviço de agente e o proxy do controlador de domínio têm correções adicionais para computadores em conformidade com FIPS.
* Serviço de proxy agora funcionará corretamente em um ambiente de chamadas rede somente 1.2 TLS.
* Menor de desempenho e correções de robustez
* Log aprimorado

Alterações:

* O nível de sistema operacional mínimo exigido para o serviço Proxy é agora o Windows Server 2012 R2. O nível de sistema operacional mínimo exigido para o serviço do agente DC permanece no Windows Server 2012.
* Agora, o serviço de Proxy requer o .NET versão 4.6.2.
* O algoritmo de validação de senha usa uma tabela de normalização de caracteres expandida. Isso pode resultar na rejeição de senhas aceitas em versões anteriores.

## <a name="12100"></a>1.2.10.0

Data de lançamento: 17/8/2018

Correções:

* Register-AzureADPasswordProtectionProxy e Register-AzureADPasswordProtectionForest agora dão suporte a autenticação multifator
* Register-AzureADPasswordProtectionProxy requer um WS2012 ou domínio posterior no domínio para evitar erros de criptografia.
* O serviço de agente do controlador de domínio é mais confiável sobre como solicitar uma nova política de senha do Azure na inicialização.
* O serviço de agente do DC solicitará uma nova política de senha do Azure a cada hora se necessário, mas agora vai fazer isso em uma hora de início selecionada aleatoriamente.
* O serviço de agente do controlador de domínio não fará com que um atraso indefinido no novo anúncio do controlador de domínio quando instalado em um servidor antes da sua promoção como uma réplica.
* O serviço de agente do controlador de domínio agora respeitará a definição de configuração "Habilitar a proteção por senha no Active Directory do Windows Server"
* Ambos os instaladores de agente e o proxy do controlador de domínio agora serão compatível com a atualização in-loco ao atualizar para versões futuras.

> [!WARNING]
> Atualização in-loco de versão 1.1.10.3 não tem suporte e resultará em um erro de instalação. Para atualizar para a versão 1.2.10 ou posterior, você deve primeiro completamente desinstalar o software de serviço de agente e o proxy de controlador de domínio, e instalar a nova versão a partir do zero. Instalar e configurar o serviço proxy de proteção por senha do Azure Active Directory.  Não é necessário registrar novamente a floresta.

> [!NOTE]
> Atualizações in-loco do software agente DC exigirá uma reinicialização.

* Serviço de agente e o proxy do controlador de domínio agora oferecem suporte em execução em um servidor configurado para usar somente os algoritmos compatíveis com FIPS.
* Menor de desempenho e correções de robustez
* Log aprimorado

## <a name="11103"></a>1.1.10.3

Data de lançamento: 15/6/2018

Versão prévia pública inicial

## <a name="next-steps"></a>Próximas etapas

[Implantar Proteção de Senha do Azure AD](howto-password-ban-bad-on-premises-deploy.md)
