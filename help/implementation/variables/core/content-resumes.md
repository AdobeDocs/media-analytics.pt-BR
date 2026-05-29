---
title: Resumo de conteúdo
description: Sinalizar uma sessão que retoma uma reprodução interrompida anteriormente para que o back-end conte um evento de Resumo do conteúdo.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 7%

---


# Resumo de conteúdo

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados para a variável **Resumo do conteúdo**. Consulte [[!UICONTROL Resumo do conteúdo]](/help/reporting/metrics/content-resumes.md) para a métrica de relatório correspondente.*

>[!ENDSHADEBOX]

O conteúdo retoma os sinalizadores de variável em uma sessão que retoma uma reprodução interrompida anteriormente. Defina-o em `media.sessionStart` para que o back-end conte um evento de [[!UICONTROL Resumo do conteúdo]](/help/reporting/metrics/content-resumes.md) para a sessão e o exclua das novas contagens de fluxo. Para implementações de API direta e API do Edge, o cliente é responsável por detectar sessões retomadas (por exemplo, depois de um buffer, pausa ou paralisação que exceda 30 minutos) e definir esse sinalizador adequadamente.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.resume` |
| **Campo da coleção XDM** | [`xdm.mediaCollection.sessionDetails.hasResume`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Característica do Audience Manager** | N/D |
| **Obrigatório** | Não |
| **Enviado com** | [Início da sessão](/help/implementation/events/session/session-start.md) |

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

Definir `hasResume` como `true` dentro de `xdm.mediaCollection.sessionDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview) para a sessão retomada:

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

>[!TAB iOS]

Passe o sinalizador de retomada como parte do conjunto de configurações opcional do objeto de mídia em `trackSessionStart`. Use a chave `MediaConstants.MediaObjectKey.RESUMED`.

```swift
var mediaObject = Media.createMediaObjectWith(name: "My Video",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)
mediaObject?[MediaConstants.MediaObjectKey.RESUMED] = true

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

>[!TAB Android]

Passe o sinalizador de retomada como parte do conjunto de configurações opcional do objeto de mídia em `trackSessionStart`. Use a chave `MediaConstants.MediaObjectKey.RESUMED`.

```kotlin
val mediaInfo = Media.createMediaObject("My Video",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)
mediaInfo[MediaConstants.MediaObjectKey.RESUMED] = true

tracker.trackSessionStart(mediaInfo, null)
```

>[!TAB Roku]

Defina `hasResume` como `true` dentro de `xdm.mediaCollection.sessionDetails` ao chamar `createMediaSession` para a sessão retomada:

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

>[!TAB API do Media Edge]

Chame o ponto de extremidade [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) com `hasResume` definido como `true` dentro de `xdm.mediaCollection.sessionDetails`:

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

>[!ENDTABS]

## Tipos de implementação herdada (somente Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

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

>[!TAB Chromecast]

Defina `MediaResumed` no objeto de informações de mídia antes de chamar `trackSessionStart`:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
mediaInfo[ADBMobile.media.MediaObjectKey.MediaResumed] = true;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB API da coleção de mídia]

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

>[!ENDTABS]
