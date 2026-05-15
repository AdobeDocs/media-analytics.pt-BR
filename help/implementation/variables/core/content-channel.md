---
title: Canal de conteúdo
description: Defina o canal para identificar a estação de distribuição, rede ou propriedade onde o conteúdo é reproduzido.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 12%

---


# Canal de conteúdo

>[!BEGINSHADEBOX]

*Esta página aborda a coleção de dados da variável **Canal de conteúdo**. Consulte [Canal de conteúdo](/help/reporting/dimensions/content-channel.md) para a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A variável de canal de conteúdo identifica a estação de distribuição, a rede ou a propriedade em que o conteúdo é reproduzido. É necessário para todas as implementações de mídia de transmissão. Qualquer sequência de caracteres é aceita. Os valores típicos incluem um nome de rede, uma parte de um caminho de site ou um identificador de propriedade interno.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.channel` |
| **Campo da coleção XDM** | [`mediaCollection.sessionDetails.channel`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Característica do Audience Manager** | `c_contextdata.a.media.channel` |
| **Obrigatório** | Sim |
| **Enviado com** | [Início da sessão](/help/implementation/events/session/session-start.md), fechamento da sessão |

## SDK da web

Definir `channel` dentro de `mediaCollection.sessionDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

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

Defina o canal por meio da configuração do rastreador ao criar o rastreador, usando `MediaConstants.TrackerConfig.CHANNEL`. O canal não faz parte do objeto de mídia.

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

Definir `channel` dentro de `mediaCollection.sessionDetails` ao chamar `createMediaSession`:

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

Chame o ponto de extremidade [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) com `channel` dentro de `mediaCollection.sessionDetails`:

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

Defina o canal em `ADB.MediaConfig` antes de criar o rastreador:

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "your.tracking.server";
mediaConfig.playerName = "HTML5 Player";
mediaConfig.channel = "Sports";

var tracker = ADB.Media.getInstance(mediaConfig);
```

## API da coleção de mídia

Inclua `media.channel` no objeto `params` de sua solicitação POST `sessionStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.channel": "Sports"
  }
}
```

Consulte a [Referência de sessões da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obter a estrutura de solicitação completa.
