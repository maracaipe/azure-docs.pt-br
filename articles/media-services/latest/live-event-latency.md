---
title: Latência LiveEvent nos Serviços de Mídia do Microsoft Azure | Microsoft Docs
description: Este tópico fornece uma visão geral de latência de LiveEvent e mostra como definir a baixa latência.
services: media-services
documentationcenter: ''
author: Juliako
manager: femila
editor: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/28/2019
ms.author: juliako
ms.openlocfilehash: db6646c2066be940b2c058653fe8f2ceb9bff3a2
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2019
ms.locfileid: "55169690"
---
# <a name="live-event-latency-in-media-services"></a>Latência do Evento ao Vivo nos Serviços de Mídia

Este artigo mostra como definir baixa latência em um [Evento ao Vivo](https://docs.microsoft.com/rest/api/media/liveevents). Esta seção também discute os resultados comuns que você vê ao usar as configurações de baixa latência e de vários players. Os resultados variam com base na latência de rede e da CDN.

Para usar o novo recurso **LowLatency**, você pode definir as **StreamOptionsFlag** à **LowLatency** sobre o **LiveEvent**. Ao criar [LiveOutput](https://docs.microsoft.com/rest/api/media/liveoutputs) para reprodução HLS, defina [LiveOutput.Hls.fragmentsPerTsSegment](https://docs.microsoft.com/rest/api/media/liveoutputs/create#hls) como 1. Depois que o fluxo está em execução, você pode usar o [Player de Mídia do Azure](http://ampdemo.azureedge.net/) (AMP- página de demonstração) e defina as opções de reprodução para usar a baixa latência heurística "perfil".

> [!NOTE]
> Atualmente, o LowLatency HeuristicProfile no Player de Mídia do Azure foi projetado para reproduzir fluxos no protocolo DASH ou HLS com CMAF. Se você estiver direcionando os dispositivos iOS ou MacOS por meio do HLS com o TS (por exemplo, `format=m3u8-aapl` ou `format=m3u8-aapl-v3`), não use essa configuração, pois AMP usa diretamente o player original fornecido pelo sistema operacional para esse caso.

O exemplo de .NET a seguir mostra como definir **LowLatency** sobre o **LiveEvent**:

```csharp
LiveEvent liveEvent = new LiveEvent(
            location: mediaService.Location, 
            description: "Sample LiveEvent for testing",
            vanityUrl: false,
            encoding: new LiveEventEncoding(
                        // Set this to Standard to enable a transcoding LiveEvent, and None to enable a pass-through LiveEvent
                        encodingType:LiveEventEncodingType.None, 
                        presetName:null
                    ),
            input: new LiveEventInput(LiveEventInputProtocol.RTMP,liveEventInputAccess), 
            preview: liveEventPreview,
            streamOptions: new List<StreamOptionsFlag?>()
            {
                // Set this to Default or Low Latency
                // To use low latency optimally, you should tune your encoder settings down to 1 second "Group Of Pictures" (GOP) length instead of 2 seconds.
                StreamOptionsFlag.LowLatency
            }
        );
```                

Veja o exemplo completo: [MediaV3LiveApp](https://github.com/Azure-Samples/media-services-v3-dotnet-core-tutorials/blob/master/NETCore/Live/MediaV3LiveApp/Program.cs#L126).

## <a name="live-events-latency"></a>Latência de Eventos ao Vivo

A tabela a seguir mostra os resultados comuns de latência (quando o sinalizador LowLatency está habilitado) nos Serviços de Mídia, medido desde a hora em que o feed de contribuição atinge o serviço até quando um visualizador vê a reprodução no player. Para usar baixa latência de maneira ideal, é necessário ajustar as configurações do codificador, reduzindo o tamanho do "GOP (Grupo de imagens)" para 1 segundo. Ao usar um tamanho maior de GOP, você minimiza o consumo de largura de banda e reduz a taxa de bits na mesma taxa de quadros. Isso é especialmente útil em vídeos com menos movimento.

### <a name="pass-through"></a>Passagem 

||2s GOP baixa latência habilitada|1s GOP baixa latência habilitada|
|---|---|---|
|TRAÇO no AMP|10s|8s|
|HLS no player de iOS nativo|14s|10s|

### <a name="live-encoding"></a>Codificação ativa

||2s GOP baixa latência habilitada|1s GOP baixa latência habilitada|
|---|---|---|
|TRAÇO no AMP|14s|10s|
|HLS no player de iOS nativo|18s|13s|

> [!NOTE]
> A latência de ponta a ponta pode variar, dependendo das condições de rede local ou com a introdução de uma camada de cache da CDN. Você deve testar as configurações exatas.

## <a name="next-steps"></a>Próximas etapas

- [Visão geral da transmissão ao vivo](live-streaming-overview.md)
- [Tutorial de live streaming](stream-live-tutorial-with-api.md)

