---
title: Matriz de suporte para recuperação de desastre de VMs VMware e servidores físicos para Azure com Azure Site Recovery | Microsoft Docs
description: Resume os sistemas operacionais e componentes com suporte para recuperação de desastre de VMs VMware e servidor físico para Azure usando o Azure Site Recovery.
author: rayne-wiselman
manager: carmonm
ms.service: site-recovery
services: site-recovery
ms.topic: conceptual
ms.date: 01/18/2019
ms.author: raynew
ms.openlocfilehash: b790cbf6c3c9ec04dfdbf0299e337d32e54e9708
ms.sourcegitcommit: a7331d0cc53805a7d3170c4368862cad0d4f3144
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/30/2019
ms.locfileid: "55299753"
---
# <a name="support-matrix-for-disaster-recovery--of-vmware-vms-and-physical-servers-to-azure"></a>Matriz de suporte para recuperação de desastre de VMs VMware e servidores físicos para o Azure

Este artigo resume os componentes compatíveis e as configurações de recuperação de desastre de VMs da VMware no Azure usando o [Azure Site Recovery](site-recovery-overview.md).

Para começar a usar o Azure Site Recovery com o cenário de implantação mais simples, visite nossos [tutoriais](tutorial-prepare-azure.md). Saiba mais sobre a arquitetura do Azure Site Recovery [aqui](vmware-azure-architecture.md).

## <a name="replication-scenario"></a>Cenário de replicação

**Cenário** | **Detalhes**
--- | ---
VMs VMware | Replicação de VMs VMware locais para Azure. É possível implantar este cenário no portal do Azure ou usando o [PowerShell](vmware-azure-disaster-recovery-powershell.md).
Servidores físicos | Replicação de servidores físicos Windows/Linux locais para Azure. Implante esse cenário no portal do Azure.

## <a name="on-premises-virtualization-servers"></a>Servidores de virtualização locais

**Servidor** | **Requisitos** | **Detalhes**
--- | --- | ---
VMware | vCenter Server 6.7, 6.5, 6.0 ou 5.5 ou vSphere 6.7, 6.5, 6.0 ou 5.5 | Recomendamos o uso de um vCenter Server.<br/><br/> Recomendamos que os hosts vSphere e os servidores vCenter estejam localizados na mesma rede que o servidor de processo. Por padrão, os componentes do servidor de processo executam no servidor de configuração, portanto, essa será a rede na qual você configurará o servidor de configuração, exceto se você configurar um servidor de processo dedicado.
Físico | N/D

## <a name="site-recovery-configuration-server"></a>Servidor de configuração do Azure Site Recovery

O servidor de configuração é um computador local que executa componentes do Site Recovery, incluindo o servidor de configuração, servidor de processo e o servidor de destino mestre. Para replicação de VMware, você configura o servidor de configuração com todos os requisitos, usando um modelo OVF para criar uma VM VMware. Para replicação do servidor físico, você configura o computador do servidor de configuração manualmente.

