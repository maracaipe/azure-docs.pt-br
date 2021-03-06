---
title: Planejando uma implantação de Arquivos do Azure | Microsoft Docs
description: Saiba o que considerar ao planejar uma implantação de Arquivos do Azure.
services: storage
author: wmgries
ms.service: storage
ms.topic: article
ms.date: 06/12/2018
ms.author: wgries
ms.subservice: files
ms.openlocfilehash: 69ca9474c613752b98efa6bb236919508a2fe430
ms.sourcegitcommit: 039263ff6271f318b471c4bf3dbc4b72659658ec
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2019
ms.locfileid: "55753683"
---
# <a name="planning-for-an-azure-files-deployment"></a>Planejando uma implantação de Arquivos do Azure
O [Arquivos do Azure](storage-files-introduction.md) oferece compartilhamentos de arquivos totalmente gerenciados na nuvem, acessíveis por meio do protocolo SMB padrão no setor. Já que o Arquivos do Azure é totalmente gerenciado, implantá-lo em cenários de produção é muito mais fácil do que implantar e gerenciar um servidor de arquivos ou um dispositivo NAS. Este artigo aborda os tópicos a serem considerados ao implantar um compartilhamento de Arquivos do Azure para uso em produção dentro de sua organização.

## <a name="management-concepts"></a>Conceitos de gerenciamento
 O diagrama a seguir ilustra as construções do gerenciamento do Arquivos do Azure:

![Estrutura do Arquivo](./media/storage-files-introduction/files-concepts.png)

* **Conta de Armazenamento**: Todo o acesso ao Armazenamento do Azure ocorre por meio de uma conta de armazenamento. Consulte [Escalabilidade e Metas de Desempenho](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json) para obter detalhes sobre a capacidade da conta de armazenamento.

* **Compartilhamento**: Um compartilhamento do Armazenamento de Arquivos é um compartilhamento de arquivo SMB no Azure. Todos os arquivos e diretórios devem ser criados em um compartilhamento pai. Uma conta pode conter um número ilimitado de compartilhamentos e um compartilhamento pode armazenar um número ilimitado de arquivos, até a capacidade total de 5 TiB do compartilhamento de arquivos.

* **Diretório**: Uma hierarquia opcional de diretórios.

* **Arquivo**: Um arquivo no compartilhamento. Um arquivo pode ter até 1 TiB de tamanho.

* **Formato de URL**: Para solicitações a um compartilhamento de arquivo do Azure feitas com o protocolo REST de Arquivo, os arquivos são endereçáveis usando o seguinte formato de URL:

    ```
    https://<storage account>.file.core.windows.net/<share>/<directory>/<file>
    ```

## <a name="data-access-method"></a>Método de acesso a dados
O Arquivos do Azure oferece dois métodos de acesso a dados internos e práticos, que você pode usar separadamente ou combinados entre si para acessar seus dados:

1. **Acesso direto à nuvem**: Qualquer compartilhamento de arquivo do Azure pode ser montado por [Windows](storage-how-to-use-files-windows.md), [macOS](storage-how-to-use-files-mac.md) e/ou [Linux](storage-how-to-use-files-linux.md) com o protocolo SMB padrão do setor ou por meio da API REST de Arquivo. Com o SMB, leituras e gravações para arquivos no compartilhamento são feitas diretamente no compartilhamento de arquivos no Azure. Para montar uma VM no Azure, o cliente SMB no sistema operacional deve dar suporte ao menos ao SMB 2.1. Para montar localmente, por exemplo, na estação de trabalho do usuário, o cliente SMB com suporte pela estação de trabalho deverá, por sua vez, dar suporte ao menos ao SMB 3.0 (com criptografia). Além de SMB, novos aplicativos ou serviços podem acessar diretamente o compartilhamento de arquivos por meio de REST de Arquivo, que fornece uma interface de programação de aplicativo fácil e escalonável para desenvolvimento de software.
2. **Sincronização de Arquivos do Azure**: Com a Sincronização de Arquivos do Azure, os compartilhamentos podem ser replicados para Servidores Windows locais ou no Azure. Seus usuários acessariam o compartilhamento de arquivos por meio do Windows Server, por exemplo, por meio de um compartilhamento NFS ou SMB. Isso é útil para cenários nos quais os dados serão acessados e modificados longe de um datacenter do Azure, como em um cenário de filial. Os dados podem ser replicados entre vários pontos de extremidade do Windows Server, por exemplo, entre várias filiais. Finalmente, dados podem ser divididos em camadas para arquivos do Azure, de modo que todos os dados ainda serão acessíveis por meio do servidor, mas ele não terá uma cópia completa dos dados. Em vez disso, os dados são recuperados diretamente quando abertos pelo usuário.

A tabela a seguir ilustra como os usuários e aplicativos podem acessar o compartilhamento de Arquivos do Azure:

