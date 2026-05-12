---
title: Extensão do conteúdo
description: Defina a duração do conteúdo em segundos no início da sessão. Ele direciona marcadores de progresso e Audiência média por minuto.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 12%

---


# Extensão do conteúdo

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados da variável **Comprimento do conteúdo**. Consulte [Comprimento do conteúdo](/help/reporting/dimensions/content-length.md) para a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A variável de comprimento do conteúdo é a duração total do conteúdo em segundos. É necessário para todas as implementações de mídia de transmissão e deve ser definido no início da sessão. A duração do conteúdo direciona várias métricas calculadas de back-end, incluindo marcadores de progresso (25/10/50/75/95%) e Público-alvo médio por minuto. Se o comprimento do conteúdo não for definido ou não for maior que zero, essas métricas não serão produzidas. Para fluxos ao vivo com duração desconhecida, use `86400` (24 horas).

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.length` |
| **Campo da coleção XDM** | [`mediaCollection.sessionDetails.length`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Obrigatório** | Sim |
| **Enviado com** | Início da sessão, fechamento da sessão |

## SDK da web

Definir `length` dentro de `mediaCollection.sessionDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        length: 128,
        contentType: "vod",
        playerName: "HTML5 Player",
        channel: "Sports",
        streamType: "video"
      },
      playhead: 0
    }
  }
});
```

## SDK móvel

Transmita a duração do conteúdo em segundos como o argumento `length` para `createMediaObject`.

**iOS (Swift)**

```swift
let mediaObject = Media.createMediaObjectWith(name: "My Video",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
var mediaInfo = Media.createMediaObject("My Video",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

## Roku (BrightScript)

Definir `length` dentro de `mediaCollection.sessionDetails` ao chamar `createMediaSession`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
                "friendlyName": "My Video",
                "length": 128,
                "contentType": "vod",
                "playerName": "Roku Player",
                "channel": "Sports",
                "streamType": "video"
            },
            "playhead": 0
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) com `length` dentro de `mediaCollection.sessionDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "length": 128,
          "contentType": "vod",
          "playerName": "HTML5 Player",
          "channel": "Sports"
        },
        "playhead": 0
      }
    }
  }]
}
```

## SDK de mídia

Passe a duração do conteúdo em segundos como o terceiro argumento para `ADB.Media.createMediaObject`:

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",
  "video-123",
  128,                      // length in seconds
  ADB.Media.StreamType.VOD,
  ADB.Media.MediaType.Video
);

tracker.trackSessionStart(mediaInfo, contextData);
```

## API da coleção de mídia

Inclua `media.length` no objeto `params` de sua solicitação POST `sessionStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.length": 128
  }
}
```

Consulte a [Referência de sessões da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obter a estrutura de solicitação completa.
