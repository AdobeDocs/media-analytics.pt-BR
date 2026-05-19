---
title: Início da sessão
description: Sinalize o início de uma sessão de mídia e obtenha a ID de sessão necessária para todos os eventos subsequentes.
feature: Streaming Media
role: Developer
source-git-commit: 6534e4c76dcb4113bbbb99aed2a0e350f9256b15
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 10%

---


# Início da sessão

O evento de início de sessão abre uma sessão de rastreamento de mídia. Deve ser o primeiro evento enviado para qualquer reprodução. A resposta retorna uma ID de sessão que todos os eventos subsequentes da mesma sessão devem incluir.

Uma sessão expira automaticamente se **nenhum evento for recebido por 10 minutos** ou se houver **nenhum movimento do indicador de reprodução por 30 minutos**. Se uma sessão expirar, você deverá chamar o início da sessão novamente para obter uma nova ID de sessão.

* **Pré-requisitos**: nenhum; sempre o primeiro evento
* **Métrica associada**: [Inícios de mídia](/help/reporting/metrics/media-starts.md)

## SDK da web

Chame [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview) com `eventType: "media.sessionStart"` e o `sessionDetails` necessário. A resposta inclui a ID da sessão em `handle[].payload[].sessionId` (tipo `media-analytics:new-session`). Armazene este valor e passe-o como `sessionID` em todos os eventos subsequentes.

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

Chame `trackSessionStart` com um objeto de mídia e metadados opcionais.

**iOS (Swift)**

```swift
let mediaObject = Media.createMediaObjectWith(name: "video-123",
                                               id: "video-id-123",
                                           length: 128,
                                       streamType: MediaConstants.StreamType.VOD,
                                        mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val mediaObject = Media.createMediaObject("video-123",
                                          "video-id-123",
                                          128,
                                          MediaConstants.StreamType.VOD,
                                          Media.MediaType.Video)

tracker.trackSessionStart(mediaObject, null)
```

## Roku (BrightScript)

Chame `createMediaSession` com os detalhes de sessão necessários:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
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

Chame o ponto de extremidade [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart). A resposta inclui a ID da sessão em `handle[].payload[].sessionId` (tipo `media-analytics:new-session`).

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "playerName": "HTML5 Player",
          "contentType": "VOD",
          "length": 128,
          "channel": "Sports"
        },
        "playhead": 0
      }
    }
  }]
}'
```

## SDK de mídia

Chame `trackSessionStart` com um objeto de mídia criado usando `ADB.Media.createMediaObject`:

```javascript
var mediaObject = ADB.Media.createMediaObject(
  "video-123",                  // name
  "video-id-123",               // media ID
  128,                          // length (seconds)
  ADB.Media.StreamType.VOD,     // stream type
  ADB.Media.MediaType.Video     // media type
);

tracker.trackSessionStart(mediaObject, null);
```

## API da coleção de mídia

Enviar uma POSTAGEM `sessionStart` para o [ponto de extremidade de sessões](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md). O cabeçalho de resposta `Location` contém a ID de sessão a ser usada em todas as solicitações de evento subsequentes.

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.channel": "Sports",
    "media.playerName": "HTML5 Player",
    "media.contentType": "vod",
    "media.length": 128,
    "media.id": "video-123"
  }
}
```
