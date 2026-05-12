---
title: Nome do reprodutor de conteúdo
description: Defina o nome do reprodutor para identificar qual reprodutor renderizou o conteúdo.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 11%

---


# Nome do reprodutor de conteúdo

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados para a variável **Nome do reprodutor de conteúdo**. Consulte [Nome do player de conteúdo](/help/reporting/dimensions/content-player-name.md) para a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A variável de nome do player de conteúdo identifica qual player renderizou o conteúdo (por exemplo, `HTML5 Player`, `Brightcove` ou `Roku Player`). É necessário para todas as implementações de mídia de transmissão e deve ser definido no início da sessão. O valor é usado na dimensão Nome do reprodutor de conteúdo para comparar engajamento e qualidade entre os reprodutores na mesma propriedade.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.playerName` |
| **Campo da coleção XDM** | [`mediaCollection.sessionDetails.playerName`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Obrigatório** | Sim |
| **Enviado com** | Início da sessão, fechamento da sessão |

## SDK da web

Definir `playerName` dentro de `mediaCollection.sessionDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

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

Defina o nome do reprodutor por meio da configuração do rastreador ao criar o rastreador, usando `MediaConstants.TrackerConfig.PLAYER_NAME`. O nome do reprodutor não faz parte do objeto de mídia.

**iOS (Swift)**

```swift
var config: [String: Any] = [:]
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"

Media.createTrackerWith(config: config) { tracker in
    self.tracker = tracker
}
```

**Android (Kotlin)**

```kotlin
val config = HashMap<String, Any>()
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"

val tracker = Media.createTracker(config)
```

## Roku (BrightScript)

Definir `playerName` dentro de `mediaCollection.sessionDetails` ao chamar `createMediaSession`:

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

Chame o ponto de extremidade [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) com `playerName` dentro de `mediaCollection.sessionDetails`:

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

Defina o nome do reprodutor em `ADB.MediaConfig` antes de criar o rastreador:

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "your.tracking.server";
mediaConfig.playerName = "HTML5 Player";
mediaConfig.channel = "Sports";

var tracker = ADB.Media.getInstance(mediaConfig);
```

## API da coleção de mídia

Inclua `media.playerName` no objeto `params` de sua solicitação POST `sessionStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.playerName": "HTML5 Player"
  }
}
```

Consulte a [Referência de sessões da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obter a estrutura de solicitação completa.
