---
title: Protegendo suas máquinas e aplicativos na Central de Segurança do Azure | Microsoft Docs
description: Este documento aborda as recomendações da Central de Segurança que ajudam a proteger suas máquinas virtuais, seus computadores e os ambientes de aplicativos Web e do Serviço de Aplicativo.
services: security-center
documentationcenter: na
author: monhaber
manager: barbkess
editor: ''
ms.assetid: 47fa1f76-683d-4230-b4ed-d123fef9a3e8
ms.service: security-center
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 1/27/2019
ms.author: monhaber
ms.openlocfilehash: 8dcaa9b98292e66d81daf3d115159b0c0c1124af
ms.sourcegitcommit: fec0e51a3af74b428d5cc23b6d0835ed0ac1e4d8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56106709"
---
# <a name="protecting-your-machines-and-applications-in-azure-security-center"></a>Protegendo suas máquinas e aplicativos na Central de Segurança do Azure
A Central de Segurança do Azure analisa o estado de segurança de seus recursos do Azure. Quando a Central de Segurança identifica possíveis vulnerabilidades de segurança, ela cria recomendações que orientam você durante o processo de configuração dos controles necessários. As recomendações aplicam-se aos tipos de recursos do Azure: VMs (máquinas virtuais) e computadores, aplicativos, rede, SQL e a identidade e acesso.

Este artigo aborda as recomendações que se aplicam a computadores e aplicativos.

## <a name="monitoring-security-health"></a>Monitoramento de integridade da segurança
Você pode monitorar o estado de segurança de seus recursos na **Central de segurança – visão geral** painel. A seção **Recursos** fornece o número de problemas identificados e o estado de segurança de cada tipo de recurso.

Você pode visualizar uma lista de todos os problemas selecionando **Recomendações**. Para obter mais informações sobre como aplicar recomendações, confira [Implementando as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md).

Para obter uma lista completa de recomendações dos Serviços de Computação e de Aplicativos, confira [Recomendações](security-center-virtual-machine-recommendations.md).

Para continuar, selecione **Computação e aplicativos** em **Recursos** ou no menu principal da Central de Segurança.
![Painel da Central de Segurança](./media/security-center-virtual-machine-recommendations/overview.png)

## <a name="monitor-compute-and-app-services"></a>Monitorar serviços de computação e de aplicativo
Em **Computação e Aplicativos**, há as guias a seguir:

- **Visão geral**: monitoramento e recomendações identificadas pela Central de Segurança.
- **VMs e computadores**: lista de suas máquinas virtuais, computadores e estado de segurança atual de cada um.
- **Serviços de nuvem**: lista de suas funções web e de trabalho monitoradas pela Central de Segurança.
- **Serviços de Aplicativos**: lista de seus ambientes do Serviço de Aplicativo e o estado de segurança atual de cada um.
- **Contêineres (versão prévia)**: lista de contêineres hospedados em máquinas do Linux de IaaS e avaliação de segurança das configurações do Docker.
- **Recursos de computação (versão prévia)**: lista de recomendações para os recursos de computação como clusters do Service Fabric e Hubs de Eventos.

Para continuar, selecione **Computação e aplicativos** em **Higiene de segurança de recurso**.

![Computação](./media/security-center-virtual-machine-recommendations/compute.png)

Há várias seções em cada guia e, em cada seção, você pode selecionar uma opção individual para ver mais detalhes sobre as etapas recomendadas e resolver esse problema específico.

### VMs e computadores não monitorados <a name="unmonitored-vms-and-computers"></a>
As VM ou os computadores não são monitorados pela Central de Segurança quando não estão executando a extensão do Microsoft Monitoring Agent. Um computador pode ter um agente local já instalado, por exemplo, o agente direto do OMS ou o agente do SCOM. Os computadores com esses agentes são identificados como não monitorados porque não há suporte total para esses agentes na Central de Segurança. Para aproveitar ao máximo todos os recursos da Central de Segurança, é necessária a extensão do Microsoft Monitoring Agent.

