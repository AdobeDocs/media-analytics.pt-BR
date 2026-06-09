---
title: Nome do ad break
description: Defina o nome amigável do ad break principal.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 6%

---


# Nome do ad break

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados para a variável **Ad break name**. Consulte [Nome do pod](/help/reporting/dimensions/pod-name.md) para a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A variável de nome do ad break é o nome amigável do ad break (por exemplo, `"pre-roll"`, `"mid-roll-1"`, `"post-roll"`). O valor é definido no objeto ad-break, não em anúncios individuais.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.ad.podFriendlyName` |
| **Campo da coleção XDM** | [`xdm.mediaCollection.advertisingPodDetails.friendlyName`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/advertising-pod-details-collection) |
| **Característica do Audience Manager** | `c_contextdata.a.media.ad.podFriendlyName` |
| **Obrigatório** | Sim (Mobile SDK); Não (Edge, API Media Collection) |
| **Enviado com** | [Início de quebra de anúncio](/help/implementation/events/ads/ad-break-start.md), anúncio fechado |

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

Definir `friendlyName` dentro de `xdm.mediaCollection.advertisingPodDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview) para `media.adBreakStart`:

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

>[!TAB iOS]

Passe o nome do ad break como o primeiro argumento (`name`) para `createAdBreakObject` e, em seguida, rastreie o evento ad-break-start antes do evento ad-start.

```swift
let adBreakObject = Media.createAdBreakObjectWith(name: "pre-roll",
                                              position: 1,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.AdBreakStart, info: adBreakObject, metadata: nil)
```

>[!TAB Android]

Passe o nome do ad break como o primeiro argumento (`name`) para `createAdBreakObject` e, em seguida, rastreie o evento ad-break-start antes do evento ad-start.

```kotlin
val adBreakObject = Media.createAdBreakObject("pre-roll",
                                              1L,
                                              0.0)

tracker.trackEvent(Media.Event.AdBreakStart, adBreakObject, null)
```

>[!TAB Roku Edge]

Definir `friendlyName` dentro de `xdm.mediaCollection.advertisingPodDetails` ao chamar `sendMediaEvent` para `media.adBreakStart`:

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

>[!TAB API do Media Edge]

Chame o ponto de extremidade [adBreakStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakstart) com `friendlyName` dentro de `xdm.mediaCollection.advertisingPodDetails`:

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

>[!ENDTABS]

## Tipos de implementação herdada (somente Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Passar o nome do ad break como primeiro argumento para `ADB.Media.createAdBreakObject`:

```javascript
var adBreakInfo = ADB.Media.createAdBreakObject(
  "pre-roll",
  1,
  0
);

tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakInfo, null);
```

>[!TAB Chromecast]

Passar o nome do ad break como primeiro argumento para `ADBMobile.media.createAdBreakObject`:

```javascript
var adBreakInfo = ADBMobile.media.createAdBreakObject(
  "pre-roll",
  1,
  0
);
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakStart, adBreakInfo);
```

>[!TAB Roku 2.x]

Passar o nome do ad break como primeiro argumento para `adb_media_init_adbreakinfo`. Observe a ordem dos parâmetros Roku: `name, startTime, position`.

```brightscript
adb = ADBMobile()
adBreakInfo = adb_media_init_adbreakinfo("pre-roll", 0.0, 1)  ' name, startTime, position

adb.mediaTrackEvent(adb.MEDIA_AD_BREAK_START, adBreakInfo)
```

>[!TAB API da coleção de mídia]

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

>[!ENDTABS]
