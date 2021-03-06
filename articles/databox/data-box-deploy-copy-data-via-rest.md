---
title: Copiar dados para o Armazenamento de Blobs do Azure Data Box por meio de APIs REST | Microsoft Docs
description: Saiba como copiar dados para o Armazenamento de Blobs do Azure Data Box por meio de APIs REST
services: databox
author: alkohli
ms.service: databox
ms.subservice: pod
ms.topic: tutorial
ms.date: 01/24/2019
ms.author: alkohli
ms.openlocfilehash: 412bf66902f156c6c8720a720973f97d1d7b1d8f
ms.sourcegitcommit: 039263ff6271f318b471c4bf3dbc4b72659658ec
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2019
ms.locfileid: "55751609"
---
# <a name="tutorial-copy-data-to-azure-data-box-blob-storage-via-rest-apis"></a>Tutorial: Copiar dados para o Armazenamento de Blobs do Azure Data Box por meio de APIs REST  

Este tutorial descreve os procedimentos usados para se conectar ao Armazenamento de Blobs do Azure Data Box por meio de APIs REST via *HTTP* ou *HTTPS*. Após a conexão, as etapas necessárias para copiar os dados para o Armazenamento de Blobs do Data Box e preparar o Data Box para envio também são descritas.

Neste tutorial, você aprenderá como:

> [!div class="checklist"]
> * Pré-requisitos
> * Conectar-se ao Armazenamento de Blobs do Data Box via *HTTP* ou *HTTPS*
> * Copiar dados para caixa de dados

## <a name="prerequisites"></a>Pré-requisitos

Antes de começar, verifique se:

1. Você concluiu o [Tutorial: Configurar o Azure Data Box](data-box-deploy-set-up.md).
2. Você recebeu seu Data Box e o status do pedido no portal está como **Entregue**.
3. Você examinou os [requisitos do sistema para o Armazenamento de Blobs do Data Box](data-box-system-requirements-rest.md) e está familiarizado com as versões compatíveis de APIs, SDKs e ferramentas.
4. Você tem acesso a um computador host contendo os dados que deseja copiar para o Data Box. O computador host deve
    - Executar um [Sistema operacional com suporte](data-box-system-requirements.md).
    - Estar conectado a uma rede de alta velocidade. É altamente recomendável que você tenha pelo menos uma conexão de 10 GbE. Se uma conexão de 10 GbE não estiver disponível, um link de dados de 1 GbE poderá ser usado, mas as velocidades de cópia serão afetadas.
