---
title: Tipo de transmissão
description: Defina o tipo de fluxo para identificar se um fluxo de mídia é conteúdo de áudio ou vídeo.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 7%

---


# Tipo de transmissão

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados para a variável **Tipo de fluxo**. Consulte [Tipo de fluxo](/help/reporting/dimensions/stream-type.md) para a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A variável de tipo de fluxo identifica se um fluxo de mídia é conteúdo de áudio ou vídeo. É necessário para todas as implementações de mídia de transmissão e deve ser definido no início de cada sessão de mídia.

A definição correta do tipo de fluxo é fundamental para os relatórios de mídia de transmissão. Ele habilita os segmentos **Tipo de Fluxo de Mídia** integrados no Adobe Analytics (todas as mídias, somente Áudio, somente Vídeo) e direciona relatórios de áudio e vídeo separados no Customer Journey Analytics. Também garante que os dados da sessão sejam classificados corretamente no pipeline de análise de mídia. As sessões com um tipo de fluxo não definido ou inválido podem ser desagrupadas ou classificadas incorretamente nos relatórios downstream.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.streamType` |
| **Campo da coleção XDM** | [`xdm.mediaCollection.sessionDetails.streamType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Característica do Audience Manager** | `c_contextdata.a.media.streamType` |
| **Obrigatório** | Sim |
| **Enviado com** | [Início da sessão](/help/implementation/events/session/session-start.md), fechamento da sessão |

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

Definir `streamType` dentro de `xdm.mediaCollection.sessionDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        friendlyName: "My Video",
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

Passar `Media.MediaType.Video` ou `Media.MediaType.Audio` como argumento `mediaType` para `createMediaObject`. Observe que o argumento `streamType` em `createMediaObject` controla a variável do tipo Content (VOD, Live, etc.), não essa variável.

```swift
let mediaObject = Media.createMediaObjectWith(name: "video-123",
                                                id: "video-id",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

>[!TAB Android]

Passar `Media.MediaType.Video` ou `Media.MediaType.Audio` como argumento `mediaType` para `createMediaObject`. Observe que o argumento `streamType` em `createMediaObject` controla a variável do tipo Content (VOD, Live, etc.), não essa variável.

```kotlin
var mediaInfo = Media.createMediaObject("video-123",
                                        "video-id",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

>[!TAB Roku]

Definir `streamType` dentro de `xdm.mediaCollection.sessionDetails` ao chamar `createMediaSession`:

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

>[!TAB API do Media Edge]

Chame o ponto de extremidade [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) com `streamType` dentro de `xdm.mediaCollection.sessionDetails`:

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
          "streamType": "video"
        },
        "playhead": 0
      }
    }
  }]
}
```

>[!ENDTABS]

## Tipos de implementação herdada (somente Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Passar `ADB.Media.MediaType.Video` ou `ADB.Media.MediaType.Audio` como quinto argumento para `Media.createMediaObject`:

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",               // name
  "video-123",              // media ID
  128,                      // length (seconds)
  ADB.Media.StreamType.VOD, // content type
  ADB.Media.MediaType.Video // stream type: Video or Audio
);

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

Passar `ADBMobile.media.MediaType.Video` ou `ADBMobile.media.MediaType.Audio` como quinto argumento para `ADBMobile.media.createMediaObject`:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject(
  "My Video",
  "video-123",
  128,
  ADBMobile.media.StreamType.VOD,
  ADBMobile.media.MediaType.Video
);
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB API da coleção de mídia]

Inclua `media.streamType` no objeto `params` de sua solicitação POST `sessionStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.streamType": "video"
  }
}
```

Consulte a [Referência de sessões da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obter a estrutura de solicitação completa e todos os campos obrigatórios.

>[!ENDTABS]