| | Acesso direto à nuvem | Sincronização de Arquivos do Azure |
|------------------------|------------|-----------------|
| Quais protocolos você precisa usar? | O Arquivos do Azure dá suporte a SMB 2.1, a SMB 3.0 e à API REST de arquivo. | Acessar o compartilhamento de arquivos do Azure por meio de qualquer protocolo com suporte no Windows Server (SMB, NFS, FTPS, etc.) |  
| Onde você está executando a carga de trabalho? | **No Azure**: Os Arquivos do Azure oferecem acesso direto aos seus dados. | **Localmente, com rede lenta**: Clientes Windows, Linux e macOS podem montar um compartilhamento de arquivo do Windows local localmente como um cache rápido do seu compartilhamento de arquivo do Azure. |
| De que nível de ACLs você precisa? | Nível de compartilhamento e de arquivo. | Nível de compartilhamento, de arquivo e de usuário. |

## <a name="data-security"></a>Segurança de dados
O Arquivos do Azure tem várias opções integradas para garantir a segurança dos dados:

* Suporte para criptografia em ambos os protocolos over-the-wire: Criptografia SMB 3.0 e REST de Arquivo via HTTPS. Por padrão: 
    * Os clientes que dão suporte a criptografia SMB 3.0 enviam e recebem dados por um canal criptografado.
    * Os clientes que não dão suporte ao SMB 3.0 com criptografia podem se comunicar no interior do datacenter via SMB 2.1 ou SMB 3.0, sem criptografia. Os clientes do SMB não têm permissão para se comunicar no interior do datacenter via SMB 2.1 ou SMB 3.0 sem criptografia.
    * Os clientes podem se comunicar por REST de arquivo via HTTP ou HTTPS.
* Criptografia em repouso ([Criptografia do Serviço de Armazenamento do Azure](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)): A SSE (Criptografia do Serviço de Armazenamento) está habilitada para todas as contas de armazenamento. Os dados em repouso são criptografados com chaves totalmente gerenciadas. Criptografia em repouso não aumenta os custos de armazenamento nem reduz o desempenho. 
* Requisito opcional de dados criptografados em trânsito: quando selecionado, o Arquivos do Azure rejeitam o acesso aos dados por canais sem criptografia. Especificamente, são permitidas somente HTTPS e SMB 3.0 com conexões de criptografia. 

    > [!Important]  
    > A exigência de transferência segura de dados fará com que clientes SMB mais antigos não sejam capazes de se comunicar com o SMB 3.0 com criptografia. Para obter mais informações, consulte [Montar no Windows](storage-how-to-use-files-windows.md), [Montar no Linux](storage-how-to-use-files-linux.md) e [Montar no macOS](storage-how-to-use-files-mac.md).

Para segurança máxima, recomendamos habilitar ambas a criptografia em repouso e a criptografia de dados em trânsito sempre que você estiver usando clientes modernos para acessar seus dados. Por exemplo, se você precisa montar um compartilhamento em uma VM Windows Server 2008 R2, que só dá suporte a SMB 2.1, você precisa permitir tráfego não criptografado para sua conta de armazenamento, já que o SMB 2.1 não dá suporte a criptografia.

Se você estiver usando a Sincronização de Arquivos do Azure para acessar o compartilhamento de Arquivos do Azure, usaremos sempre HTTPS e SMB 3.0 com criptografia para sincronizar seus dados aos Windows Servers, independentemente de você exigir ou não criptografia de dados em repouso.

## <a name="file-share-performance-tiers"></a>Níveis de desempenho do compartilhamento de arquivos
Os arquivos do Azure dão suporte a dois níveis de desempenho: Standard e Premium.

* Os **compartilhamentos de arquivos padrão** contam com HDDs (unidades de disco rígido) rotacionais que fornecem um desempenho confiável para as cargas de trabalho de E/S que são menos sensíveis à variabilidade de desempenho, como os compartilhamentos de arquivos de finalidade geral e os ambientes de desenvolvimento/teste. Os compartilhamentos de arquivos padrão estão disponíveis apenas em um modelo de cobrança pago conforme o uso.
* Os **compartilhamentos de arquivos Premium (versão prévia)** contam com SSDs (discos de estado sólido) que fornecem alto desempenho consistente e baixa latência, em milissegundos de dígito único para a maioria das operações de E/S e para as cargas de E/S mais intensivas. Isso os torna adequados para uma ampla variedade de cargas de trabalho, como bancos de dados, hospedagem de websites, ambientes de desenvolvimento, etc. Os compartilhamentos de arquivos Premium estão disponíveis em um modelo de cobrança provisionado.

### <a name="provisioned-shares"></a>Compartilhamentos provisionados
Os compartilhamentos de arquivos Premium são provisionados com base em uma taxa de GiB/IOPS/transferência fixa. Para cada GiB provisionado, o compartilhamento emitirá um IOPS e uma taxa de transferência de 0,1 MiB/s até os limites máximos por compartilhamento. O provisionamento mínimo permitido é de 100 GiB, com um IOPS e uma taxa de transferência mínimos. O tamanho do compartilhamento pode ser aumentado a qualquer momento, mas pode ser reduzido uma vez a cada 24 horas desde a última expansão.

