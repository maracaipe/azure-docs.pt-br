---
title: SDKs da Grade de Eventos do Azure
description: Descreve os SDKs de Grade de Eventos do Azure. Esses SDKs fornecem gerenciamento, publicação e o consumo.
services: event-grid
author: spelluru
manager: timlt
ms.service: event-grid
ms.topic: reference
ms.date: 01/19/2019
ms.author: spelluru
ms.openlocfilehash: 53a1f50647e05b71afe6accb85f8a90cd8b7e253
ms.sourcegitcommit: cf88cf2cbe94293b0542714a98833be001471c08
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54470386"
---
# <a name="event-grid-sdks-for-management-and-publishing"></a>SDKs de Grade de Eventos para o gerenciamento e publicação

Grade de Eventos fornece SDKs que permitem gerenciar seus recursos e lançar eventos programaticamente.

## <a name="management-sdks"></a>SDKs de gerenciamento

Os SDKs de gerenciamento permitem criar, atualizar e excluir assinaturas e tópicos de grade de eventos. No momento, os seguintes SDKs estão disponíveis:

* [.NET](https://www.nuget.org/packages/Microsoft.Azure.Management.EventGrid)
* [Go](https://github.com/Azure/azure-sdk-for-go)
* [Java](https://search.maven.org/#search%7Cga%7C1%7Cazure-mgmt-eventgrid)
* [Node](https://www.npmjs.com/package/azure-arm-eventgrid)
* [Python](https://pypi.python.org/pypi/azure-mgmt-eventgrid)
* [Ruby](https://rubygems.org/gems/azure_mgmt_event_grid)

## <a name="data-plane-sdks"></a>SDKs de plano de dados

Os SDKs de plano de dados permitem que você publique eventos para tópicos, tomando cuidado de autenticar, formar o evento, e publicar de forma assíncrona ao endpoint especificado. Elas também permitem que você consuma eventos de terceiros primeiro. No momento, os seguintes SDKs estão disponíveis:

* [.NET](https://www.nuget.org/packages/Microsoft.Azure.EventGrid)
* [Go](https://github.com/Azure/azure-sdk-for-go)
* [Java](https://mvnrepository.com/artifact/com.microsoft.azure/azure-eventgrid)
* [Node](https://www.npmjs.com/package/azure-eventgrid)
* [Python](https://pypi.python.org/pypi/azure-eventgrid)
* [Ruby](https://rubygems.org/gems/azure_event_grid)

## <a name="next-steps"></a>Próximas etapas

* Por aplicativos de exemplo, consulte [exemplos de código da grade de eventos](https://azure.microsoft.com/resources/samples/?sort=0&service=event-grid).
* Para ver uma introdução à Grade de Eventos, confira [O que é uma Grade de eventos?](overview.md)
* Para comandos de grade de eventos em CLI do Azure, consulte [CLI do Azure](/cli/azure/eventgrid).
* Para comandos de grade de eventos em PowerShell, consulte [PowerShell](/powershell/module/azurerm.eventgrid).
