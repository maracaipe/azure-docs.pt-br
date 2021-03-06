---
title: Solucionar problemas do Storm usando o Azure HDInsight
description: Obtenha respostas para perguntas comuns sobre o uso do Apache Storm com o Azure HDInsight.
keywords: Azure HDInsight, Storm, perguntas frequentes, guia de solução de problemas, problemas comuns
services: hdinsight
ms.service: hdinsight
author: hrasheed-msft
ms.author: hrasheed
ms.reviewer: jasonh
ms.topic: conceptual
ms.date: 12/06/2018
ms.custom: seodec18
ms.openlocfilehash: 5634d812b3fbd4e904516767b008f63104b3d7b7
ms.sourcegitcommit: c94cf3840db42f099b4dc858cd0c77c4e3e4c436
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2018
ms.locfileid: "53632731"
---
# <a name="troubleshoot-apache-storm-by-using-azure-hdinsight"></a>Solucionar problemas do Apache Storm usando o Azure HDInsight

Aprenda sobre os principais problemas e suas resoluções para trabalhar com [Cargas úteis do Apache Storm](https://storm.apache.org/) em [Apache Ambari](https://ambari.apache.org/).

## <a name="how-do-i-access-the-storm-ui-on-a-cluster"></a>Como fazer para acessar a interface do usuário do Storm em um cluster?
Você tem duas opções para acessar a interface do usuário do Storm em um navegador:

### <a name="ambari-ui"></a>Interface do usuário do Ambari
1. Vá até o painel do Ambari.
2. Na lista de serviços, selecione **Storm**.
3. No menu **Links Rápidos**, selecione **Interface do Usuário do Storm**.

### <a name="direct-link"></a>Link direto
Você pode acessar a interface do usuário do Storm na seguinte URL:

https://\<nome DNS do cluster\>/stormui

Exemplo:

 https://stormcluster.azurehdinsight.net/stormui

## <a name="how-do-i-transfer-storm-event-hub-spout-checkpoint-information-from-one-topology-to-another"></a>Como fazer para transferir informações de ponto de verificação de spout no hub de eventos Storm de uma topologia para outra?

Quando desenvolve topologias que leem os Hubs de Eventos do Azure usando o arquivo .jar do spout do hub de eventos Storm no HDInsight, você precisa implantar uma topologia que tenha o mesmo nome em um novo cluster. No entanto, você deve reter os dados do ponto de verificação que foram confirmados no [Apache ZooKeeper](https://zookeeper.apache.org/) no cluster antigo.

### <a name="where-checkpoint-data-is-stored"></a>O local em que os dados de ponto de verificação são armazenados
Os dados de ponto de verificação para deslocamentos são armazenados pelo spout do hub de eventos no ZooKeeper em dois caminhos raiz:
- Pontos de verificação de spout não transacionais são armazenados em /eventhubspout.
- Dados de pontos de verificação de spout transacionais são armazenados em /transactional.

### <a name="how-to-restore"></a>Como restaurar
Para fazer com que os scripts e bibliotecas que você usa exportem dados para fora do ZooKeeper e, em seguida, importar os dados de volta para o ZooKeeper com um novo nome, consulte [Exemplos de Storm no HDInsight](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).

A pasta lib tem arquivos .jar que contêm a implementação para a operação de exportação/importação. A pasta bash tem um script de exemplo que demonstra como exportar dados do servidor do ZooKeeper no cluster antigo e importá-los de volta para o servidor do ZooKeeper no novo cluster.

Execute o script [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) nos nós do ZooKeeper para exportar e, em seguida, importar dados. Atualize o script para a versão correta da HDP (Hortonworks Data Platform). (Estamos trabalhando para tornar esses scripts genéricos no HDInsight. Scripts genéricos podem ser executados em qualquer nó no cluster sem modificações pelo usuário.)

O comando de exportação grava os metadados em um caminho de HDFS (Sistema de Arquivos Distribuído) do Apache Hadoop (no repositório do Azure Blob Storage ou Azure Data Lake Storage) em um local que você definir.

### <a name="examples"></a>Exemplos

#### <a name="export-offset-metadata"></a>Exportar metadados de deslocamento
1. Use SSH para ir até o cluster do ZooKeeper no cluster do qual o deslocamento do ponto de verificação precisa ser exportado.
2. Execute o seguinte comando (depois de atualizar a cadeia de caracteres de versão do HDP) para exportar dados de deslocamento do ZooKeeper para o caminho do HDFS /stormmetadata/zkdata:

    ```apache   
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter export /eventhubspout /stormmetadata/zkdata
    ```

#### <a name="import-offset-metadata"></a>Importar metadados de deslocamento
1. Use SSH para ir até o cluster do ZooKeeper no cluster do qual o deslocamento do ponto de verificação precisa ser importado.
2. Execute o seguinte comando (depois de atualizar a cadeia de caracteres de versão do HDP) para importar dados de deslocamento do ZooKeeper do caminho do HDFS /stormmetadata/zkdata para o servidor do ZooKeeper no cluster de destino:

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter import /eventhubspout /home/sshadmin/zkdata
    ```
   
#### <a name="delete-offset-metadata-so-that-topologies-can-start-processing-data-from-the-beginning-or-from-a-timestamp-that-the-user-chooses"></a>Exclua metadados de deslocamento para que as topologias possam começar a processar dados desde o início ou desde um carimbo de data/hora escolhido pelo usuário
1. Use SSH para ir até o cluster do ZooKeeper no cluster do qual o deslocamento do ponto de verificação precisa ser excluído.
2. Execute o comando a seguir (depois de atualizar a cadeia de caracteres de versão do HDP) para excluir todos os dados de deslocamento do ZooKeeper no cluster atual:

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter delete /eventhubspout
    ```

## <a name="how-do-i-locate-storm-binaries-on-a-cluster"></a>Como fazer para localizar binários do Storm em um cluster?
Binários do Storm para a pilha do HDP atual estão em /usr/hdp/current/storm-client. O local é o mesmo para nós de cabeçalho e para nós de trabalho.
 
Pode haver vários binários para versões específicas do HDP em /usr/hdp (por exemplo, /usr/hdp/2.5.0.1233/storm). A pasta /usr/hdp/current/storm-client está vinculada simbolicamente à versão mais recente em execução no cluster.

Para obter mais informações, consulte [Conectar um cluster HDInsight usando SSH](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) e [Apache Storm](https://storm.apache.org/).
 
## <a name="how-do-i-determine-the-deployment-topology-of-a-storm-cluster"></a>Como fazer para determinar a topologia de implantação de um cluster do Storm?
Primeiro, identifique todos os componentes instalados com o HDInsight Storm. Um cluster do Storm consiste em quatro categorias de nó:

* Nós de gateway
* Nós de cabeçalho
* Nós do ZooKeeper
* Nós de trabalho
 
### <a name="gateway-nodes"></a>Nós de gateway
Um nó de gateway é um serviço de proxy reverso e de gateway que habilita o acesso público a um serviço de gerenciamento do Ambari ativo. Ele também lida com a seleção de líder do Ambari.
 
### <a name="head-nodes"></a>Nós de cabeçalho
Nós de cabeçalho do Storm executam os seguintes serviços:
* Nimbus
* Servidor Ambari
* Servidor de Métricas do Ambari
* Coletor de Métricas do Ambari
 
### <a name="zookeeper-nodes"></a>Nós do ZooKeeper
O HDInsight tem um quorum do ZooKeeper de três nós. O tamanho do quorum é fixo e não é configurável.
 
Serviços do Storm no cluster são configurados para usar o quorum do ZooKeeper automaticamente.
 
### <a name="worker-nodes"></a>Nós de trabalho
Nós de trabalho do Storm executam os seguintes serviços:
* Supervisor
* JVMs (máquinas virtuais Java) de trabalho, para executar topologias
* Agente do Ambari
 
## <a name="how-do-i-locate-storm-event-hub-spout-binaries-for-development"></a>Como fazer para localizar binários de spout do hub de eventos Storm para desenvolvimento?
 
Para obter mais informações sobre como usar arquivos .jar de spout do hub de eventos do Storm com sua topologia, consulte os seguintes recursos.
 
### <a name="java-based-topology"></a>Topologia baseada em Java
[Processar eventos dos Hubs de Eventos do Azure com o Apache Storm no HDInsight (Java)](https://docs.microsoft.com/azure/hdinsight/hdinsight-storm-develop-java-event-hub-topology)
 
### <a name="c-based-topology-mono-on-hdinsight-34-linux-storm-clusters"></a>Topologia baseada em C# (Mono em clusters Storm Linux no HDInsight 3.4+)
[Processar eventos dos Hubs de Eventos do Azure com o Apache Storm no HDInsight (C#)](https://docs.microsoft.com/azure/hdinsight/hdinsight-storm-develop-csharp-event-hub-topology)
 
### <a name="latest-apache-storm-event-hub-spout-binaries-for-hdinsight-35-linux-storm-clusters"></a>Os mais recentes binários do spout do hub de eventos do Apache Storm para clusters do HDInsight 3.5+ Linux Storm
Para saber como usar o spout de hub de eventos do Storm mais recente que funciona com clusters Storm Linux do HDInsight 3.5+, consulte o [arquivo Leiame](https://github.com/hdinsight/mvn-repo/blob/master/README.md) do repositório de mvn.
 
### <a name="source-code-examples"></a>Exemplos de código-fonte
Veja [exemplos](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) de ler e gravar no Hub de Eventos do Azure usando uma topologia do Apache Storm (escrita em Java) em um cluster do Azure HDInsight.
 
## <a name="how-do-i-locate-storm-log4j-2-configuration-files-on-clusters"></a>Como fazer para localizar arquivos de configuração do Storm Log4J 2 em clusters?
 
Para identificar os arquivos de configuração do [Apache Log4j 2](https://logging.apache.org/log4j/2.x/) para os serviços do Storm.
 
### <a name="on-head-nodes"></a>Em nós de cabeçalho
A configuração de Log4J Nimbus é lida de /usr/hdp/\<versão de HDP\>/storm/log4j2/cluster.xml.
 
### <a name="on-worker-nodes"></a>Em nós de trabalho
A configuração de Log4J de supervisor é lida de /usr/hdp/\<versão de HDP\>/storm/log4j2/cluster.xml.
 
O arquivo de configuração de Log4J de trabalho é lido de /usr/hdp/\<versão de HDP\>/storm/log4j2/worker.xml.
 
Exemplos: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml

### <a name="see-also"></a>Veja também
[Solucionar problemas usando o Azure HDInsight](../../hdinsight/hdinsight-troubleshoot-guide.md)
