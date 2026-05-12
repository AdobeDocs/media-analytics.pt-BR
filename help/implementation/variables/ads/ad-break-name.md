---
title: Nome do ad break
description: Defina o nome amigável do ad break principal.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 12%

---


# Nome do ad break

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados para a variável **Ad break name**. Consulte [Nome do pod](/help/reporting/dimensions/pod-name.md) para a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A variável de nome do ad break é o nome amigável do ad break (por exemplo, `"pre-roll"`, `"mid-roll-1"`, `"post-roll"`). O valor é definido no objeto ad-break, não em anúncios individuais.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.ad.podFriendlyName` |
| **Campo da coleção XDM** | [`mediaCollection.advertisingPodDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-collection) |
| **Obrigatório** | Sim (Mobile SDK); Não (Edge, API Media Collection) |
| **Enviado com** | Início do anúncio, fechamento do anúncio |

## SDK da web

Definir `friendlyName` dentro de `mediaCollection.advertisingPodDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview) para `media.adBreakStart`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adBreakStart",
    mediaCollection: {
      advertisingPodDetails: {
        friendlyName: "pre-roll",
        index: 1,
        offset: 0
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## SDK móvel

Passe o nome do ad break como o primeiro argumento (`name`) para `createAdBreakObject` e, em seguida, rastreie o evento ad-break-start antes do evento ad-start.

**iOS (Swift)**

```swift
let adBreakObject = Media.createAdBreakObjectWith(name: "pre-roll",
                                              position: 1,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.AdBreakStart, info: adBreakObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val adBreakObject = Media.createAdBreakObject("pre-roll",
                                              1L,
                                              0.0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

## Roku (BrightScript)

Definir `friendlyName` dentro de `mediaCollection.advertisingPodDetails` ao chamar `sendMediaEvent` para `media.adBreakStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adBreakStart",
        "mediaCollection": {
            "advertisingPodDetails": {
                "friendlyName": "pre-roll",
                "index": 1,
                "offset": 0
            },
            "playhead": 0
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [adBreakStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakstart) com `friendlyName` dentro de `mediaCollection.advertisingPodDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakStart",
      "mediaCollection": {
        "advertisingPodDetails": {
          "friendlyName": "pre-roll",
          "index": 1,
          "offset": 0
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## SDK de mídia

Passar o nome do ad break como primeiro argumento para `ADB.Media.createAdBreakObject`:

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "pre-roll",
  1,
  0
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

## API da coleção de mídia

Inclua `media.ad.podFriendlyName` no objeto `params` de sua solicitação POST `adBreakStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adBreakStart",
  "params": {
    "media.ad.podFriendlyName": "pre-roll"
  }
}
```

Consulte a [Referência de eventos da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) para obter a estrutura de solicitação completa.
