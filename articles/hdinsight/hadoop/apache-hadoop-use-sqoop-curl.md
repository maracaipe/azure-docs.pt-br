---
title: Use o Apache Sqoop com o Curl no HDInsight - Azure
description: Aprenda a enviar tarefas do Apache Sqoop remotamente para o HDInsight usando o Curl.
services: hdinsight
author: hrasheed-msft
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 05/16/2018
ms.author: hrasheed
ms.openlocfilehash: a7b657d11e829d636063639e26a90d671a5d1473
ms.sourcegitcommit: c2e61b62f218830dd9076d9abc1bbcb42180b3a8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/15/2018
ms.locfileid: "53438346"
---
# <a name="run-apache-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a>Execute tarefas do Apache Sqoop com o Hadoop no HDInsight com Curl
[!INCLUDE [sqoop-selector](../../../includes/hdinsight-selector-use-sqoop.md)]

Aprenda a usar o Curl para executar tarefas do Apache Sqoop em um cluster do Apache Hadoop no HDInsight.

Curl é usado para demonstrar como você pode interagir com o HDInsight usando solicitações HTTP brutas para executar, monitorar e recuperar os resultados de trabalhos do Sqoop. Isso funciona usando a API REST do WebHCat (anteriormente conhecido como Templeton) fornecida pelo seu cluster HDInsight.

## <a name="prerequisites"></a>Pré-requisitos
Para concluir as etapas neste artigo, você precisará do seguinte:


* Conclua [Usar o Apache Sqoop com o Hadoop no HDInsight](hdinsight-use-sqoop.md#create-cluster-and-sql-database) para configurar um ambiente com um cluster HDInsight e um banco de dados SQL do Azure.
* [Curl](https://curl.haxx.se/). Curl é uma ferramenta para transferir dados de ou um cluster HDInsight ou para ele.
* [jq](https://stedolan.github.io/jq/). O utilitário jq é usado para processar os dados JSON retornados de solicitações REST.


## <a name="submit-apache-sqoop-jobs-by-using-curl"></a>Enviar trabalhos do Apache Sqoop usando o cURL
> [!NOTE]  
> Ao usar o Curl ou qualquer outra comunicação do REST com WebHCat, você deve autenticar as solicitações, fornecendo o nome de usuário e a senha para o administrador do cluster HDInsight. Você também deve usar o nome do cluster como parte do URI (Uniform Resource Identifier) usado para enviar as solicitações ao servidor.
> 
> Para os comandos nesta seção, substitua **USERNAME** pelo usuário para autenticar o cluster e substitua **PASSWORD** pela senha da conta de usuário. Substitua **CLUSTERNAME** pelo nome do cluster.
> 
> A API REST é protegida por meio de [autenticação básica](https://en.wikipedia.org/wiki/Basic_access_authentication). Você deve sempre fazer solicitações usando HTTPS (HTTP seguro) para ajudar a garantir que suas credenciais sejam enviadas com segurança para o servidor.
> 
> 

1. De uma linha de comando, use o seguinte comando para verificar se você pode se conectar ao cluster HDInsight:

    ```bash   
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    Você deve receber uma resposta com esta aparência:

    ```json   
    {"status":"ok","version":"v1"}
    ```
   
    Os parâmetros usados nesse comando são os seguintes:
   
   * **-u** - o nome de usuário e a senha usada para autenticar a solicitação.
   * **-G** - indica que se trata de uma solicitação GET.
     
     O início da URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, é o mesmo para todas as solicitações. O caminho, **/status**, indica que a solicitação é para retornar o status de WebHCat (também conhecido como Templeton) ao servidor. 
2. Use o seguinte para enviar um trabalho do sqoop:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /example/data/sample.log --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/data/sqoop/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop
    ```

    Os parâmetros usados nesse comando são os seguintes:

    * **-d** – uma vez que `-G` não é usado; a solicitação padrão é o método POST. `-d` especifica os valores de dados que são enviados com a solicitação.

        * **user.name** - o usuário que está executando o comando.

        * **command** - o comando Sqoop a ser executado.

        * **statusdir** - o diretório no qual o status deste trabalho será gravado.

    Esse comando deverá retornar uma ID de trabalho que pode ser usada para verificar o status do trabalho.

        ```json
        {"id":"job_1415651640909_0026"}
        ```

3. Para verificar o status do trabalho, use o comando a seguir. Substitua **JOBID** pelo valor retornado na etapa anterior. Por exemplo, se o valor retornado for **, `{"id":"job_1415651640909_0026"}`JOBID** será `job_1415651640909_0026`.

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    Se o trabalho foi concluído, o estado será **SUCCEEDED**.
   
   > [!NOTE]  
   > Essa solicitação de Curl retorna um documento JSON (JavaScript Object Notation) com informações sobre o trabalho; jq é usado para recuperar o valor de estado.

4. Depois que o estado do trabalho for alterado para **SUCCEEDED**, você poderá recuperar os resultados do trabalho no Armazenamento de Blobs do Azure. O parâmetro `statusdir` passado com a consulta contém o local do arquivo de saída; nesse caso, **wasb:///example/data/sqoop/curl**. Esse endereço armazena a saída do trabalho no diretório **example/data/sqoop/curl** no contêiner de armazenamento padrão usado pelo cluster HDInsight.
   
    É possível usar o Portal do Azure para acessar os blobs stderr e stdout.  Também é possível usar o Microsoft SQL Server Management Studio para verificar os dados carregados para a tabela log4jlogs.

## <a name="limitations"></a>Limitações
* Exportação em massa — com HDInsight baseado em Linux, o conector Sqoop usado para exportar dados no Microsoft SQL Server ou no Banco de Dados SQL do Azure, atualmente, não permite inserções em massa.
* Envio em lote — com HDInsight baseado em Linux, ao usar o comutador `-batch` na execução de inserções, Sqoop executará várias inserções em vez de operações de inserção em lotes.

## <a name="summary"></a>Resumo
Conforme demonstrado neste documento, você pode usar uma solicitação HTTP bruta para executar, monitorar e exibir os resultados de trabalhos do Sqoop no cluster HDInsight.

Para obter mais informações sobre a interface REST usada neste artigo, confira o <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Guia da API REST do Apache Sqoop</a>.

## <a name="next-steps"></a>Próximas etapas
Para obter informações gerais sobre o Hive com HDInsight:

* [Usar o Apache Sqoop com o Apache Hadoop no HDInsight](hdinsight-use-sqoop.md)

Para obter informações sobre outras maneiras que você pode trabalhar com Hadoop no HDInsight:

* [Use o Apache Hive com o Apache Hadoop no HDInsight](hdinsight-use-hive.md)
* [Use o Apache Pig com o Apache Hadoop no HDInsight](hdinsight-use-pig.md)
* [Usar o MapReduce com o Apache Hadoop no HDInsight](hdinsight-use-mapreduce.md)

Para outros artigos do HDInsight que envolvem curl:
 
* [Criar clusters Apache Hadoop usando a API REST do Azure](../hdinsight-hadoop-create-linux-clusters-curl-rest.md)
* [Executar consultas do Apache Hive com o Apache Hadoop no HDInsight usando a REST](apache-hadoop-use-hive-curl.md)
* [Executar trabalhos do MapReduce com o Apache Hadoop no HDInsight usando a REST](apache-hadoop-use-mapreduce-curl.md)
* [Executar trabalhos do Apache Pig com o Apache Hadoop no HDInsight usando o cURL](apache-hadoop-use-pig-curl.md)