Você pode instalar a extensão na VM ou no computador não monitorado, além do agente local já instalado. Configure os dois agentes iguais, conectando-os ao mesmo workspace. Isso permite que a Central de Segurança interaja com a extensão do Microsoft Monitoring Agent e colete dados. Consulte [Habilitar a extensão da VM](../azure-monitor/learn/quick-collect-azurevm.md) para obter instruções sobre como instalar a extensão do Microsoft Monitoring Agent.

Consulte [Monitorando problemas de integridade do agente](security-center-troubleshooting-guide.md#mon-agent) para saber mais sobre o motivo pelo qual a Central de Segurança não consegue monitorar com êxito as VMs e os computadores inicializados para o provisionamento automático.

### <a name="recommendations"></a>Recomendações
Esta seção tem um conjunto de recomendações para cada VM e computador, funções web e de trabalho, Aplicativos Web do Serviço de Aplicativo do Azure e o ambiente do Serviço de Aplicativo do Azure que a Central de Segurança monitora. A primeira coluna lista a recomendação. A segunda coluna mostra o número total de recursos que são afetados por essa recomendação. A terceira coluna mostra a gravidade do problema.

Cada recomendação tem um conjunto de ações que você poderá executar depois de selecioná-la. Por exemplo, se você selecionar **Atualizações do sistema ausentes**, o número de VMs e computadores com patches ausentes e a gravidade da atualização ausente serão exibidos.

**Aplicar atualizações do sistema** tem um resumo de atualizações críticas no formato de gráfico, um para Windows e outro para Linux. A segunda parte tem uma tabela com as seguintes informações:

- **NOME**: Nome da atualização ausente.
- **NÃO. DE VMs E COMPUTADORES**: Número total de máquinas virtuais e computadores que não têm essa atualização.
- **GRAVIDADE DA ATUALIZAÇÃO**: Descreve a gravidade dessa recomendação específica:

    - **Crítica**: Existe uma vulnerabilidade em um recurso significativo (aplicativo, máquina virtual ou grupo de segurança de rede) e ela requer atenção.
    - **Importante**: São necessárias etapas adicionais ou não críticas para concluir um processo ou eliminar uma vulnerabilidade.
    - **Moderada**: Uma vulnerabilidade que deve ser resolvida, mas não exige atenção imediata. (Por padrão, não são apresentadas recomendações baixas, mas você pode filtrar as recomendações baixas caso deseje exibi-las.)


- **ESTADO**: O estado atual da recomendação:

    - **Aberto**: A recomendação ainda não foi resolvida.
    - **Em Andamento**: A recomendação está sendo aplicada atualmente a esses recursos e não é necessário que você realize nenhuma ação.
    - **Resolvida**: A recomendação já foi concluída. (Quando o problema foi resolvido, a entrada será esmaecida).

Para exibir os detalhes de recomendação, clique no nome da atualização ausente na lista.


> [!NOTE]
> As recomendações de segurança aqui são as mesmas que as do bloco **Recomendações**. Confira [Implementando recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md) para obter mais informações de como resolver as recomendações.
>
>

### <a name="vms-and-computers"></a>VMs e computadores
A seção de VMs e computadores fornece uma visão geral de todas as recomendações para VMs e computadores. Cada coluna representa um conjunto de recomendações.

![Recomendações para VMs e computadores](./media/security-center-virtual-machine-recommendations/vm-computers.png)

Há quatro tipos de ícones representados nesta lista:

![Computador não Azure](./media/security-center-virtual-machine-recommendations/security-center-monitoring-icon1.png) Computador não Azure.

![VM do Azure Resource Manager](./media/security-center-virtual-machine-recommendations/security-center-monitoring-icon2.png) VM do Azure Resource Manager.

![VM Clássica do Azure](./media/security-center-virtual-machine-recommendations/security-center-monitoring-icon3.png) VM Clássica do Azure.


![VMs identificadas no workspace](./media/security-center-virtual-machine-recommendations/security-center-monitoring-icon4.png) VMs identificadas somente pelo workspace que faz parte da assinatura exibida. Isso inclui VMs de outras assinaturas que se reportam ao workspace nesta assinatura e VMs que foram instaladas com o agente direto SCOM e não têm nenhuma ID de recurso.

O ícone que aparece em cada recomendação ajuda a identificar rapidamente a VM e o computador que precisa de atenção e o tipo de recomendação. Você também pode usar os filtros para pesquisar a lista por **Tipo de recurso** e por **Gravidade**.

Para detalhar as recomendações de segurança para cada VM, clique na VM.
Veja aqui os detalhes de segurança da VM ou do computador. Na parte inferior, você pode ver a ação recomendada e a gravidade de cada problema.
![Serviços de nuvem](./media/security-center-virtual-machine-recommendations/recommendation-list.png)

### <a name="cloud-services"></a>Serviços de Nuvem
Para serviços de nuvem, uma recomendação será criada quando a versão do sistema operacional estiver desatualizada.

![Serviços de Nuvem](./media/security-center-virtual-machine-recommendations/security-center-monitoring-fig1-new006-2017.png)

Em um cenário no qual há uma recomendação (que não é o caso do exemplo anterior), você precisa seguir as etapas na recomendação para atualizar a versão do sistema operacional. Quando uma atualização estiver disponível, você terá um alerta (vermelho ou laranja - depende da gravidade do problema). Ao selecionar esse alerta nas linhas WebRole1 (executa o Windows Server com aplicativo Web implantado automaticamente no IIS) ou WorkerRole1 (executa o Windows Server com aplicativo Web implantado automaticamente no IIS), você verá mais detalhes sobre essa recomendação.

Para ver uma explicação mais detalhada sobre essa recomendação, clique em **Atualizar versão do sistema operacional** na coluna **DESCRIÇÃO**.



![Atualizar a versão do sistema operacional](./media/security-center-virtual-machine-recommendations/security-center-monitoring-fig8-new4.png)

### <a name="app-services"></a>Serviços de aplicativos
Você precisa habilitar o Serviço de Aplicativo em sua assinatura para exibir as informações de Serviço de Aplicativo. Para obter instruções sobre como habilitar esse recurso, confira [Proteger o Serviço de Aplicativo com a Central de Segurança do Azure](security-center-app-services.md).
[!NOTE]
> O monitoramento do Serviço de Aplicativo está na versão prévia e está disponível apenas no nível Standard da Central de Segurança.


Em **Serviços de Aplicativos**, você encontra uma lista de seus ambientes do Serviço de Aplicativo e o resumo de integridade com base na avaliação executada pela Central de Segurança.

![Serviços de aplicativos](./media/security-center-virtual-machine-recommendations/app-services.png)

Há três tipos de ícones representados nesta lista:

![Ambiente de Serviços de Aplicativos](./media/security-center-virtual-machine-recommendations/ase.png) Ambiente de Serviços de Aplicativos.

![Aplicativo Web](./media/security-center-virtual-machine-recommendations/web-app.png) Aplicativo Web.

![Aplicativo de função](./media/security-center-virtual-machine-recommendations/function-app.png) Aplicativo de função.

1. Selecione um aplicativo Web. Abre uma exibição de resumo com três guias:

  - **Recomendações**: com base nas avaliações realizadas pela Central de segurança que falhou.
  - **Avaliações aprovadas**: lista de avaliações realizadas pela Central de Segurança que foram aprovadas.
  - **Avaliações não disponíveis**: lista de avaliações que falharam devido a um erro ou a recomendação não é relevante para o Serviço de Aplicativo específico

  Em **Recomendações** há uma lista das recomendações para o aplicativo Web selecionado e a gravidade de cada recomendação.

  ![Recomendações dos Serviços de Aplicativos](./media/security-center-virtual-machine-recommendations/app-services-rec.png)

2. Selecione uma recomendação para ver uma descrição da recomendação e uma lista de recursos não íntegros, recursos íntegros e recursos não examinados.

 - Na coluna **Avaliações aprovadas** há uma lista de avaliações aprovadas.  Gravidade dessas avaliações sempre é verde.

 -  Selecione uma avaliação passada na lista para obter uma descrição da avaliação, uma lista de recursos íntegros e não íntegros e uma lista de recursos não examinados. Há uma guia para os recursos não íntegros, mas essa lista está sempre vazia, pois a avaliação foi aprovada.

    ![Correção do Serviço de Aplicativo](./media/security-center-virtual-machine-recommendations/app-service-remediation.png)


## <a name="compute-and-app-recommendations"></a>Recomendações de computação e aplicativo
|Tipo de recurso|Classificação de segurança|Recomendações|DESCRIÇÃO|
|----|----|----|----|
|serviço de aplicativo|20|Aplicativo Web deve ser acessível somente por HTTPS|Limitar o acesso de aplicativos da Web somente por HTTPS.|
|serviço de aplicativo|20|O aplicativo de funções deve ser acessível apenas por HTTPS|Limite o acesso de aplicativos de função somente por HTTPS.|
|serviço de aplicativo|5|Ativar logs de diagnóstico no serviço de aplicativo|Ativar os registros e mantenha-os por até um ano. Isso permite recriar trilhas de atividades para fins de investigação quando ocorre um incidente de segurança ou quando sua rede é comprometida. |
|serviço de aplicativo|10|Depuração remota deve ser desativada para o aplicativo da Web|Desative a depuração para aplicativos da Web se você não precisar mais usá-lo. A depuração remota exige que as portas de entrada estejam abertas em um aplicativo de funções.|
|serviço de aplicativo|10|Depuração remota deve ser desativada para o aplicativo de função|Desative a depuração para o aplicativo de função, se você não precisar mais usá-lo. A depuração remota exige que as portas de entrada estejam abertas em um aplicativo de funções.|
|serviço de aplicativo|10|Configurar restrições de IP para o aplicativo Web|Defina uma lista de endereços IP com permissão para acessar seu aplicativo. O uso de restrições de IP protege um aplicativo Web de ataques comuns.|
|serviço de aplicativo|10|Não permita que todos os recursos ('*') acessem o aplicativo| Não permita o conjunto do parâmetro WEBSITE_LOAD_CERTIFICATES para "". Definir o parâmetro como "" significa que todos os certificados são carregados no armazenamento de certificados pessoais de aplicativos da web. Isso pode levar a abuso do princípio de privilégio mínimo porque é improvável que o site precise de acesso a todos os certificados em tempo de execução.|
|serviço de aplicativo|20|O CORS não deve permitir que todos os recursos acessem seus aplicativos da Web|Permitir que apenas os domínios necessários interajam com seu aplicativo da web. O CORS (compartilhamento de recurso de origem cruzada) não deve permitir que todos os domínios acessem seu aplicativo Web.|
|serviço de aplicativo|20|O CORS não deve permitir o acesso a todos os recursos ao seu aplicativo de funções| Permitir que apenas os domínios necessários interajam com seu aplicativo de função. O CORS (compartilhamento de recurso de origem cruzada) não deve permitir que todos os domínios acessem seu aplicativo de funções.|
|Computar recursos (lote)|1|Configurar regras de alerta de métrica na conta do Lote|Configure as regras de alerta de métrica na conta do Lote e ative as métricas Pool Delete Complete Events e Pool Delete Start Events|
|Recursos de computação (estrutura de serviço)|10|Use o Azure Active Directory para autenticação de cliente no Service Fabric|Realize a autenticação do cliente somente através do Active Directory do Azure no Service Fabric.|
|Recursos de computação (conta de automação)|5| Ativar criptografia da conta de automação|Ativar a criptografia de ativos variáveis da conta de automação ao armazenar dados confidenciais.|
|(Balanceador de carga) de recursos de computação|5|Ativar logs de diagnóstico no Load Balancer|Ativar os registros e mantenha-os por até um ano. Isso permite recriar trilhas de atividades para fins de investigação quando ocorre um incidente de segurança ou quando sua rede é comprometida. |
|Recursos de computação (pesquisa)|5|Ativar logs de diagnóstico no serviço de pesquisa|Ativar os registros e mantenha-os por até um ano. Isso permite recriar trilhas de atividades para fins de investigação quando ocorre um incidente de segurança ou quando sua rede é comprometida. |
|Recursos de computação (barramento de serviço)|5|Ativar logs de diagnóstico no Barramento de Serviço|Ativar os registros e mantenha-os por até um ano. Isso permite recriar trilhas de atividades para fins de investigação quando ocorre um incidente de segurança ou quando sua rede é comprometida. |
|Recursos de computação (análise de fluxo)|5|Ativar logs de diagnóstico no Stream Analytics do Azure|Ativar os registros e mantenha-os por até um ano. Isso permite recriar trilhas de atividades para fins de investigação quando ocorre um incidente de segurança ou quando sua rede é comprometida. |
|Recursos de computação (estrutura de serviço)|5|Ativar logs de diagnóstico no Service Fabric|Ativar os registros e mantenha-os por até um ano. Isso permite recriar trilhas de atividades para fins de investigação quando ocorre um incidente de segurança ou quando sua rede é comprometida. |
|Computar recursos (lote)|5|Ativar logs de diagnóstico em contas em lote|Ativar os registros e mantenha-os por até um ano. Isso permite recriar trilhas de atividades para fins de investigação quando ocorre um incidente de segurança ou quando sua rede é comprometida. |
|Recursos de computação (hub de eventos)|5|Ativar logs de diagnóstico no Hub de Eventos|Ativar os registros e mantenha-os por até um ano. Isso permite recriar trilhas de atividades para fins de investigação quando ocorre um incidente de segurança ou quando sua rede é comprometida. |
|Recursos de computação (aplicativos lógicos)|5|Ativar logs de diagnósticos em aplicativos lógicos|Ativar os registros e mantenha-os por até um ano. Isso permite recriar trilhas de atividades para fins de investigação quando ocorre um incidente de segurança ou quando sua rede é comprometida. |
|Recursos de computação (estrutura de serviço)|15|Defina a propriedade ClusterProtectionLevel para EncryptAndSign no Service Fabric|O Service Fabric fornece três níveis de proteção (Nenhum, Sinal e EncryptAndSign) para comunicação de nó a nó usando um certificado de cluster principal.  Defina o nível de proteção para garantir que todas as mensagens de nó a nó sejam criptografadas e assinadas digitalmente. |
|Recursos de computação (barramento de serviço)|1|Remover todas as regras de autorização, exceto RootManageSharedAccessKey, do namespace do Service Bus |Os clientes do Service Bus não devem usar uma diretiva de acesso no nível do namespace que forneça acesso a todas as filas e tópicos em um namespace. Para alinhar-se ao modelo de segurança com menos privilégios, você deve criar políticas de acesso no nível da entidade para que as filas e os tópicos forneçam acesso somente à entidade específica.|
|Recursos de computação (hub de eventos)|1|Remova todas as regras de autorização, exceto RootManageSharedAccessKey, do namespace Hub de eventos |Os clientes do Hub de Eventos não devem usar uma política de acesso no nível do namespace que forneça acesso a todas as filas e tópicos em um namespace. Para alinhar-se ao modelo de segurança com menos privilégios, você deve criar políticas de acesso no nível da entidade para que as filas e os tópicos forneçam acesso somente à entidade específica.|
|Recursos de computação (hub de eventos)|5|Definir regras de autorização na entidade do Hub de Eventos|Auditar regras de autorização na entidade do Hub de Eventos para conceder acesso com privilégios mínimos.|
|Computador|50|Instale o agente de monitoramento em suas máquinas|Instale o agente de monitoramento para ativar a coleta de dados, a varredura de atualizações, a varredura da linha de base e a proteção do ponto de extremidade em cada máquina.|
|Computador|50|Habilitar o provisionamento automático e coleta de dados para suas assinaturas |Habilite o provisionamento automático e coleta de dados para computadores em suas assinaturas para habilitar a coleta de dados, as atualizações de varredura, linha de base e proteção de ponto de extremidade em cada computador adicionado às suas assinaturas.|
|Computador|40|Resolver problemas de integridade do agente de monitoramento em suas máquinas|Para obter a proteção completa da Central de Segurança, resolva os problemas do agente de monitoramento em suas máquinas seguindo as instruções no guia de Resolução de Problemas.| 
|Computador|40|Resolver problemas de integridade da proteção do endpoint em suas máquinas|Para obter a proteção completa da Central de Segurança, resolva os problemas do agente de monitoramento em suas máquinas seguindo as instruções no guia de solução de problemas.|
|Computador|40|Solucione problemas de dados de varredura ausentes em suas máquinas|Solucione problemas de dados de varredura ausentes em máquinas virtuais e computadores. A falta de dados de varredura em suas máquinas resulta em avaliações de segurança ausentes, como varredura de atualização, varredura de linha de base e varredura de solução de proteção de ponto de extremidade ausente.|
|Computador|40|Instalar atualizações do sistema em suas máquinas|Instale a segurança do sistema ausente e atualizações críticas para proteger suas máquinas virtuais Windows e Linux e computadores
|Computador|15|Adicione um firewall do aplicativo Web| Implemente uma solução WAF (firewall de aplicativo da web) para proteger seus aplicativos da web. |
|Computador|40|Atualize a versão do sistema operacional para suas funções de serviço em nuvem|Atualize a versão do sistema operacional (OS) para suas funções de serviço em nuvem para a versão mais recente disponível para sua família de sistemas operacionais.|
|Computador|35|Corrigir vulnerabilidades na configuração de segurança em suas máquinas|Corrigir vulnerabilidades na configuração de segurança em suas máquinas para protegê-las contra ataques. |
|Computador|35|Corrigir vulnerabilidades na configuração de segurança em seus contêineres|Corrigir vulnerabilidades na configuração de segurança em computadores com o Docker instalado para protegê-los contra ataques.|
|Computador|25|Ativar controles de aplicativos adaptativos|Ative o controle de aplicativos para controlar quais aplicativos podem ser executados em suas VMs localizadas no Azure. Isso ajudará a proteger suas VMs contra malware. O Security Center usa aprendizado de máquina para analisar os aplicativos em execução em cada VM e ajuda você a aplicar regras de permissão usando essa inteligência. Esse recurso simplifica o processo de configuração e manutenção de regras de permissão do aplicativo.|
|Computador|20|Instale a solução de proteção de ponto de extremidade em suas máquinas|Instale uma solução de proteção de ponto de extremidade em suas máquinas virtuais para protegê-las contra ameaças e vulnerabilidades.|
|Computador|20|Reinicie suas máquinas para aplicar atualizações do sistema|Reinicie suas máquinas para aplicar as atualizações do sistema e proteger a máquina contra vulnerabilidades.|
|Computador|15|Aplicar criptografia de disco em suas máquinas virtuais|Criptografe seus discos de máquina virtual usando a Criptografia de Disco do Azure para máquinas virtuais Windows e Linux. O Azure Disk Encryption (ADE) aproveita o recurso BitLocker padrão do setor do Windows eo recurso DM-Crypt do Linux para fornecer criptografia de disco de dados e sistema operacional para ajudar a proteger e proteger seus dados e ajudar a cumprir seus compromissos de conformidade e segurança organizacional no cofre de chaves do Azure do cliente. Quando os requisitos de conformidade e segurança exigirem que você criptografe os dados de ponta a ponta usando suas chaves de criptografia, incluindo a criptografia do disco efêmero (localmente conectado temporariamente), use a criptografia de disco do Azure. Como alternativa, por padrão, os discos gerenciados são criptografados em repouso por padrão, usando a Criptografia do Serviço de Armazenamento do Azure, em que as chaves de criptografia são chaves gerenciadas pela Microsoft no Azure. Se isso atender aos seus requisitos de conformidade e segurança, você poderá aproveitar a criptografia de disco gerenciada padrão para atender aos seus requisitos.|
|Computador|30|Instalar uma solução de avaliação de vulnerabilidades em suas máquinas virtuais|Instalar uma solução de avaliação de vulnerabilidades em suas máquinas virtuais|
|Computador|15|Adicione um firewall do aplicativo Web| Implemente uma solução WAF (firewall de aplicativo da web) para proteger seus aplicativos da web. |
|Computador|30|Corrigir vulnerabilidades usando uma solução de avaliação de vulnerabilidades|As máquinas virtuais para as quais uma solução de terceiros de avaliação de vulnerabilidade é implantada estão sendo continuamente avaliadas em relação às vulnerabilidades do aplicativo e do sistema operacional. Sempre que essas vulnerabilidades forem encontradas, elas estarão disponíveis para mais informações como parte da recomendação.|
|Computador|30|Instalar uma solução de avaliação de vulnerabilidades em suas máquinas virtuais|Instalar uma solução de avaliação de vulnerabilidades em suas máquinas virtuais|
|Computador|1|Migrar máquinas virtuais para novos recursos do Azure Resource Manager|Use o Azure Resource Manager para suas máquinas virtuais para fornecer melhorias de segurança como: controle de acesso mais rígido (RBAC), melhor auditoria, implantação e governança baseadas no Resource Manager, acesso a identidades gerenciadas, acesso ao cofre de chaves para segredos, autenticação baseada no Azure AD e suporte a marcas e grupos de recursos para facilitar o gerenciamento de segurança. |
|Computador|30|Corrigir vulnerabilidades usando uma solução de avaliação de vulnerabilidades|As máquinas virtuais para as quais uma solução de terceiros de avaliação de vulnerabilidade é implantada estão sendo continuamente avaliadas em relação às vulnerabilidades do aplicativo e do sistema operacional. Sempre que essas vulnerabilidades forem encontradas, elas estarão disponíveis para mais informações como parte da recomendação.|

 





## <a name="next-steps"></a>Próximas etapas
Para saber mais sobre as recomendações que se aplicam aos outros tipos de recursos do Azure, consulte o seguinte:


* [Noções básicas sobre as recomendações da Central de Segurança do Azure para máquinas virtuais](security-center-virtual-machine-recommendations.md)
* [Monitorar identidade e acesso na Central de Segurança do Azure](security-center-identity-access.md)
* [Protegendo sua rede na Central de Segurança do Azure](security-center-network-recommendations.md)
* [Protegendo o serviço do SQL Azure na Central de Segurança do Azure](security-center-sql-service-recommendations.md)

Para saber mais sobre a Central de Segurança, confira o seguinte:

* [Configurando políticas de segurança na Central de Segurança do Azure](tutorial-security-policy.md) : saiba como configurar políticas de segurança para suas assinaturas e grupos de recursos do Azure.
* [Gerenciando e respondendo a alertas de segurança na Central de Segurança do Azure](security-center-managing-and-responding-alerts.md) : aprenda a gerenciar e a responder a alertas de segurança.
* [Perguntas frequentes da Central de Segurança do Azure](security-center-faq.md) : encontre as perguntas frequentes sobre como usar o serviço.

