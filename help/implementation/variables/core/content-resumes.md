---
title: Resumo de conteúdo
description: Sinalizar uma sessão que retoma uma reprodução interrompida anteriormente para que o back-end conte um evento de Resumo do conteúdo.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 10%

---


# Resumo de conteúdo

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados para a variável **Resumo do conteúdo**. Consulte [Resumo do conteúdo](/help/reporting/metrics/content-resumes.md) para a métrica de relatório correspondente.*

>[!ENDSHADEBOX]

O conteúdo retoma os sinalizadores de variável em uma sessão que retoma uma reprodução interrompida anteriormente. Defina-o em `media.sessionStart` para que o back-end conte um evento de Resumo de conteúdo para a sessão e o exclua das novas contagens de fluxo. Para implementações de API direta e API do Edge, o cliente é responsável por detectar sessões retomadas (por exemplo, depois de um buffer, pausa ou paralisação que exceda 30 minutos) e definir esse sinalizador adequadamente.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.resume` |
| **Campo da coleção XDM** | [`mediaCollection.sessionDetails.hasResume`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Obrigatório** | Não |
| **Enviado com** | Início da sessão |

## SDK da web

Definir `hasResume` como `true` dentro de `mediaCollection.sessionDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview) para a sessão retomada:

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
      playhead: 60
    }
  }
});
```

## SDK móvel

Passe o sinalizador de retomada como parte do conjunto de configurações opcional do objeto de mídia em `trackSessionStart`. Use a chave `MediaConstants.MediaObjectKey.RESUMED`.

**iOS (Swift)**

```swift
var mediaObject = Media.createMediaObjectWith(name: "My Video",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)
mediaObject?[MediaConstants.MediaObjectKey.RESUMED] = true

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val mediaInfo = Media.createMediaObject("My Video",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)
mediaInfo[MediaConstants.MediaObjectKey.RESUMED] = true

tracker.trackSessionStart(mediaInfo, null)
```

## Roku (BrightScript)

Defina `hasResume` como `true` dentro de `mediaCollection.sessionDetails` ao chamar `createMediaSession` para a sessão retomada:

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
            "playhead": 60
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) com `hasResume` definido como `true` dentro de `mediaCollection.sessionDetails`:

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
          "channel": "Sports",
          "hasResume": true
        },
        "playhead": 60
      }
    }
  }]
}
```

## SDK de mídia

Defina a chave `RESUMED` no objeto de informações de mídia antes de chamar `trackSessionStart`:

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",
  "video-123",
  128,
  ADB.Media.StreamType.VOD,
  ADB.Media.MediaType.Video
);
mediaInfo[ADB.Media.MediaObjectKey.Resumed] = true;

tracker.trackSessionStart(mediaInfo, contextData);
```

## API da coleção de mídia

Inclua `media.resume` no objeto `params` de sua solicitação POST `sessionStart`:

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.resume": true
  }
}
```

Consulte a [Referência de sessões da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obter a estrutura de solicitação completa.
