---
title: Usar modelos do Azure para criar HDInsight com Azure Data Lake Storage Gen1 | Microsoft Docs
description: Use os modelos do Azure Resource Manager para criar e usar clusters HDInsight com Azure Data Lake Storage Gen1
services: data-lake-store,hdinsight
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8ef8152f-2121-461e-956c-51c55144919d
ms.service: data-lake-store
ms.devlang: na
ms.topic: conceptual
ms.date: 05/29/2018
ms.author: nitinme
ms.openlocfilehash: e08e7ae0a97b206a692dd47e91c4c94847cb9833
ms.sourcegitcommit: de81b3fe220562a25c1aa74ff3aa9bdc214ddd65
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/13/2019
ms.locfileid: "56235165"
---
# <a name="create-an-hdinsight-cluster-with-azure-data-lake-storage-gen1-using-azure-resource-manager-template"></a>Criar um cluster HDInsight com Azure Data Lake Storage Gen1 usando o modelo do Azure Resource Manager
> [!div class="op_single_selector"]
> * [Usando o Portal](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Usando o PowerShell (para o armazenamento padrão)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Usando o PowerShell (para o armazenamento adicional)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Usando o Gerenciador de Recursos](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

Saiba como usar o Azure PowerShell para configurar um cluster HDInsight com Azure Data Lake Storage Gen1, **como armazenamento adicional**.

Para tipos de cluster com suporte, o Data Lake Storage Gen1 pode ser usado como armazenamento padrão ou conta de armazenamento adicional. Quando o Data Lake Storage Gen1 é usado como armazenamento adicional, a conta de armazenamento padrão para os clusters ainda será Azure Storage Blobs (WASB) e os arquivos relacionados ao cluster (como logs, etc.) ainda serão gravados no armazenamento padrão, enquanto os dados que você quer processar podem ser armazenados em uma conta do Data Lake Storage Gen1. Usar o Data Lake Storage Gen1 como uma conta de armazenamento adicional não afeta o desempenho nem a capacidade de leitura/gravação no armazenamento do cluster.

## <a name="using-data-lake-storage-gen1-for-hdinsight-cluster-storage"></a>Usar o Data Lake Storage Gen1 para armazenamento de cluster HDInsight

Aqui estão algumas considerações importantes para usar HDInsight com Data Lake Storage Gen1:

* A opção para criar clusters HDInsight com acesso ao Data Lake Storage Gen1 como armazenamento padrão está disponível para as versões 3.5 e 3.6 do HDInsight.

* A opção para criar clusters HDInsight com acesso ao Data Lake Storage Gen1 como armazenamento adicional está disponível para as versões 3.2, 3.4, 3.5 e 3.6 do HDInsight.

Neste artigo, provisionamos um cluster Hadoop com o Data Lake Storage Gen1 como armazenamento adicional. Para obter instruções sobre como criar um cluster Hadoop com Data Lake Storage Gen1 como armazenamento padrão, consulte [Criar um cluster HDInsight com Data Lake Storage Gen1 usando o portal do Azure](data-lake-store-hdinsight-hadoop-use-portal.md).

## <a name="prerequisites"></a>Pré-requisitos

[!INCLUDE [updated-for-az](../../includes/updated-for-az.md)]

Antes de começar este tutorial, você deve ter o seguinte:

* **Uma assinatura do Azure**. Consulte [Obter a avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Azure PowerShell 1.0 ou superior**. Consulte [Como instalar e configurar o PowerShell do Azure](/powershell/azure/overview).
* **Entidade de serviço do Azure Active Directory**. As etapas neste tutorial fornecem instruções sobre como criar uma entidade de serviço no Azure AD. No entanto, você deve ser administrador do Azure AD para poder criar uma entidade de serviço. Se você for administrador do Azure AD, poderá ignorar esse pré-requisito e continuar com o tutorial.

    **Se você não for um administrador do Azure AD**, não poderá executar as etapas necessárias para criar uma entidade de serviço. Nesse caso, o administrador do Azure AD primeiro deve criar uma entidade de serviço antes de criar um cluster HDInsight com Data Lake Storage Gen1. Além disso, a entidade de serviço deve ser criada usando um certificado, conforme descrito em [Criar uma entidade de serviço com certificado](../active-directory/develop/howto-authenticate-service-principal-powershell.md#create-service-principal-with-certificate-from-certificate-authority).

## <a name="create-an-hdinsight-cluster-with-data-lake-storage-gen1"></a>Criar um cluster HDInsight com Data Lake Storage Gen1
O modelo do Resource Manager e os pré-requisitos para usar o modelo estão disponíveis no GitHub em [Implantar um cluster HDInsight Linux com o novo Data Lake Storage Gen1](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage). Siga as instruções fornecidas neste link para criar um cluster HDInsight com Data Lake Storage Gen1 como o armazenamento adicional.

As instruções no link mencionado acima exigem o PowerShell. Antes de iniciar as instruções, verifique se você está conectado com sua conta do Azure. Na área de trabalho, abra uma nova janela do Azure PowerShell e insira o snippet a seguir. Quando solicitado a fazer logon, certifique-se de fazer logon como um proprietário/administrador da assinatura:

```
# Log in to your Azure account
Connect-AzAccount

# List all the subscriptions associated to your account
Get-AzSubscription

# Select a subscription
Set-AzContext -SubscriptionId <subscription ID>
```

O modelo implanta estes tipos de recursos:

* [Microsoft.DataLakeStore/accounts](/azure/templates/microsoft.datalakestore/accounts)
* [Microsoft.Storage/storageAccounts](/azure/templates/microsoft.storage/storageaccounts)
* [Microsoft.HDInsight/clusters](/azure/templates/microsoft.hdinsight/clusters)

## <a name="upload-sample-data-to-data-lake-storage-gen1"></a>Carregar dados de exemplo para o Data Lake Storage Gen1
O modelo do Resource Manager cria uma nova conta do Data Lake Storage Gen1 e a associa ao cluster HDInsight. Agora você deve carregar alguns dados de exemplo para o Data Lake Storage Gen1. Esses dados serão necessários posteriormente no tutorial para executar trabalhos de um cluster HDInsight que acessa dados na conta do Data Lake Storage Gen1. Para obter instruções sobre como carregar dados, consulte [Carregar um arquivo para a conta do Data Lake Storage Gen1](data-lake-store-get-started-portal.md#uploaddata). Se estiver procurando alguns dados de exemplo para carregar, é possível obter a pasta **Dados da Ambulância** no [Repositório Git do Azure Data Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).

## <a name="set-relevant-acls-on-the-sample-data"></a>Definir ACLs relevantes nos dados de exemplo
Para certificar-se de que os dados de exemplo carregados estejam acessíveis no cluster HDInsight, você deve garantir que o aplicativo do Azure AD usado para estabelecer a identidade entre o cluster HDInsight e o Data Lake Storage Gen1 tenha acesso ao arquivo/pasta que você está tentando acessar. Para fazer isso, execute as seguintes etapas.

1. Localize o nome do aplicativo do Azure AD associado ao cluster do HDInsight e à conta do Data Lake Storage Gen1. Uma maneira para procurar o nome é abrir a folha do cluster HDInsight que você criou usando o modelo do Resource Manager, clique na guia **Identidade do Cluster AAD** e procure o valor do **Nome de exibição da entidade de serviço**.
2. Agora, forneça acesso a esse aplicativo do Azure AD no arquivo/pasta que você deseja acessar do cluster HDInsight. Para definir as ACLs corretas no arquivo/pasta no Data Lake Storage Gen1, consulte [Proteger dados no Data Lake Storage Gen1](data-lake-store-secure-data.md#filepermissions).

## <a name="run-test-jobs-on-the-hdinsight-cluster-to-use-data-lake-storage-gen1"></a>Executar trabalhos de teste no cluster HDInsight para usar Data Lake Storage Gen1
Após configurar um cluster HDInsight, você poderá executar trabalhos de teste no cluster para testar se o cluster HDInsight pode acessar o Data Lake Storage Gen1. Para fazer isso, executaremos um exemplo de trabalho do Hive que cria uma tabela usando os dados de exemplo que você carregou anteriormente para a conta do Data Lake Storage Gen1.

Nesta seção, você acessará um cluster Linux HDInsight por SSH e executará uma consulta Hive de exemplo. Se está usando um cliente Windows, recomendamos usar **PuTTY**, que pode ser baixado de [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

Para saber mais sobre a utilização do PuTTY, confira [Usar SSH com o Hadoop baseado em Linux no HDInsight no Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).

1. Uma vez conectado, inicie a CLI do Hive usando o seguinte comando:

   ```
   hive
   ```
2. Usando a CLI, insira as instruções a seguir para criar uma nova tabela nomeada **veículos**, usando os dados de exemplo no Data Lake Storage Gen1:

   ```
   DROP TABLE vehicles;
   CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestoragegen1>.azuredatalakestore.net:443/';
   SELECT * FROM vehicles LIMIT 10;
   ```

   Você deverá ver um resultado semelhante ao seguinte:

   ```
   1,1,2014-09-14 00:00:03,46.81006,-92.08174,51,S,1
   1,2,2014-09-14 00:00:06,46.81006,-92.08174,13,NE,1
   1,3,2014-09-14 00:00:09,46.81006,-92.08174,48,NE,1
   1,4,2014-09-14 00:00:12,46.81006,-92.08174,30,W,1
   1,5,2014-09-14 00:00:15,46.81006,-92.08174,47,S,1
   1,6,2014-09-14 00:00:18,46.81006,-92.08174,9,S,1
   1,7,2014-09-14 00:00:21,46.81006,-92.08174,53,N,1
   1,8,2014-09-14 00:00:24,46.81006,-92.08174,63,SW,1
   1,9,2014-09-14 00:00:27,46.81006,-92.08174,4,NE,1
   1,10,2014-09-14 00:00:30,46.81006,-92.08174,31,N,1
   ```


## <a name="access-data-lake-storage-gen1-using-hdfs-commands"></a>Acessar o Data Lake Storage Gen1 usando os comandos do HDFS
Após configurar o cluster HDInsight para usar o Data Lake Storage Gen1, você poderá usar os comandos do shell do HDFS para acessar o armazenamento.

Nesta seção, você acessará um cluster Linux HDInsight por SSH e executará comandos do HDFS. Se está usando um cliente Windows, recomendamos usar **PuTTY**, que pode ser baixado de [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

Para saber mais sobre a utilização do PuTTY, confira [Usar SSH com o Hadoop baseado em Linux no HDInsight no Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).

Uma vez conectado, use o seguinte comando do sistema de arquivos HDFS para listar os arquivos na conta do Data Lake Storage Gen1.

```
hdfs dfs -ls adl://<Data Lake Storage Gen1 account name>.azuredatalakestore.net:443/
```

Isso deve listar o arquivo que você carregou anteriormente para o Data Lake Storage Gen1.

```
15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
Found 1 items
-rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestoragegen1.azuredatalakestore.net:443/mynewfolder
```

Também é possível usar o comando `hdfs dfs -put` para carregar alguns arquivos no Data Lake Storage Gen1 e, em seguida, usar `hdfs dfs -ls` para verificar se os arquivos foram carregados com êxito.


## <a name="next-steps"></a>Próximas etapas
* [Copiar dados do Azure Storage Blobs para o Data Lake Storage Gen1](data-lake-store-copy-data-wasb-distcp.md)
* [Usar Data Lake Storage Gen1 com clusters HDInsight do Azure](../hdinsight/hdinsight-hadoop-use-data-lake-store.md)