Com base no melhor esforço, todos os compartilhamentos poderão acumular até três IOPS por GiB de armazenamento provisionado por 60 minutos ou mais, dependendo do tamanho do compartilhamento. Os novos compartilhamentos começam com o crédito de intermitência completa com base na capacidade provisionada.

| Capacidade provisionada | 100 GiB | 500 GiB | 1 TiB | 5 TiB | 
|----------------------|---------|---------|-------|-------|
| IOPS de linha de base | 100 | 500 | 1.024 | 5.120 | 
| Limite de intermitência | 300 | 1.500 | 3.072 | 15.360 | 
| Produtividade | 110 MiB/segundo | 150 MiB/segundo | 202 MiB/segundo | 612 MiB/segundo |

## <a name="file-share-redundancy"></a>Redundância de compartilhamento de arquivo
Os arquivos do Azure oferecem suporte a três opções de redundância de dados: armazenamento localmente redundante (LRS), armazenamento com redundância de zona (ZRS) e armazenamento com redundância geográfica (GRS). As seções a seguir descrevem as diferenças entre as opções de redundância diferentes:

### <a name="locally-redundant-storage"></a>Armazenamento com redundância local
[!INCLUDE [storage-common-redundancy-LRS](../../../includes/storage-common-redundancy-LRS.md)]

### <a name="zone-redundant-storage"></a>Armazenamento com redundância de zona
[!INCLUDE [storage-common-redundancy-ZRS](../../../includes/storage-common-redundancy-ZRS.md)]

### <a name="geo-redundant-storage"></a>Armazenamento com redundância geográfica
> [!Warning]  
> Se estiver usando o compartilhamento de arquivos do Azure como um ponto de extremidade de nuvem em uma conta de armazenamento GRS, você não deve iniciar o failover da conta de armazenamento. Se isso for feito, a sincronização deixará de funcionar e poderá causar a perda inesperada de dados no caso de arquivos recentes em camadas. No caso de perda de uma região do Azure, a Microsoft disparará o failover da conta de armazenamento de modo que seja compatível com a Sincronização de Arquivos do Azure.

[!INCLUDE [storage-common-redundancy-GRS](../../../includes/storage-common-redundancy-GRS.md)]

## <a name="data-growth-pattern"></a>Padrão de crescimento de dados
Atualmente, o tamanho máximo de um compartilhamento de arquivos do Azure é de 5 TiB. Devido a essa limitação atual, você deve considerar o crescimento esperado dos dados durante a implantação de um compartilhamento de Arquivos do Azure. 

É possível sincronizar vários compartilhamentos de arquivos do Azure em um único Servidor de Arquivos do Windows com a Sincronização de Arquivos do Azure. Isso lhe assegura que os compartilhamentos de arquivos mais antigos e maiores, que talvez você tenha localmente, poderão ser transferidos para a Sincronização de Arquivos do Azure. Para obter mais informações, veja [Planejando uma implantação da Sincronização de Arquivos do Azure](storage-files-planning.md).

## <a name="data-transfer-method"></a>Método de transferência de dados
Há muitas opções fáceis para transferência de dados em massa de um arquivo de compartilhamento existente, tal como um compartilhamento de arquivos local, para o Arquivos do Azure. Alguns populares incluem (lista não exaustiva):

* **Sincronização de Arquivos do Azure**: Como parte de uma primeira sincronização entre um compartilhamento de arquivo do Azure (um "Ponto de Extremidade da Nuvem") e um namespace de diretório do Windows (um "Ponto de Extremidade de Servidor"), a Sincronização de Arquivos do Azure replicará todos os dados do compartilhamento de arquivo existente para o Arquivos do Azure.
* **[Importação/Exportação do Azure](../common/storage-import-export-service.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)**: O serviço de importação/exportação do Azure permite a transferência de grandes quantidades de dados com segurança em um compartilhamento de arquivos do Azure pelo envio de discos rígidos para um datacenter do Azure. 
* **[Robocopy](https://technet.microsoft.com/library/cc733145.aspx)**: Robocopy é uma ferramenta de cópia bem conhecida que é fornecida com o Windows e o Windows Server. Robocopy pode ser usado para transferir dados para arquivos do Azure montando o compartilhamento de arquivos localmente e, em seguida, usando a localização montada como o destino no comando Robocopy.
* **[AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#upload-files-to-an-azure-file-share)**: O AzCopy é um utilitário de linha de comando projetado para copiar dados de e para os Arquivos do Azure e o Armazenamento de Blobs do Azure, usando comandos simples com o desempenho ideal. O AzCopy está disponível para Windows, Mac e Linux.

## <a name="next-steps"></a>Próximas etapas
* [Planejando uma implantação da Sincronização de Arquivos do Azure](storage-sync-files-planning.md)
* [Implantando Arquivos do Azure](storage-files-deployment-guide.md)
* [Implantando a Sincronização de Arquivos do Azure](storage-sync-files-deployment-guide.md)
