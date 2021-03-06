---
title: Replicação transacional com o Banco de Dados SQL do Azure | Microsoft Docs
description: Saiba mais sobre o uso da replicação transacional do SQL Server com bancos de dados autônomos, em pool e em instâncias no Banco de Dados SQL do Azure.
services: sql-database
ms.service: sql-database
ms.subservice: data-movement
ms.custom: ''
ms.devlang: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.reviewer: carlrab
manager: craigg
ms.date: 01/25/2019
ms.openlocfilehash: 1c542c1e906b078b76b78ed30af8bdf67110199c
ms.sourcegitcommit: 359b0b75470ca110d27d641433c197398ec1db38
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/07/2019
ms.locfileid: "55814105"
---
# <a name="transactional-replication-with-standalone-pooled-and-instance-databases-in-azure-sql-database"></a>Replicação transacional do SQL Server com bancos de dados autônomos, em pool e em instâncias no Banco de Dados SQL do Azure

A replicação transacional é um recurso do Banco de Dados SQL do Azure e SQL Server que permite que você replique dados de uma tabela no Banco de Dados SQL do Azure ou un SQL Server para as tabelas localizadas em bancos de dados remotos. Esse recurso permite que você sincronize várias tabelas em bancos de dados diferentes.

## <a name="when-to-use-transactional-replication"></a>Quando usar replicação transacional

A replicação transacional é útil nos seguintes cenários:

- Publique as alterações feitas em uma ou mais tabelas em um banco de dados e distribua-as para um ou vários Bancos de Dados SQL do Azure ou do SQL Server que se inscreveram para as alterações.
- Mantenha vários bancos de dados distribuídos em estado sincronizado.
- Por meio da publicação contínua das alterações, migre bancos de dados de um SQL Server ou Instância Gerenciada para outro banco de dados.

## <a name="overview"></a>Visão geral

Os principais componentes na replicação transacional são mostrados na figura a seguir:  

![replicação com um Banco de Dados SQL](media/replication-to-sql-database/replication-to-sql-database.png)


