---
title: Início da sessão
description: Sinalize o início de uma sessão de mídia e obtenha a ID de sessão necessária para todos os eventos subsequentes.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 4%

---


# Início da sessão

O evento de início de sessão abre uma sessão de rastreamento de mídia. Deve ser o primeiro evento enviado para qualquer reprodução. A resposta retorna uma ID de sessão que todos os eventos subsequentes da mesma sessão devem incluir.

Uma sessão expira automaticamente se **nenhum evento for recebido por 10 minutos** ou se houver **nenhum movimento do indicador de reprodução por 30 minutos**. Se uma sessão expirar, você deverá chamar o início da sessão novamente para obter uma nova ID de sessão.

* **Pré-requisitos**: nenhum; sempre o primeiro evento
* **Métrica associada**: [[!UICONTROL Inícios de mídia]](/help/reporting/metrics/media-starts.md)

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

Chame `trackSessionStart` com um objeto de mídia e metadados opcionais.

```swift
let mediaObject = Media.createMediaObjectWith(name: "video-123",
                                               id: "video-id-123",
                                           length: 128,
                                       streamType: MediaConstants.StreamType.VOD,
                                        mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

>[!TAB Android]

Chame `trackSessionStart` com um objeto de mídia e metadados opcionais.

```kotlin
val mediaObject = Media.createMediaObject("video-123",
                                          "video-id-123",
                                          128,
                                          MediaConstants.StreamType.VOD,
                                          Media.MediaType.Video)

tracker.trackSessionStart(mediaObject, null)
```

>[!TAB Roku Edge]

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

>[!TAB API do Media Edge]

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

>[!ENDTABS]

## Tipos de implementação herdada (somente Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

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

>[!TAB Chromecast]

Chame `trackSessionStart` com um objeto de mídia criado usando `ADBMobile.media.createMediaObject`:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject(
  "video-123",                        // name
  "video-id-123",                     // media ID
  128,                                // length (seconds)
  ADBMobile.media.StreamType.VOD,
  ADBMobile.media.MediaType.Video
);

ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

Criar um objeto de mídia com `adb_media_init_mediainfo` e chamar `mediaTrackSessionStart`. O segundo argumento opcional aceita uma matriz associativa de `a.media.*` chaves de metadados ou `invalid`:

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("video-123", "video-id-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB API da coleção de mídia]

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

>[!ENDTABS]

## Retomar uma sessão

Ao retomar uma sessão fechada anteriormente (por exemplo, após uma transferência entre dispositivos ou após o aplicativo restaurar o estado de reprodução salvo), defina o sinalizador de retomada no início da sessão. Isso faz com que o Analytics incremente [[!UICONTROL Resumo do conteúdo]](/help/reporting/metrics/content-resumes.md) em vez de [[!UICONTROL Inícios da mídia]](/help/reporting/metrics/media-starts.md).

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

Adicionar `hasResume: true` a `sessionDetails`:

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
        streamType: "video",
        hasResume: true
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Defina a chave `resumed` no objeto de mídia antes de chamar `trackSessionStart`:

```swift
var mediaObject = Media.createMediaObjectWith(name: "video-123",
                                               id: "video-id-123",
                                           length: 128,
                                       streamType: MediaConstants.StreamType.VOD,
                                        mediaType: MediaType.Video)

mediaObject[MediaConstants.MediaObjectKey.resumed] = true
tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

>[!TAB Android]

Defina a chave `RESUMED` no objeto de mídia antes de chamar `trackSessionStart`:

```kotlin
val mediaObject = Media.createMediaObject("video-123", "video-id-123", 128,
                                          MediaConstants.StreamType.VOD,
                                          Media.MediaType.Video)

mediaObject[Media.MediaObjectKey.RESUMED] = true
tracker.trackSessionStart(mediaObject, null)
```

>[!TAB Roku Edge]

Adicionar `"hasResume": true` a `sessionDetails`:

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
                "streamType": "video",
                "hasResume": true
            },
            "playhead": 0
        }
    }
})
```

>[!TAB API do Media Edge]

Adicionar `"hasResume": true` a `sessionDetails`:

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
          "channel": "Sports",
          "hasResume": true
        },
        "playhead": 0
      }
    }
  }]
}'
```

>[!ENDTABS]

## Tipos de implementação herdada (somente Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Definir a chave `MediaResumed` no objeto de mídia:

```javascript
var mediaObject = ADB.Media.createMediaObject(
  "video-123", "video-id-123", 128,
  ADB.Media.StreamType.VOD, ADB.Media.MediaType.Video
);

mediaObject[ADB.Media.MediaObjectKey.MediaResumed] = true;
tracker.trackSessionStart(mediaObject, null);
```

>[!TAB Chromecast]

Definir a chave `MediaResumed` no objeto de mídia:

```javascript
var mediaObject = ADBMobile.media.createMediaObject(
  "video-123", "video-id-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video
);

mediaObject[ADBMobile.media.MediaObjectKey.MediaResumed] = true;
ADBMobile.media.trackSessionStart(mediaObject, null);
```

>[!TAB Roku 2.x]

Defina a chave `resumed` no objeto de mídia antes de chamar `mediaTrackSessionStart`:

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("video-123", "video-id-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)
mediaInfo.resumed = true

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB API da coleção de mídia]

Adicionar `"media.resume": true` ao objeto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.channel": "Sports",
    "media.playerName": "HTML5 Player",
    "media.contentType": "vod",
    "media.length": 128,
    "media.id": "video-123",
    "media.resume": true
  }
}
```

>[!ENDTABS]