**Componente** | **Requisitos**
--- |---
Núcleos de CPU | 8
RAM | 16 GB
Número de discos | 3 discos<br/><br/> Os discos incluem o disco do sistema operacional, disco de cache do servidor de processo e a unidade de retenção para failback.
Espaço livre em disco | 600 GB de espaço necessário para cache do servidor de processo.
Espaço livre em disco | 600 GB de espaço necessário para a unidade de retenção.
Sistema operacional  | Windows Server 2012 R2 ou Windows Server 2016 |
Localidade do sistema operacional | Inglês (en-us)
PowerCLI | [PowerCLI 6.0](https://my.vmware.com/web/vmware/details?productId=491&downloadGroup=PCLI600R1 "PowerCLI 6.0") deve estar instalado.
Funções do Windows Server | Não habilite: <br/> - Active Directory Domain Services <br/>- Serviços de Informações da Internet <br/> - Hyper-V |
Políticas de grupo| Não habilite: <br/> - Impedir o acesso ao prompt de comando. <br/> - Impedir o acesso às ferramentas de edição do registro. <br/> - Lógica de confiança para anexos de arquivo. <br/> - Ativar a execução do script. <br/> [Saiba mais](https://technet.microsoft.com/library/gg176671(v=ws.10).aspx)|
IIS | Verifique se você:<br/><br/> - Não tem um site padrão preexistente <br/> - Habilitar [autenticação anônima](https://technet.microsoft.com/library/cc731244(v=ws.10).aspx) <br/> - Habilitar configuração [FastCGI](https://technet.microsoft.com/library/cc753077(v=ws.10).aspx)  <br/> - Não tem site/aplicativo preexistente ouvindo na porta 443<br/>
Tipo de NIC | VMXNET3 (quando implantado como uma VM VMware)
Tipo de endereço IP | estático
Portas | 443 usada para orquestração de canal de controle)<br/>9443 usada para transporte de dados

## <a name="replicated-machines"></a>Computadores replicados

O Site Recovery dá suporte para replicação de qualquer carga de trabalho em execução em um computador com suporte.

**Componente** | **Detalhes**
--- | ---
Configurações do computador | Os computadores que são replicados para o Azure precisam atender aos [requisitos do Azure](#azure-vm-requirements).
Sistema operacional Windows | Windows Server 2016 de 64 bits (Server Core, Server com Desktop Experience), Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 com pelo menos SP1. </br></br>  [Windows Server 2008 com pelo menos o SP2 - 32 e 64 bits](migrate-tutorial-windows-server-2008.md) (somente migração). </br></br> Não há suporte para Windows 2016 Nano Server.
Sistema operacional Linux | Red Hat Enterprise Linux: 5.2 a 5.11<b>\*\*</b>, 6.1 a 6.10<b>\*\*</b>, 7.0 a 7.6 <br/><br/>CentOS: 5.2 a 5.11<b>\*\*</b>, 6.1 a 6.10<b>\*\*</b>, 7.0 a 7.6 <br/><br/>Servidor do Ubuntu 14.04 LTS[ (suporte para versões de kernel)](#ubuntu-kernel-versions)<br/><br/>Servidor LTS do Ubuntu 16.04[ (versões de kernel com suporte)](#ubuntu-kernel-versions)<br/><br/>Debian 7/Debian 8[ (versões de kernel com suporte)](#debian-kernel-versions)<br/><br/>SUSE Linux Enterprise Server 12 SP1,SP2,SP3 [ (versões de kernel com suporte)](#suse-linux-enterprise-server-12-supported-kernel-versions)<br/><br/>SUSE Linux Enterprise Server 11 SP3<b>\*\*</b>, SUSE Linux Enterprise Server 11 SP4 * </br></br>Oracle Linux 6.4, 6.5, 6.6, 6.7, 6.8, 6.9, 6.10, 7.0, 7.1, 7.2, 7.3, 7.4, 7.5 executando o kernel compatível com Red Hat ou o UEK3 (Unbreakable Enterprise Kernel 3) <br/><br/></br>-A atualização de máquinas replicadas do SUSE Linux Enterprise Server 11 SP3 para o SP4 não é suportada. Para atualizar, desabilite a replicação e habilite novamente após a atualização.</br></br> - [Saiba mais](https://support.microsoft.com/help/2941892/support-for-linux-and-open-source-technology-in-azure) sobre suporte para Linux e tecnologia de código aberto no Azure. O Site Recovery orquestra o failover para executar servidores Linux no Azure. No entanto, os fornecedores de Linux podem limitar o suporte a apenas versões de distribuição que não atingiram o fim da vida útil.<br/><br/> - Nas distribuições do Linux, apenas os kernels de ações que fazem parte da distribuição / versão menor da distribuição são suportados.<br/><br/> - A atualização de máquinas protegidas nas principais versões de distribuição do Linux não é suportada. Para atualizar, desabilite a replicação, atualize o sistema operacional e, em seguida, habilite a replicação novamente.<br/><br/> - Os servidores que executam o Red Hat Enterprise Linux 5.2-5.11 ou o CentOS 5.2-5.11 devem ter os [componentes do Linux Integration Services (LIS)](https://www.microsoft.com/download/details.aspx?id=55106) instalados para que as máquinas inicializem no Azure.

### <a name="ubuntu-kernel-versions"></a>Versões de kernel do Ubuntu


**Versão com suporte** | **Serviço de Mobilidade do Azure Site Recovery versão** | **Versão do kernel** |
--- | --- | --- |
14.04 LTS | [9.22][9.22 UR] | 3.13.0-24-generic a 3.13.0-164-generic,<br/>3.16.0-25-generic para 3.16.0-77-generic,<br/>3.19.0-18-generic para 3.19.0-80-generic,<br/>4.2.0-18-generic para 4.2.0-42-generic,<br/>4.4.0-21-generic para 4.4.0-140-generic,<br/>4.15.0-1023-azure a 4.15.0-1036-azure |
14.04 LTS | [9.21][9.21 UR] | 3.13.0-24-generic para 3.13.0-163-generic,<br/>3.16.0-25-generic para 3.16.0-77-generic,<br/>3.19.0-18-generic para 3.19.0-80-generic,<br/>4.2.0-18-generic para 4.2.0-42-generic,<br/>4.4.0-21-generic para 4.4.0-140-generic,<br/>4.15.0-1023-azure para 4.15.0-1035-azure |
14.04 LTS | [9.20][9.20 UR] | 3.13.0-24-generic a 3.13.0-153-generic,<br/>3.16.0-25-generic para 3.16.0-77-generic,<br/>3.19.0-18-generic para 3.19.0-80-generic,<br/>4.2.0-18-generic para 4.2.0-42-generic,<br/>4.4.0-21-generic para 4.4.0-138-generic,<br/>4.15.0-1023-azure para 4.15.0-1025-azure |
14.04 LTS | [9.19][9.19 UR] | 3.13.0-24-generic a 3.13.0-153-generic,<br/>3.16.0-25-generic para 3.16.0-77-generic,<br/>3.19.0-18-generic para 3.19.0-80-generic,<br/>4.2.0-18-generic para 4.2.0-42-generic,<br/>4.4.0-21-generic até 4.4.0-131-generic |
|||
16.04 LTS | [9.22][9.22 UR] | 4.4.0-21-generic para 4.4.0-140-generic,<br/>4.8.0-34-generic a 4.8.0-58-generic,<br/>4.10.0-14-generic para 4.10.0-42-generic,<br/>4.11.0-13-generic para 4.11.0-14-generic,<br/>4.13.0-16-generic a 4.13.0-45-generic,<br/>4.15.0-13-generic a 4.15.0-43-generic<br/>4.11.0-1009-azure para 4.11.0-1016-azure,<br/>4.13.0-1005-azure a 4.13.0-1018-azure <br/>4.15.0-1012-azure a 4.15.0-1036-azure|
16.04 LTS | [9.21][9.21 UR] | 4.4.0-21-generic para 4.4.0-140-generic,<br/>4.8.0-34-generic a 4.8.0-58-generic,<br/>4.10.0-14-generic para 4.10.0-42-generic,<br/>4.11.0-13-generic para 4.11.0-14-generic,<br/>4.13.0-16-generic a 4.13.0-45-generic,<br/>4.15.0-13-generic para 4.15.0-42-generic<br/>4.11.0-1009-azure para 4.11.0-1016-azure,<br/>4.13.0-1005-azure a 4.13.0-1018-azure <br/>4.15.0-1012-azure para 4.15.0-1035-azure|
16.04 LTS | [9.20][9.20 UR] | 4.4.0-21-generic para 4.4.0-138-generic,<br/>4.8.0-34-generic a 4.8.0-58-generic,<br/>4.10.0-14-generic para 4.10.0-42-generic,<br/>4.11.0-13-generic para 4.11.0-14-generic,<br/>4.13.0-16-generic a 4.13.0-45-generic,<br/>4.15.0-13-generic para 4.15.0-38-generic<br/>4.11.0-1009-azure para 4.11.0-1016-azure,<br/>4.13.0-1005-azure a 4.13.0-1018-azure <br/>4.15.0-1012-azure a 4.15.0-1025-azure|
16.04 LTS | [9.19][9.19 UR] | 4.4.0-21-generic até 4.4.0-131-generic,<br/>4.8.0-34-generic a 4.8.0-58-generic,<br/>4.10.0-14-generic para 4.10.0-42-generic,<br/>4.11.0-13-generic para 4.11.0-14-generic,<br/>4.13.0-16-generic a 4.13.0-45-generic,<br/>4.15.0-13-generic até 4.15.0-30-generic<br/>4.11.0-1009-azure para 4.11.0-1016-azure,<br/>4.13.0-1005-azure a 4.13.0-1018-azure <br/>4.15.0-1012-azure até 4.15.0-1019-azure|
16.04 LTS | [9.18][9.18 UR] | 4.4.0-21-generic a 4.4.0-130-generic,<br/>4.8.0-34-generic a 4.8.0-58-generic,<br/>4.10.0-14-generic para 4.10.0-42-generic,<br/>4.11.0-13-generic para 4.11.0-14-generic,<br/>4.13.0-16-generic a 4.13.0-45-generic |

### <a name="debian-kernel-versions"></a>Versões de Kernel do Debian


**Versão com suporte** | **Serviço de Mobilidade do Azure Site Recovery versão** | **Versão do kernel** |
--- | --- | --- |
Debian 7 | [9.18][9.18 UR],[9.19][9.19 UR],[9.20][9.20 UR],[9.21][9.21 UR] | 3.2.0-4-amd64 a 3.2.0-6-amd64, 3.16.0-0.bpo.4-amd64 |
|||
Debian 8 | [9.20][9.20 UR],[9.21][9.21 UR] | 3.16.0-4-amd64 a 3.16.0-7-amd64, 4.9.0-0.bpo.4-amd64 a 4.9.0-0.bpo.8-amd64 |
Debian 8 | [9.19][9.19 UR] | 3.16.0-4-amd64 até 3.16.0-6-amd64, 4.9.0-0.bpo.4-amd64 até 4.9.0-0.bpo.7-amd64 |
Debian 8 | [9.18][9.18 UR] | 3.16.0-4-amd64 a 3.16.0-6-amd64, 4.9.0-0.bpo.4-amd64 a 4.9.0-0.bpo.6-amd64 |


### <a name="suse-linux-enterprise-server-12-supported-kernel-versions"></a>SUSE Linux Enterprise Server 12 versões de kernel com suporte

**Versão** | **Versão de serviço de mobilidade** | **Versão do kernel** |
--- | --- | --- |
SUSE Linux Enterprise Server 12 (SP1,SP2,SP3) | [9.21][9.21 UR] | SP1 3.12.49-11-default a 3.12.74-60.64.40-default</br></br> SP1(LTSS) 3.12.74-60.64.45-default a 3.12.74-60.64.107-default</br></br> SP2 4.4.21-69-default a 4.4.120-92.70-default</br></br>SP2(LTSS) 4.4.121-92.73-default a 4.4.121-92.98-default</br></br>SP3 4.4.73-5-default a 4.4.156-94.72-default |
SUSE Linux Enterprise Server 12 (SP1,SP2,SP3) | [9.20][9.20 UR] | SP1 3.12.49-11-default a 3.12.74-60.64.40-default</br></br> SP1(LTSS) 3.12.74-60.64.45-default a 3.12.74-60.64.107-default</br></br> SP2 4.4.21-69-default a 4.4.120-92.70-default</br></br>SP2(LTSS) 4.4.121-92.73-default a 4.4.121-92.98-default</br></br>SP3 4.4.73-5-default a 4.4.156-94.64-default |
SUSE Linux Enterprise Server 12 (SP1,SP2,SP3) | [9.19][9.19 UR] | SP1 3.12.49-11-default a 3.12.74-60.64.40-default</br></br> SP1(LTSS) 3.12.74-60.64.45-default a 3.12.74-60.64.96-default</br></br> SP2 4.4.21-69-default a 4.4.120-92.70-default</br></br>SP2(LTSS) 4.4.121-92.73-default para 4.4.121-92.85-default</br></br>SP3 4.4.73-5-default até 4.4.140-94.42-default |
SUSE Linux Enterprise Server 12 (SP1,SP2,SP3) | [9.18][9.18 UR] | SP1 3.12.49-11-default a 3.12.74-60.64.40-default</br></br> SP1(LTSS) 3.12.74-60.64.45-default a 3.12.74-60.64.96-default</br></br> SP2 4.4.21-69-default a 4.4.120-92.70-default</br></br>SP2(LTSS) 4.4.121-92.73-default para 4.4.121-92.85-default</br></br>SP3 4.4.73-5-default a 4.4.138-94.39-default |

## <a name="linux-file-systemsguest-storage"></a>Sistemas de arquivos Linux/armazenamento convidado

**Componente** | **Com suporte**
--- | ---
Sistemas de arquivos | ext3, ext4, XFS
Gerenciador de volumes | Antes da [versão 9.20](https://support.microsoft.com/en-in/help/4478871/update-rollup-31-for-azure-site-recovery), <br/> 1. LVM2 é compatível. <br/> 2. Há suporte para o LVM para discos de dados somente. <br/> 3. As VMs do Azure tem apenas um único disco de sistema operacional.<br/><br/>Da [versão 9.20](https://support.microsoft.com/en-in/help/4478871/update-rollup-31-for-azure-site-recovery) em diante, LVM e LVM2 são compatíveis.
Dispositivos de armazenamento paravirtualizados | Não há suporte para dispositivos exportados por drivers paravirtualizados.
Dispositivos de E/S de bloqueio de várias filas | Sem suporte.
Servidores físicos com o controlador de armazenamento CCISS da HP | Sem suporte.
Convenção de nomenclatura de ponto de montagem/dispositivo | O nome do dispositivo ou o nome do ponto de montagem deve ser exclusivo. Assegure que não existam dois pontos de montagem/dispositivos que se diferenciam apenas por maiúsculas e minúsculas. </br> Exemplo: Nomear dois dispositivos da mesma máquina virtual como *dispositivo1* e *Dispositivo1* não é permitido.
Diretórios | Antes da [versão 9.20](https://support.microsoft.com/en-in/help/4478871/update-rollup-31-for-azure-site-recovery), <br/> 1. Os diretórios a seguir (se configurados como partições/sistemas de arquivos separados), precisam estar todos no mesmo disco do sistema operacional no servidor de origem: /(raiz), /boot, /usr, /usr/local, /var, /etc.</br>2. /boot deve estar em uma partição de disco e não ser um volume LVM.<br/><br/> Da [versão 9.20](https://support.microsoft.com/en-in/help/4478871/update-rollup-31-for-azure-site-recovery) em diante, as restrições acima não se aplicam. Não há suporte para /boot no volume LVM em mais de um disco.
Diretório de inicialização | Não há suporte para mais de um disco de inicialização em uma máquina virtual <br/><br/> Um computador sem o disco de inicialização não pode ser protegida

Requisitos de espaço livre de | 2 GB na/partição raiz <br/><br/> 250 MB na pasta de instalação XFSv5 | Recursos XFSv5 em sistemas de arquivos XFS, como a soma de verificação dos metadados, têm suporte do Serviço de Mobilidade versão 9.10 em diante. Use o utilitário xfs_info para verificar o superbloco XFS da partição. Se ftype é definido como 1, isso indica que os recursos do XFSv5 estão sendo usados.

## <a name="vmdisk-management"></a>Gerenciamento de VM/disco

**Ação** | **Detalhes**
--- | ---
Redimensionar o disco na VM replicada |  Com suporte.
Adicionar disco na VM replicada | Desabilitar a replicação para a VM, adicionar o disco e, em seguida, reabilitar a replicação. Adição de um disco em uma máquina virtual de replicação não é suportado atualmente.

## <a name="network"></a>Rede

**Componente** | **Com suporte**
--- | ---
Agrupamento NIC da rede do host | Compatível com VMs da VMware. <br/><br/>Sem suporte para a replicação de computador físico.
VLAN da rede do host | Sim.
IPv4 da rede do host | Sim.
IPv6 da rede do host |  Não.
Agrupamento NIC da rede do convidado/servidor |  Não.
IPv4 da rede do convidado/servidor | Sim.
IPv6 da rede do convidado/servidor |  Não.
IP estático da rede do convidado/servidor (Windows) | Sim.
IP estático da rede do convidado/servidor (Linux) | Sim. <br/><br/>As VMs são configuradas para usar o DHCP no failback.
Várias NICs da rede do convidado/servidor | Sim.


## <a name="azure-vm-network-after-failover"></a>Rede VM do Azure (após o failover)

**Componente** | **Com suporte**
--- | ---
Azure ExpressRoute | SIM
ILB | SIM
ELB | SIM
Gerenciador de Tráfego do Azure | SIM
NIC múltipla | SIM
Endereço IP Reservado | SIM
IPv4 | SIM
Manter endereço IP de origem | SIM
Pontos de extremidade de serviço de Rede Virtual do Azure<br/> (sem Firewalls de Armazenamento do Azure) | SIM
Rede Acelerada | Não 

## <a name="storage"></a>Armazenamento
**Componente** | **Com suporte**
--- | ---
Dados dinâmicos | O disco do Sistema Operacional precisa ser um disco básico. <br/><br/>Os discos de Dados podem ser discos dinâmicos
NFS do host | Sim para VMware<br/><br/> Não para servidores físicos
Host SAN iSCSI/FC) | SIM
Host vSAN | Sim para VMware<br/><br/> N/D para servidores físicos
MPIO (Múltiplos caminhos) do host | Sim, testado com Microsoft DSM, EMC PowerPath 5.7 SP4, EMC PowerPath DSM for CLARiiON
Volumes de host Virtual (VVols) | Sim para VMware<br/><br/> N/D para servidores físicos
VMDK do convidado/servidor | SIM
EFI/UEFI do convidado/servidor| Parcial (migração para o Azure para Windows Server 2012 e posterior) <br/><br/> Consulte a observação ao final da tabela
Disco de cluster compartilhado do convidado/servidor | Não 
Disco criptografado do convidado/servidor | Não 
NFS do convidado/servidor | Não 
SMB 3.0 do convidado/servidor | Não 
RDM do convidado/servidor | SIM<br/><br/> N/D para servidores físicos
Disco do convidado/servidor > 1 TB | SIM<br/><br/>Até 4.095 GB<br/><br/> O disco deve ser maior que 1024 MB.
Disco do convidado/servidor com tamanho de setor lógico e físico de 4.000 cada | SIM
Disco do convidado/servidor com tamanho de setor lógico de 4.000 e físico de 512 bytes | SIM
Volume do convidado/servidor com discos distribuídos >4 TB <br/><br/>Gerenciamento de volumes lógicos (LVM)| SIM
Convidado/servidor - espaços de armazenamento | Não 
Adicionar/remover disco a quente por convidado/servidor | Não 
Convidado/servidor - excluir disco | SIM
MPIO (Múltiplos caminhos) de convidado/servidor | Não 

> [!NOTE]
> Máquinas virtuais da VMware com inicialização UEFI com Windows Server 2012 ou posterior podem ser migrados para o Azure. As restrições a seguir se aplicam:

> - Há suporte apenas para a migração para o Azure. O failback não é compatível com o site do VMware local.
> - O servidor não deve ter mais de quatro partições no disco do sistema operacional.
> - Exige o Serviço de Mobilidade versão 9.13 ou posterior.

## <a name="azure-storage"></a>Armazenamento do Azure

**Componente** | **Com suporte**
--- | ---
Armazenamento com redundância local | SIM
Armazenamento com redundância geográfica | SIM
Armazenamento com redundância geográfica com acesso de leitura | SIM
Armazenamento frio | Não 
Armazenamento quente| Não 
Blobs de bloco | Não 
Criptografia em repouso (Criptografia do Serviço de Armazenamento)| SIM
Armazenamento Premium | SIM
Serviço de importação/exportação | Não 
Firewalls de armazenamento do Azure para redes virtuais configurados na conta de armazenamento de cache/armazenamento de destino (usada para armazenar dados de replicação) | Não 
Contas de armazenamento v2 de uso geral (camadas hot e cool) | Não 

## <a name="azure-compute"></a>Computação do Azure

**Recurso** | **Com suporte**
--- | ---
Conjuntos de disponibilidade | SIM
HUB | SIM
Discos gerenciados | SIM

## <a name="azure-vm-requirements"></a>Requisitos de VM do Azure

VMs locais que são replicados para o Azure devem atender aos requisitos de VM do Azure resumidos nesta tabela. Quando o Site Recovery executar uma verificação de pré-requisitos, ele irá falhar se alguns dos requisitos não forem atendidos.

**Componente** | **Requisitos** | **Detalhes**
--- | --- | ---
Sistema operacional convidado | Verificar [sistemas operacionais com suporte](#replicated-machines) para computadores replicados. | A verificação falha se não tiver suporte.
Arquitetura do sistema operacional convidado | 64 bits. | A verificação falha se não tiver suporte.
Tamanho do disco do sistema operacional | Até 2.048 GB. | A verificação falha se não tiver suporte.
Contagem do disco do sistema operacional | 1 | A verificação falha se não tiver suporte.
Contagem de disco de dados | 64 ou menos. | A verificação falha se não tiver suporte.
Tamanho do disco de dados | Até 4.095 GB | A verificação falha se não tiver suporte.
Adaptadores de rede | Há suporte para vários adaptadores. |
VHD compartilhado | Sem suporte. | A verificação falha se não tiver suporte.
Disco FC | Sem suporte. | A verificação falha se não tiver suporte.
BitLocker | Sem suporte. | O BitLocker precisa ser desabilitado antes de habilitar a replicação em um computador. |
Nome da VM | De 1 a 63 caracteres.<br/><br/> Restrito a letras, números e hifens.<br/><br/> O nome do computador precisa começar e terminar com uma letra ou um número. |  Atualize o valor nas propriedades do computador no Site Recovery.


## <a name="vault-tasks"></a>Tarefas do Vault

**Ação** | **Com suporte**
--- | ---
Mover cofre entre grupos de recursos<br/><br/> Dentro e entre as assinaturas | Não 
Mover armazenamento, rede, VMs do Azure entre grupos de recursos<br/><br/> Dentro e entre as assinaturas | Não 


## <a name="download-latest-azure-site-recovery-components"></a>Baixe os últimos componentes do Azure Site Recovery

**Nome** | **Descrição** | **Instruções de download da última versão**
--- | --- | --- | --- | ---
Servidor de configuração | Coordena as comunicações entre servidores VMware locais e o Azure  <br/><br/>  Instalado nos servidores VMware no locais | Para a nova instalação, clique [aqui](vmware-azure-deploy-configuration-server.md). Para atualizar o componente existente para a última versão, clique [aqui](vmware-azure-manage-configuration-server.md#upgrade-the-configuration-server).
Servidor de processo|Instalado por padrão no servidor de configuração. Recebe dados de replicação, otimiza-os com caching, compactação e criptografia e os envia para o Armazenamento do Microsoft Azure. À medida que a implantação cresce, você pode adicionar outros servidores de processo separados para lidar com volumes maiores de tráfego de replicação.| Para a nova instalação, clique [aqui](vmware-azure-set-up-process-server-scale.md). Para atualizar o componente existente para a última versão, clique [aqui](vmware-azure-manage-process-server.md#upgrade-a-process-server).
Serviço de Mobilidade | Coordena a replicação entre servidores VMware/servidores físicos locais e o Azure/site secundário<br/><br/> Instalado na VM VMware ou nos servidores físicos que você deseja replicar | Para a nova instalação, clique [aqui](vmware-azure-install-mobility-service.md). Para atualizar o componente existente para a última versão, clique [aqui](vmware-physical-mobility-service-overview.md#update-the-mobility-service).

Para saber mais sobre os últimos recursos e correções, clique [aqui](https://aka.ms/ASR_latest_release_notes).


## <a name="next-steps"></a>Próximas etapas
[Saiba como](tutorial-prepare-azure.md) para preparar o Azure para recuperação de desastres de máquinas virtuais da VMware.

[9.22 UR]: https://support.microsoft.com/help/4485985/update-rollup-32-for-azure-site-recovery
[9.21 UR]: https://support.microsoft.com/help/4485985/update-rollup-32-for-azure-site-recovery
[9.20 UR]: https://support.microsoft.com/help/4478871/update-rollup-31-for-azure-site-recovery
[9.19 UR]: https://support.microsoft.com/help/4468181/azure-site-recovery-update-rollup-30
[9.18 UR]: https://support.microsoft.com/help/4466466/update-rollup-29-for-azure-site-recovery