O **publicador** é uma instância ou um servidor que publica as alterações feitas em algumas tabelas (artigos), enviando as atualizações para o distribuidor. A publicação de um banco de dados SQL do Azure de um SQL Server local é uma ação compatível com as seguintes versões do SQL Server:

   - SQL Server 2019 (versão prévia)
   - SQL Server 2016 para SQL 2017
   - SQL Server 2014 SP1 CU3 ou posterior (12.00.4427)
   - SQL Server 2014 RTM CU10 (12.00.2556)
   - SQL Server 2012 SP3 ou posterior (11.0.6020)
   - SQL Server 2012 SP2 CU8 (11.0.5634.0)
   - Para outras versões do SQL Server que não dão suporte à publicação para objetos no Azure, é possível utilizar o método de [republicação de dados](https://docs.microsoft.com/sql/relational-databases/replication/republish-data) para mover dados para versões mais recentes do SQL Server. 

O **distribuidor** é uma instância ou um servidor que coleta as alterações nos artigos de um publicador e as distribui aos assinantes. O distribuidor pode ser uma Instância Gerenciada do Banco de Dados SQL do Azure ou um SQL Server (qualquer versão, desde que seja igual ou maior do que a versão do publicador). 

O **assinante** é uma instância ou um servidor que está recebendo as alterações feitas no publicador. Os assinantes podem ser bancos de dados autônomos, em pool e em instâncias do Banco de Dados SQL do Azure ou de bancos de dados do SQL Server. Um assinante em um banco de dados autônomo ou em pool precisa ser configurado como um assinante push. 

| Função | Bancos de dados autônomos e em pool | Bancos de dados em instâncias |
| :----| :------------- | :--------------- |
| **Publicador** | Não  | Sim | 
| **Distribuidor** | Não  | Sim|
| **Assinante de pull** | Não  | Sim|
| **Assinante push**| Sim | Sim|
| &nbsp; | &nbsp; | &nbsp; |

Existem diferentes [tipos de replicação](https://docs.microsoft.com/sql/relational-databases/replication/types-of-replication?view=sql-server-2017):


| Replicação | Bancos de dados autônomos e em pool | Bancos de dados em instâncias|
| :----| :------------- | :--------------- |
| [**Transacional**](https://docs.microsoft.com/sql/relational-databases/replication/transactional/transactional-replication) | Sim (somente como assinante) | Sim | 
| [**Instantâneo**](https://docs.microsoft.com/sql/relational-databases/replication/snapshot-replication) | Sim (somente como assinante) | Sim|
| [**Replicação de mesclagem**](https://docs.microsoft.com/sql/relational-databases/replication/merge/merge-replication) | Não  | Não |
| [**Entre pares**](https://docs.microsoft.com/sql/relational-databases/replication/transactional/peer-to-peer-transactional-replication) | Não  | Não |
| **Unidirecional** | Sim | Sim|
| [**Bidirecional**](https://docs.microsoft.com/sql/relational-databases/replication/transactional/bidirectional-transactional-replication) | Não  | Sim|
| [**Assinaturas atualizáveis**](https://docs.microsoft.com/sql/relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication) | Não  | Não |
| &nbsp; | &nbsp; | &nbsp; |

  >[!NOTE]
  > - Tentativa de configurar a replicação usando uma versão mais antiga pode resultar em erro número MSSQL_REPL20084 (o processo não pôde se conectar ao Assinante.) e MSSQL_REPL40532 (não é possível abrir o servidor \<nome> solicitado pelo logon. Houve falha no logon).
  > - Para usar todos os recursos do Banco de Dados SQL do Azure, você deve estar usando as versões mais recentes do [SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) e do [SSDT (SQL Server Data Tools)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt?view=sql-server-2017).

## <a name="requirements"></a>Requisitos

- A conectividade usa Autenticação SQL entre os participantes da replicação. 
- Um compartilhamento da Conta de Armazenamento do Azure para o diretório de trabalho usado pela replicação. 
- A porta 445 (TCP de saída) precisa ser aberta nas regras de segurança de sub-rede da Instância Gerenciada para acessar o compartilhamento de arquivo do Azure. 
- A porta 1433 (TCP de saída) precisará ser aberta se o publicador/distribuidor estiver em uma Instância Gerenciada e o assinante for local. 

## <a name="common-configurations"></a>Configurações comuns

De modo geral, o publicador e o distribuidor devem ambos estar na nuvem ou ser locais. Há suporte para as seguintes configurações: 

### <a name="publisher-with-local-distributor-on-a-managed-instance"></a>Publicador com distribuidor local em uma Instância Gerenciada

![Instância única como publicador e distribuidor ](media/replication-with-sql-database-managed-instance/01-single-instance-asdbmi-pubdist.png)

O publicador e o distribuidor são configurados em uma única Instância Gerenciada e estão distribuindo as alterações para outra Instância Gerenciada, banco de dados individual, banco de dados em pool ou SQL Server, localmente. Nessa configuração, a Instância Gerenciada de publicador/distribuidor não pode ser configurada com [Grupos de failover automático e replicação geográfica](sql-database-auto-failover-group.md).

### <a name="publisher-with-remote-distributor-on-a-managed-instance"></a>Publicador com distribuidor remoto em uma Instância Gerenciada

Nessa configuração, uma Instância Gerenciada publica alterações ao distribuidor localizado em outra Instância Gerenciada que pode atender a muitas Instâncias Gerenciadas de origem e distribuir alterações para um ou mais destinos em Instância Gerenciada, banco de dados individual, banco de dados em pool ou SQL Server.

![Instâncias separadas para publicador e distribuidor](media/replication-with-sql-database-managed-instance/02-separate-instances-asdbmi-pubdist.png)

O publicador e o distribuidor são configurados em duas Instâncias Gerenciadas. Nesta configuração

- As duas Instâncias Gerenciadas estão na mesma vNet.
- As duas Instâncias Gerenciadas estão na mesma localização.
- Instâncias Gerenciadas que hospedam bancos de dados do publicador e do distribuidor não podem [replicados geograficamente usando grupos de failover automático](sql-database-auto-failover-group.md).

### <a name="publisher-and-distributor-on-premises-with-a-subscriber-on-a-standalone-pooled-and-instance-database"></a>Publicador e distribuidor locais com um assinante em um banco de dados autônomo, em pool e em instâncias 

![BD SQL do Azure como assinante](media/replication-with-sql-database-managed-instance/03-azure-sql-db-subscriber.png)
 
Nessa configuração, um Banco de Dados SQL do Azure (banco de dados autônomo, em pool e em instâncias) é um assinante. Essa configuração dá suporte à migração do local para o Azure. Se for um assinante está em um banco de dados autônomo ou um em pool, ele precisa estar no modo de envio por push.  

## <a name="next-steps"></a>Próximas etapas

1. [Configurar a replicação transacional para uma Instância Gerenciada](replication-with-sql-database-managed-instance.md#configure-publishing-and-distribution-example). 
1. [Criar uma publicação](https://docs.microsoft.com/sql/relational-databases/replication/publish/create-a-publication).
1. [Crie uma assinatura push](https://docs.microsoft.com/sql/relational-databases/replication/create-a-push-subscription) usando o nome do servidor de Banco de Dados SQL do Azure como o assinante (por exemplo, `N'azuresqldbdns.database.windows.net` e o nome do Banco de Dados SQL do Azure como o banco de dados de destino (por exemplo, **AdventureWorks**. )


## <a name="see-also"></a>Veja também  

- [Replicação para um Banco de Dados SQL](replication-to-sql-database.md)
- [Replicação para Instância Gerenciada](replication-with-sql-database-managed-instance.md)
- [Criar uma publicação](https://docs.microsoft.com/sql/relational-databases/replication/publish/create-a-publication)
- [Criar uma Assinatura Push](https://docs.microsoft.com/sql/relational-databases/replication/create-a-push-subscription/)
- [Tipos de Replicação](https://docs.microsoft.com/sql/relational-databases/replication/types-of-replication)
- [Monitoramento (Replicação)](https://docs.microsoft.com/sql/relational-databases/replication/monitor/monitoring-replication)
- [Inicializar uma Assinatura](https://docs.microsoft.com/sql/relational-databases/replication/initialize-a-subscription)  