5. [Baixe o AzCopy 7.1.0](https://aka.ms/azcopyforazurestack20170417) no computador host. Você usará o AzCopy para copiar dados para o Armazenamento de Blobs do Azure Data Box do computador host.


## <a name="connect-to-data-box-blob-storage"></a>Conectar-se ao Armazenamento de Blobs do Data Box

Conecte-se ao Armazenamento de Blobs do Data Box via *HTTP* ou *HTTPS*. Em geral, *HTTPS* é a maneira segura e recomendada de se conectar ao Armazenamento de Blobs do Data Box. *HTTP* é usado para a conexão em redes confiáveis. Dependendo se você estiver se conectando ao Armazenamento de Blobs do Data Box via *HTTP* ou *HTTPS*, as etapas poderão ser diferentes.

## <a name="connect-via-http"></a>Conectar-se via HTTP

A conexão às APIs REST do Armazenamento de Blobs do Data Box via *HTTP* exige as seguintes etapas:

- Adicionar o IP do dispositivo e o ponto de extremidade de serviço Blob ao host remoto
- Configurar software de terceiros e verificar a conexão

Cada uma dessas etapas é descrita nas seções a seguir.

#### <a name="add-device-ip-address-and-blob-service-endpoint-to-the-remote-host"></a>Adicionar o endereço IP do dispositivo e o ponto de extremidade de serviço Blob ao host remoto

[!INCLUDE [data-box-add-device-ip](../../includes/data-box-add-device-ip.md)]

#### <a name="configure-partner-software-and-verify-connection"></a>Configurar o software parceiro e verificar a conexão

[!INCLUDE [data-box-configure-partner-software](../../includes/data-box-configure-partner-software.md)]

[!INCLUDE [data-box-verify-connection](../../includes/data-box-verify-connection.md)]

## <a name="connect-via-https"></a>Conectar-se via HTTPS

A conexão às APIs REST do Armazenamento de Blobs do Azure via HTTPS exige as seguintes etapas:

- Baixar o certificado no portal do Azure
- Preparar o computador host para gerenciamento remoto
- Adicionar o IP do dispositivo e o ponto de extremidade de serviço Blob ao host remoto
- Configurar software de terceiros e verificar a conexão

Cada uma dessas etapas é descrita nas seções a seguir.

### <a name="download-certificate"></a>Baixar certificado

Use o portal do Azure para baixar o certificado.

1. Entre no portal do Azure.
2. Acesse sua ordem do Data Box e navegue para **Geral > Detalhes do dispositivo**.
3. Em **Credenciais do dispositivo**, acesse **Acesso à API** no dispositivo. Clique em **Download**. Essa ação baixa um arquivo de certificado **<your order name>.cer**. **Salve** esse arquivo. Você instalará esse certificado no computador cliente ou host que será usado para se conectar ao dispositivo.

    ![Baixar o certificado no portal do Azure](media/data-box-deploy-copy-data-via-rest/download-cert-1.png)
 
### <a name="prepare-the-host-for-remote-management"></a>Preparar o host para gerenciamento remoto

Siga estas etapas para preparar o cliente Windows para uma conexão remota que usa uma sessão *HTTPS*:

- Importe o arquivo .cer para o repositório raiz do cliente ou do host remoto.
- Adicione o endereço IP do dispositivo e o ponto de extremidade de serviço Blob ao arquivo de hosts no cliente Windows.

Cada um dos procedimentos acima é descrito abaixo.

#### <a name="import-the-certificate-on-the-remote-host"></a>Importe o certificado no host remoto

Use o Windows PowerShell ou a interface do usuário do Windows Server para importar e instalar o certificado no sistema host.

**Como usar o PowerShell**

1. Inicie uma sessão do Windows PowerShell como administrador.
2. No prompt de comando, digite:

    ```
    Import-Certificate -FilePath C:\temp\localuihttps.cer -CertStoreLocation Cert:\LocalMachine\Root
    ```

**Usando a interface do usuário do Windows Server**

1.  Clique com o botão direito do mouse no arquivo .cer e selecione **Instalar certificado**. Isso inicia o Assistente para importação de certificados.
2.  Em **Localização do repositório**, selecione **Computador Local** e, em seguida, clique em **Próximo**.

    ![Importar o certificado usando o PowerShell](media/data-box-deploy-copy-data-via-rest/import-cert-ws-1.png)

3.  Selecione **Colocar todos os certificados no seguinte repositório** e, em seguida, clique em **Procurar**. Navegue até o repositório de raiz do seu host remoto e, em seguida, clique em **Próximo**.

    ![Importar o certificado usando o PowerShell](media/data-box-deploy-copy-data-via-rest/import-cert-ws-2.png)

4.  Clique em **Concluir**. Será exibida uma mensagem que informa que a importação foi bem-sucedida.

    ![Importar o certificado usando o PowerShell](media/data-box-deploy-copy-data-via-rest/import-cert-ws-3.png)

### <a name="to-add-device-ip-address-and-blob-service-endpoint-to-the-remote-host"></a>Para adicionar o endereço IP do dispositivo e o ponto de extremidade de serviço Blob ao host remoto

As etapas a serem seguidas são idênticas ao que você usou ao se conectar via *HTTP*.

### <a name="configure-partner-software-to-establish-connection"></a>Configurar o software parceiro para estabelecer a conexão

As etapas a serem seguidas são idênticas ao que você usou ao se conectar via *HTTP*. A única diferença é que você deve deixar a *opção Usar HTTP* desmarcada.

## <a name="copy-data-to-data-box"></a>Copiar dados para caixa de dados

Depois que você estiver conectado ao Armazenamento de Blobs do Data Box, a próxima etapa será copiar dados. Antes da cópia de dados, examine as seguintes considerações:

-  Ao copiar dados, verifique se o tamanho dos dados está de acordo com os limites de tamanho descritos nos [armazenamento do Azure e nos limites da Caixa de Dados](data-box-limits.md).
- Se os dados, que estão sendo carregados pelo Data Box, forem carregados simultaneamente por outros aplicativos fora do Data Box, isso poderá resultar em falhas no trabalho de upload e em dados corrompidos.

Neste tutorial, o AzCopy é usado para copiar dados para o Armazenamento de Blobs do Data Box. Use também o Gerenciador de Armazenamento do Azure (se preferir uma ferramenta baseada em GUI) ou um software parceiro para copiar os dados.
O procedimento de cópia tem as seguintes etapas:

- Criar um contêiner
- Carregar o conteúdo de uma pasta no Armazenamento de Blobs do Data Box
- Carregar os arquivos modificados no Armazenamento de Blobs do Data Box

Cada uma dessas etapas é descrita mais detalhadamente nas seções a seguir.

### <a name="create-a-container"></a>Criar um contêiner

A primeira etapa é criar um contêiner, pois os blobs são sempre carregados em um contêiner. Os contêineres organizam os grupos de blobs como você organiza arquivos em pastas no computador. Siga estas etapas para criar um contêiner de blobs.

1. Abra o Explorer do Armazenamento.
2. No painel esquerdo, expanda a conta de armazenamento na qual você deseja criar o contêiner de blobs.
3. Clique com o botão direito do mouse em **Contêineres de Blobs** e, no menu de contexto, selecione **Criar Contêiner de Blobs**.

   ![Menu de contexto Criar contêineres de blob](media/data-box-deploy-copy-data-via-rest/create-blob-container-1.png)

4. Uma caixa de texto será exibida abaixo da pasta **Contêineres de Blobs**. Insira o nome de seu contêiner de blobs. Confira [Criar o contêiner e definir as permissões](../storage/blobs/storage-quickstart-blobs-dotnet.md) para obter informações sobre regras e restrições de nomenclatura de contêineres de blobs.
5. Pressione **Enter** quanto terminar de criar o contêiner de blobs ou **Esc** para cancelar. Após a criação bem-sucedida do contêiner de blobs, ele será exibido na pasta **Contêineres de Blobs** da conta de armazenamento selecionada.

   ![Contêiner de blobs criado](media/data-box-deploy-copy-data-via-rest/create-blob-container-2.png)

### <a name="upload-contents-of-a-folder-to-data-box-blob-storage"></a>Carregar o conteúdo de uma pasta no Armazenamento de Blobs do Data Box

Use o AzCopy para carregar todos os arquivos de uma pasta no Armazenamento de Blobs no Windows ou no Linux. Para carregar todos os blobs em uma pasta, digite o seguinte comando do AzCopy:

#### <a name="linux"></a>Linux

    azcopy \
        --source /mnt/myfolder \
        --destination https://data-box-storage-account-name.blob.device-serial-no.microsoftdatabox.com/container-name/files/ \
        --dest-key <key> \
        --recursive

#### <a name="windows"></a> Windows

    AzCopy /Source:C:\myfolder /Dest:https://data-box-storage-account-name.blob.device-serial-no.microsoftdatabox.com/container-name/files/ /DestKey:<key> /S


Substitua `<key>` pela chave da conta. Para obter a chave da conta, no portal do Azure, acesse sua conta de armazenamento. Acesse **Configurações > Chaves de acesso**, selecione uma chave e cole-a no comando do AzCopy.

Se o contêiner de destino especificado não existir, o AzCopy o criará e carregará o arquivo nele. Atualize o caminho de origem para o diretório de dados e substitua `data-box-storage-account-name` na URL de destino pelo nome da conta de armazenamento associada ao Data Box.

Para carregar o conteúdo do diretório especificado recursivamente do Armazenamento de Blobs, especifique a opção `--recursive` (Linux) ou `/S` (Windows). Quando você executa o AzCopy com uma dessas opções, todas as subpastas e os respectivos arquivos são carregados também.

### <a name="upload-modified-files-to-data-box-blob-storage"></a>Carregar os arquivos modificados no Armazenamento de Blobs do Data Box

Use o AzCopy para carregar arquivos com base na hora de sua última modificação. Para testar isso, modifique ou crie novos arquivos em seu diretório de origem para fins de teste. Para carregar apenas arquivos novos ou atualizados, adicione o parâmetro `--exclude-older` (Linux) ou `/XO` (Windows) ao comando AzCopy.

Se você quiser copiar apenas os recursos de origem que não existem no destino, especifique ambos os parâmetros, `--exclude-older` e `--exclude-newer` (Linux), ou `/XO` e `/XN` (Windows), no comando AzCopy. O AzCopy carrega apenas os dados atualizados, com base em seu carimbo de data/hora.

#### <a name="linux"></a>Linux
    azcopy \
    --source /mnt/myfolder \
    --destination https://data-box-storage-account-name.blob.device-serial-no.microsoftdatabox.com/container-name/files/ \
    --dest-key <key> \
    --recursive \
    --exclude-older

#### <a name="windows"></a> Windows

    AzCopy /Source:C:\myfolder /Dest:https://data-box-storage-account-name.blob.device-serial-no.microsoftdatabox.com/container-name/files/ /DestKey:<key> /S /XO


A próxima etapa é preparar seu dispositivo para envio.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu sobre tópicos do Azure Data Box como:

> [!div class="checklist"]
> * Pré-requisitos
> * Conectar-se ao Armazenamento de Blobs do Data Box via *HTTP* ou *HTTPS*
> * Copiar dados para caixa de dados


Avance para o próximo tutorial para saber como enviar o Data Box novamente à Microsoft.

> [!div class="nextstepaction"]
> [Envie o Azure Data Box para a Microsoft](./data-box-deploy-picked-up.md)
