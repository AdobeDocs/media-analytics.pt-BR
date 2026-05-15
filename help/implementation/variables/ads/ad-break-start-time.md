---
title: Hora de início do ad break
description: Defina a hora de início (deslocamento) do ad break no conteúdo, em segundos.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 12%

---


# Hora de início do ad break

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados para a variável **Tempo de início de ad break**. Consulte [Posição do pod](/help/reporting/dimensions/pod-position.md) para a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A variável de hora de início do ad break é o deslocamento do ad break no conteúdo, medido em segundos. Para uma exibição antes da exibição, o valor é `0`; para uma exibição durante a exibição, o valor é a posição do indicador de reprodução na qual a interrupção começa.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.ad.podSecond` |
| **Campo da coleção XDM** | [`mediaCollection.advertisingPodDetails.offset`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-collection) |
| **Característica do Audience Manager** | `c_contextdata.a.media.ad.podSecond` |
| **Obrigatório** | Sim |
| **Enviado com** | [Início de quebra de anúncio](/help/implementation/events/ads/ad-break-start.md), anúncio fechado |

## SDK da web

Definir `offset` dentro de `mediaCollection.advertisingPodDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adBreakStart",
    mediaCollection: {
      advertisingPodDetails: {
        friendlyName: "mid-roll-1",
        index: 2,
        offset: 90
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## SDK móvel

Passe a hora de início em segundos como o terceiro argumento para `createAdBreakObject`.

**iOS (Swift)**

```swift
let adBreakObject = Media.createAdBreakObjectWith(name: "mid-roll-1",
                                              position: 2,
                                             startTime: 90)

tracker.trackEvent(event: MediaEvent.AdBreakStart, info: adBreakObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val adBreakObject = Media.createAdBreakObject("mid-roll-1",
                                              2L,
                                              90.0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

## Roku (BrightScript)

Definir `offset` dentro de `mediaCollection.advertisingPodDetails` ao chamar `sendMediaEvent` para `media.adBreakStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adBreakStart",
        "mediaCollection": {
            "advertisingPodDetails": {
                "friendlyName": "mid-roll-1",
                "index": 2,
                "offset": 90
            },
            "playhead": 90
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [adBreakStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakstart) com `offset` dentro de `mediaCollection.advertisingPodDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakStart",
      "mediaCollection": {
        "advertisingPodDetails": {
          "index": 2,
          "offset": 90
        },
        "sessionID": "{sid}",
        "playhead": 90
      }
    }
  }]
}
```

## SDK de mídia

Passe a hora de início como terceiro argumento para `ADB.Media.createAdBreakObject`:

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "mid-roll-1",
  2,
  90
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

## API da coleção de mídia

Inclua `media.ad.podSecond` no objeto `params` de sua solicitação POST `adBreakStart`:

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "adBreakStart",
  "params": {
    "media.ad.podSecond": 90
  }
}
```

Consulte a [Referência de eventos da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) para obter a estrutura de solicitação completa.
