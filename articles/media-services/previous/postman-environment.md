---
title: Importar o ambiente Postman para chamadas REST de Serviços de Mídia do Azure
description: Este tópico fornece uma definição do ambiente Postman para chamadas REST dos Serviços de Mídia do Azure.
services: media-services
documentationcenter: ''
author: Juliako
manager: femila
editor: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2019
ms.author: juliako
ms.openlocfilehash: 99ed30809e49e36012263255c8cd0884cf6bbce8
ms.sourcegitcommit: e69fc381852ce8615ee318b5f77ae7c6123a744c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "55992051"
---
# <a name="import-the-postman-environment"></a>Importar o ambiente Postman  

Este artigo contém uma definição das variáveis de ambiente de **Postman** que são usadas na [coleção de Postman](postman-collection.md) que contêm as solicitações HTTP agrupadas que chamam as APIs REST dos Serviços de Mídia. Esses arquivos de ambiente e de coleção são usados pelo tutorial [Configurar o Postman para chamadas da API REST dos Serviços de Mídia](media-rest-apis-with-postman.md).

```
{
  "id": "2dbce3ce-74c2-2ceb-0461-c4c2323f5b09",
  "name": "AzureMedia",
  "values": [
    {
      "enabled": true,
      "key": "TenantID",
      "value": "",
      "type": "text"
    },
    {
      "enabled": true,
      "key": "AzureADSTSEndpoint",
      "value": "",
      "type": "text"
    },
    {
      "enabled": true,
      "key": "RESTAPIEndpoint",
      "value": "",
      "type": "text"
    },
    {
      "enabled": true,
      "key": "ClientID",
      "value": "",
      "type": "text"
    },
    {
      "enabled": true,
      "key": "ClientSecret",
      "value": "",
      "type": "text"
    },
    {
      "enabled": true,
      "key": "AccessToken",
      "value": "",
      "type": "text"
    },
    {
      "enabled": true,
      "key": "LastAssetId",
      "value": "",
      "type": "text"
    },
    {
      "enabled": true,
      "key": "LastAccessPolicyId",
      "value": "",
      "type": "text"
    },
    {
      "enabled": true,
      "key": "UploadURL",
      "value": "",
      "type": "text"
    },
    {
      "enabled": true,
      "key": "MediaFileName",
      "value": "BigBuckBunny.mp4",
      "type": "text"
    },
    {
      "enabled": true,
      "key": "LastChannelId",
      "value": "",
      "type": "text"
    }
  ],
  "_postman_variable_scope": "environment",
  "_postman_exported_using": "Postman/5.5.0"
}
```
