---
title: Criação de tabelas - SQL Data Warehouse do Azure | Microsoft Docs
description: Introdução à criação de tabelas no SQL Data Warehouse do Azure.
services: sql-data-warehouse
author: ronortloff
manager: craigg
ms.service: sql-data-warehouse
ms.topic: conceptual
ms.subservice: implement
ms.date: 04/17/2018
ms.author: rortloff
ms.reviewer: igorstan
ms.openlocfilehash: 290230237a68730a908c6fd0fb0df1d63035b93b
ms.sourcegitcommit: 898b2936e3d6d3a8366cfcccc0fccfdb0fc781b4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/30/2019
ms.locfileid: "55247333"
---
# <a name="designing-tables-in-azure-sql-data-warehouse"></a>Criação de tabelas no SQL Data Warehouse do Azure

Aprenda os conceitos principais para a criação de tabelas no SQL Data Warehouse do Azure. 

## <a name="determine-table-category"></a>Determinar a categoria da tabela 

Um [esquema em estrela](https://en.wikipedia.org/wiki/Star_schema) organiza dados em tabelas de fatos e dimensões. Algumas tabelas são usadas para dados de integração ou de preparo antes de movê-las para uma tabela de fatos ou dimensões. Ao criar uma tabela, decida se os dados da tabela pertencem a uma tabela de integração, de dimensão ou de fato. Essa decisão informa a distribuição e a estrutura da tabela apropriadas. 

- As **Tabelas de fatos** contêm dados quantitativos normalmente gerados em um sistema transacional e, depois, carregados no data warehouse. Por exemplo, uma empresa de varejo gera transações de vendas todos os dias e, em seguida, carrega os dados para uma tabela de fatos do data warehouse para análise.

- As **Tabelas de dimensões** contêm dados de atributo que podem ser alterados, mas essas alterações são raras. Por exemplo, um nome e endereço do cliente são armazenados em uma tabela de dimensões e atualizados somente quando o perfil do cliente é alterado. Para minimizar o tamanho de uma tabela de fatos grande, não deixe o nome e o endereço do cliente em todas as linhas de uma tabela de fatos. Em vez disso, a tabela de fatos e a tabela de dimensões podem compartilhar uma ID do cliente. Uma consulta pode unir as duas tabelas para associar o perfil e as transações de um cliente. 

- As **Tabelas de integrações** oferecem um local para dados de preparo ou integração. Você pode criar uma tabela de integração como uma tabela regular, uma tabela externa ou uma tabela temporária. Por exemplo, é possível carregar dados em uma tabela de preparo, executar transformações nos dados de preparo e, em seguida, inserir os dados em uma tabela de produção.

## <a name="schema-and-table-names"></a>Nomes de tabelas e esquemas
No SQL Data Warehouse, um data warehouse é um tipo de banco de dados. Todas as tabelas no data warehouse estão contidas no mesmo banco de dados.  Você não pode unir tabelas de diversos data warehouses. Esse comportamento é diferente do SQL Server, que oferece suporte a junções entre bancos de dados. 

Em um banco de dados do SQL Server, você pode usar fato, dimensão ou integração nos nomes de esquemas. A migração de um banco de dados do SQL Server para o SQL Data Warehouse funciona melhor se migrar todas as tabelas de fato, dimensão e integração para um esquema no SQL Data Warehouse. Por exemplo, você pode armazenar todas as tabelas do data warehouse de exemplo [WideWorldImportersDW](/sql/sample/world-wide-importers/database-catalog-wwi-olap) em um esquema chamado wwi. O código a seguir cria um [esquema definido pelo usuário](/sql/t-sql/statements/create-schema-transact-sql) chamado wwi.

```sql
CREATE SCHEMA wwi;
```

Para mostrar a organização das tabelas no SQL Data Warehouse, você pode usar fact, dim e int como prefixos para os nomes das tabelas. A tabela a seguir mostra alguns dos nomes de tabelas e esquema para WideWorldImportersDW. Ele compara os nomes no SQL Server com nomes no SQL Data Warehouse. 

| WideWorldImportersDW table  | Tipo de tabela | SQL Server | SQL Data Warehouse |
|:-----|:-----|:------|:-----|
| City | Dimensão | Dimension.City | wwi.DimCity |
| Classificar | Fato | Fact.Order | wwi.FactOrder |


## <a name="table-persistence"></a>Persistência da tabela 

As tabelas armazenam dados permanentemente no Armazenamento do Microsoft Azure, temporariamente no Armazenamento do Microsoft Azure, ou em um armazenamento de dados externo para data warehouse.

### <a name="regular-table"></a>Tabela regular

Uma tabela regular armazena dados no Armazenamento do Microsoft Azure como parte do data warehouse. A tabela e os dados persistem independentemente se há uma sessão aberta.  Este exemplo cria uma tabela regular com duas colunas. 

```sql
CREATE TABLE MyTable (col1 int, col2 int );  
```

### <a name="temporary-table"></a>Tabela temporária
Uma tabela temporária só existe durante a sessão. As tabelas temporárias são boas opções para evitar que outros usuários vejam os resultados temporários, além de reduzirem a necessidade de limpeza.  Como as tabelas temporárias também utilizam o armazenamento local, podem oferecer um desempenho mais rápido para algumas operações.  Para obter mais informações, confira [Tabelas temporárias](sql-data-warehouse-tables-temporary.md).

### <a name="external-table"></a>Tabela externa
Uma tabela externa aponta para dados localizados no Azure Storage Blob ou Azure Data Lake Store. Quando usada em conjunto com a instrução CREATE TABLE AS SELECT, selecionar a partir de uma tabela externa importa dados no SQL Data Warehouse. Ou seja, as tabelas externas são úteis para carregar dados. Para ver um tutorial de carregamento, confira [Usar o PolyBase para carregar dados do Armazenamento de Blobs do Azure](load-data-from-azure-blob-storage-using-polybase.md).

## <a name="data-types"></a>Tipos de dados
O SQL Data Warehouse oferece suporte aos tipos comuns de dados usados. Para obter uma lista dos tipos de dados com suporte, consulte [tipos de dados na referência CREATE TABLE](/sql/t-sql/statements/create-table-azure-sql-data-warehouse#DataTypes) na instrução CREATE TABLE. Minimizar o tamanho dos tipos de dados ajuda a melhorar o desempenho da consulta. Para obter diretrizes sobre o uso dos tipos de dados, consulte [Tipos de dados](sql-data-warehouse-tables-data-types.md).

## <a name="distributed-tables"></a>Tabelas distribuídas
Um recurso fundamental do SQL Data Warehouse é a maneira como ele pode armazenar e operar em tabelas em 60 [distribuições](massively-parallel-processing-mpp-architecture.md#distributions).  As tabelas são distribuídas usando um método de replicação, hash ou round robin.

### <a name="hash-distributed-tables"></a>Tabelas distribuídas em hash
A distribuição hash distribui linhas com base no valor na coluna de distribuição. A tabela de hash distribuída foi projetada para alcançar alto desempenho para junções de consulta em tabelas grandes. Há vários fatores que afetam a escolha da coluna de distribuição. 

Para obter mais informações, consulte [Criação de diretrizes para tabelas distribuídas](sql-data-warehouse-tables-distribute.md).

### <a name="replicated-tables"></a>Tabelas replicadas
Uma tabela replicada possui uma cópia completa da tabela disponível em cada nó de Computação. Consultas de execução rápida em tabelas replicadas como junções em tabelas replicadas não exigem a movimentação de dados. No entanto, a replicação exige armazenamento extra e não é prática para tabelas grandes. 

Para obter mais informações, confira [Criação de diretrizes para tabelas replicadas](design-guidance-for-replicated-tables.md).

### <a name="round-robin-tables"></a>Tabelas round robin
Uma tabela round robin distribui linhas de tabela uniformemente em todas as distribuições. As linhas são distribuídas aleatoriamente. Carregar dados em uma tabela round robin é rápido.  No entanto, as consultas podem exigir mais movimentação de dados que os outros métodos de distribuição. 

Para obter mais informações, consulte [Criação de diretrizes para tabelas distribuídas](sql-data-warehouse-tables-distribute.md).


### <a name="common-distribution-methods-for-tables"></a>Métodos de distribuição comuns para tabelas
A categoria da tabela geralmente determina qual opção escolher para a distribuição da tabela. 

| Categoria de tabela | Opção de distribuição recomendada |
|:---------------|:--------------------|
| Fato           | Use a distribuição de hash com índice columnstore clusterizado. O desempenho melhora quando duas tabelas de hash são unidas na mesma coluna de distribuição. |
| Dimensão      | Use a replicada para tabelas menores. Se as tabelas forem grandes demais para serem armazenadas em cada nó de computação, use a distribuição de hash. |
| Staging        | Use um round robin para a tabela de preparo. A carga com CTAS é rápida. Quando os dados estiverem na tabela de preparo, use INSERT...SELECT para mover os dados para uma tabela de produção. |

## <a name="table-partitions"></a>Partições de tabela
Uma tabela particionada armazena e executa operações nas linhas da tabela de acordo com os intervalos de dados. Por exemplo, uma tabela pode ser particionada por dia, mês ou ano. Você pode melhorar o desempenho de consultas através da eliminação da partição, o que limita a verificação de uma consulta para dados dentro de uma partição. Você também pode manter os dados por meio de alternância de partição. Como os dados no SQL Data Warehouse já foram distribuídos, um número excessivo de partições pode diminuir o desempenho da consulta. Para saber mais informações, confira [Diretrizes de particionamento](sql-data-warehouse-tables-partition.md).

## <a name="columnstore-indexes"></a>Índices ColumnStore
Por padrão, o SQL Data Warehouse armazena uma tabela como um índice columnstore clusterizado. Essa forma de armazenamento de dados atinge a alta compactação de dados e o desempenho de consultas em tabelas grandes.  Normalmente, o índice columnstore clusterizado é a melhor opção, mas existem alguns casos onde um índice clusterizado ou um heap são estruturas de armazenamento mais adequadas.

Para obter uma lista de recursos columnstore, confira [Quais são as novidades dos índices columnstores](/sql/relational-databases/indexes/columnstore-indexes-what-s-new). Para melhorar o desempenho do índice columnstore, confira [Como maximizar a qualidade do rowgroup para índices columnstore](sql-data-warehouse-memory-optimizations-for-columnstore-compression.md).

## <a name="statistics"></a>Estatísticas
O otimizador de consulta usa estatísticas de nível de coluna quando cria o plano para executar uma consulta. Para melhorar o desempenho de consulta, é importante criar estatísticas em colunas individuais, especialmente nas colunas usadas em junções de consulta. Criar e atualizar estatísticas não acontece automaticamente. [Crie estatísticas](/sql/t-sql/statements/create-statistics-transact-sql) depois de criar uma tabela. Atualize as estatísticas depois que um número significativo de linhas for adicionado ou alterado. Por exemplo, atualize as estatísticas depois de uma carga. Para obter mais informações, confira [Diretrizes sobre estatísticas](sql-data-warehouse-tables-statistics.md).

## <a name="commands-for-creating-tables"></a>Comandos para a criação de tabelas
Você pode criar uma tabela como uma nova tabela vazia. Você também pode criar e popular uma tabela com os resultados de uma instrução de seleção. A seguir estão os comandos T-SQL para criar uma tabela.

| Instruções T-SQL | DESCRIÇÃO |
|:----------------|:------------|
| [CREATE TABLE](/sql/t-sql/statements/create-table-azure-sql-data-warehouse) | Cria uma tabela vazia com a definição de todas as opções e colunas da tabela. |
| [CREATE EXTERNAL TABLE](/sql/t-sql/statements/create-external-table-transact-sql) | Cria uma tabela externa. A definição da tabela é armazenada no SQL Data Warehouse. Os dados da tabela são armazenados no Armazenamento de Blobs do Azure ou do Azure Data Lake Store. |
| [CREATE TABLE AS SELECT](/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) | Popula uma tabela nova com os resultados de uma instrução selecionada. Os tipos de dados e colunas de tabela baseiam-se nos resultados da instrução selecionada. Para importar dados, essa instrução pode selecionar de uma tabela externa. |
| [CREATE EXTERNAL TABLE AS SELECT](/sql/t-sql/statements/create-external-table-as-select-transact-sql) | Cria uma tabela externa nova exportando os resultados de uma instrução selecionada para um local externo.  O local é o armazenamento de Blobs do Azure ou o Azure Data Lake Store. |

## <a name="aligning-source-data-with-the-data-warehouse"></a>Como alinhar dados de origem com o data warehouse

As tabelas do data warehouse são populadas pelo carregamento de dados de outra fonte de dados. Para executar um carregamento bem-sucedido, os números e os tipos de dados das colunas na fonte de dados devem se alinhar com a definição da tabela no data warehouse. Obter os dados para alinhar pode ser a parte mais difícil da criação de tabelas. 

Se os dados são provenientes de vários armazenamentos de dados, você pode trazer os dados para o data warehouse e armazená-los em uma tabela de integração. Quando os dados estão na tabela de integração, você pode usar a potência do SQL Data Warehouse para executar operações de transformação. Quando os dados estiverem preparados, será possível inseri-los nas tabelas de produção.

## <a name="unsupported-table-features"></a>Recursos da tabela sem suporte
O SQL Data Warehouse oferece suporte a muitos, mas não a todos, os recursos de tabela oferecidos por outros bancos de dados.  A lista a seguir mostra alguns dos recursos de tabela que não têm suporte no SQL Data Warehouse.

- Chave primária, Chaves estrangeiras, Exclusiva: verifique as [restrições da tabela](/sql/t-sql/statements/alter-table-table-constraint-transact-sql)

- [Colunas Computadas](/sql/t-sql/statements/alter-table-computed-column-definition-transact-sql)
- [Exibições Indexadas](/sql/relational-databases/views/create-indexed-views)
- [Sequência](/sql/t-sql/statements/create-sequence-transact-sql)
- [Colunas Esparsas](/sql/relational-databases/tables/use-sparse-columns)
- Chaves substitutas. Implementar com [identidade](sql-data-warehouse-tables-identity.md).
- [Sinônimos](/sql/t-sql/statements/create-synonym-transact-sql)
- [Gatilhos](/sql/t-sql/statements/create-trigger-transact-sql)
- [Índices Exclusivos](/sql/t-sql/statements/create-index-transact-sql)
- [Tipos Definidos pelo Usuário](/sql/relational-databases/native-client/features/using-user-defined-types)

## <a name="table-size-queries"></a>Consultas do tamanho da tabela
Uma maneira simples de identificar o espaço e as linhas consumidas por uma tabela em cada uma das 60 distribuições é usar [DBCC PDW_SHOWSPACEUSED](/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql).

```sql
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

No entanto, usar comandos DBCC pode ser bastante limitado.  Exibições de gerenciamento dinâmico (DMVs) mostram mais detalhes que os comandos DBCC. Comece criando essa exibição.

```sql
CREATE VIEW dbo.vTableSizes
AS
WITH base
AS
(
SELECT 
 GETDATE()                                                             AS  [execution_time]
, DB_NAME()                                                            AS  [database_name]
, s.name                                                               AS  [schema_name]
, t.name                                                               AS  [table_name]
, QUOTENAME(s.name)+'.'+QUOTENAME(t.name)                              AS  [two_part_name]
, nt.[name]                                                            AS  [node_table_name]
, ROW_NUMBER() OVER(PARTITION BY nt.[name] ORDER BY (SELECT NULL))     AS  [node_table_name_seq]
, tp.[distribution_policy_desc]                                        AS  [distribution_policy_name]
, c.[name]                                                             AS  [distribution_column]
, nt.[distribution_id]                                                 AS  [distribution_id]
, i.[type]                                                             AS  [index_type]
, i.[type_desc]                                                        AS  [index_type_desc]
, nt.[pdw_node_id]                                                     AS  [pdw_node_id]
, pn.[type]                                                            AS  [pdw_node_type]
, pn.[name]                                                            AS  [pdw_node_name]
, di.name                                                              AS  [dist_name]
, di.position                                                          AS  [dist_position]
, nps.[partition_number]                                               AS  [partition_nmbr]
, nps.[reserved_page_count]                                            AS  [reserved_space_page_count]
, nps.[reserved_page_count] - nps.[used_page_count]                    AS  [unused_space_page_count]
, nps.[in_row_data_page_count] 
    + nps.[row_overflow_used_page_count] 
    + nps.[lob_used_page_count]                                        AS  [data_space_page_count]
, nps.[reserved_page_count] 
 - (nps.[reserved_page_count] - nps.[used_page_count]) 
 - ([in_row_data_page_count] 
         + [row_overflow_used_page_count]+[lob_used_page_count])       AS  [index_space_page_count]
, nps.[row_count]                                                      AS  [row_count]
from 
    sys.schemas s
INNER JOIN sys.tables t
    ON s.[schema_id] = t.[schema_id]
INNER JOIN sys.indexes i
    ON  t.[object_id] = i.[object_id]
    AND i.[index_id] <= 1
INNER JOIN sys.pdw_table_distribution_properties tp
    ON t.[object_id] = tp.[object_id]
INNER JOIN sys.pdw_table_mappings tm
    ON t.[object_id] = tm.[object_id]
INNER JOIN sys.pdw_nodes_tables nt
    ON tm.[physical_name] = nt.[name]
INNER JOIN sys.dm_pdw_nodes pn
    ON  nt.[pdw_node_id] = pn.[pdw_node_id]
INNER JOIN sys.pdw_distributions di
    ON  nt.[distribution_id] = di.[distribution_id]
INNER JOIN sys.dm_pdw_nodes_db_partition_stats nps
    ON nt.[object_id] = nps.[object_id]
    AND nt.[pdw_node_id] = nps.[pdw_node_id]
    AND nt.[distribution_id] = nps.[distribution_id]
LEFT OUTER JOIN (select * from sys.pdw_column_distribution_properties where distribution_ordinal = 1) cdp
    ON t.[object_id] = cdp.[object_id]
LEFT OUTER JOIN sys.columns c
    ON cdp.[object_id] = c.[object_id]
    AND cdp.[column_id] = c.[column_id]
)
, size
AS
(
SELECT
   [execution_time]
,  [database_name]
,  [schema_name]
,  [table_name]
,  [two_part_name]
,  [node_table_name]
,  [node_table_name_seq]
,  [distribution_policy_name]
,  [distribution_column]
,  [distribution_id]
,  [index_type]
,  [index_type_desc]
,  [pdw_node_id]
,  [pdw_node_type]
,  [pdw_node_name]
,  [dist_name]
,  [dist_position]
,  [partition_nmbr]
,  [reserved_space_page_count]
,  [unused_space_page_count]
,  [data_space_page_count]
,  [index_space_page_count]
,  [row_count]
,  ([reserved_space_page_count] * 8.0)                                 AS [reserved_space_KB]
,  ([reserved_space_page_count] * 8.0)/1000                            AS [reserved_space_MB]
,  ([reserved_space_page_count] * 8.0)/1000000                         AS [reserved_space_GB]
,  ([reserved_space_page_count] * 8.0)/1000000000                      AS [reserved_space_TB]
,  ([unused_space_page_count]   * 8.0)                                 AS [unused_space_KB]
,  ([unused_space_page_count]   * 8.0)/1000                            AS [unused_space_MB]
,  ([unused_space_page_count]   * 8.0)/1000000                         AS [unused_space_GB]
,  ([unused_space_page_count]   * 8.0)/1000000000                      AS [unused_space_TB]
,  ([data_space_page_count]     * 8.0)                                 AS [data_space_KB]
,  ([data_space_page_count]     * 8.0)/1000                            AS [data_space_MB]
,  ([data_space_page_count]     * 8.0)/1000000                         AS [data_space_GB]
,  ([data_space_page_count]     * 8.0)/1000000000                      AS [data_space_TB]
,  ([index_space_page_count]  * 8.0)                                   AS [index_space_KB]
,  ([index_space_page_count]  * 8.0)/1000                              AS [index_space_MB]
,  ([index_space_page_count]  * 8.0)/1000000                           AS [index_space_GB]
,  ([index_space_page_count]  * 8.0)/1000000000                        AS [index_space_TB]
FROM base
)
SELECT * 
FROM size
;
```

### <a name="table-space-summary"></a>Resumo do espaço da tabela

Esta consulta retorna as linhas e o espaço por tabela.  E permite que você veja quais são as tabelas maiores e se elas são distribuídas em hash, round robin ou replicadas.  Nas tabelas distribuídas em hash, a consulta exibe a coluna de distribuição.  

```sql
SELECT 
     database_name
,    schema_name
,    table_name
,    distribution_policy_name
,      distribution_column
,    index_type_desc
,    COUNT(distinct partition_nmbr) as nbr_partitions
,    SUM(row_count)                 as table_row_count
,    SUM(reserved_space_GB)         as table_reserved_space_GB
,    SUM(data_space_GB)             as table_data_space_GB
,    SUM(index_space_GB)            as table_index_space_GB
,    SUM(unused_space_GB)           as table_unused_space_GB
FROM 
    dbo.vTableSizes
GROUP BY 
     database_name
,    schema_name
,    table_name
,    distribution_policy_name
,      distribution_column
,    index_type_desc
ORDER BY
    table_reserved_space_GB desc
;
```

### <a name="table-space-by-distribution-type"></a>Espaço da tabela pelo tipo de distribuição

```sql
SELECT 
     distribution_policy_name
,    SUM(row_count)                as table_type_row_count
,    SUM(reserved_space_GB)        as table_type_reserved_space_GB
,    SUM(data_space_GB)            as table_type_data_space_GB
,    SUM(index_space_GB)           as table_type_index_space_GB
,    SUM(unused_space_GB)          as table_type_unused_space_GB
FROM dbo.vTableSizes
GROUP BY distribution_policy_name
;
```

### <a name="table-space-by-index-type"></a>Espaço da tabela pelo tipo de índice

```sql
SELECT 
     index_type_desc
,    SUM(row_count)                as table_type_row_count
,    SUM(reserved_space_GB)        as table_type_reserved_space_GB
,    SUM(data_space_GB)            as table_type_data_space_GB
,    SUM(index_space_GB)           as table_type_index_space_GB
,    SUM(unused_space_GB)          as table_type_unused_space_GB
FROM dbo.vTableSizes
GROUP BY index_type_desc
;
```

### <a name="distribution-space-summary"></a>Resumo do espaço de distribuição

```sql
SELECT 
    distribution_id
,    SUM(row_count)                as total_node_distribution_row_count
,    SUM(reserved_space_MB)        as total_node_distribution_reserved_space_MB
,    SUM(data_space_MB)            as total_node_distribution_data_space_MB
,    SUM(index_space_MB)           as total_node_distribution_index_space_MB
,    SUM(unused_space_MB)          as total_node_distribution_unused_space_MB
FROM dbo.vTableSizes
GROUP BY     distribution_id
ORDER BY    distribution_id
;
```

## <a name="next-steps"></a>Próximas etapas
Depois de criar as tabelas para o data warehouse, a próxima etapa é carregar dados na tabela.  Para obter um tutorial de carregamento, consulte [Carregamento de dados no SQL Data Warehouse](load-data-wideworldimportersdw.md).
