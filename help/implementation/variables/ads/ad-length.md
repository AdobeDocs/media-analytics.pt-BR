---
title: Comprimento do anúncio
description: Defina a duração de cada anúncio em segundos.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 8%

---


# Comprimento do anúncio

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados da variável **Comprimento do anúncio**. Consulte [Comprimento do anúncio](/help/reporting/dimensions/ad-length.md) para a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A variável de duração do anúncio é a duração do anúncio em segundos. Defina-o em cada evento `media.adStart`.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.ad.length` |
| **Campo da coleção XDM** | [`xdm.mediaCollection.advertisingDetails.length`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Característica do Audience Manager** | `c_contextdata.a.media.ad.length` |
| **Obrigatório** | Sim |
| **Enviado com** | [Início do anúncio](/help/implementation/events/ads/ad-start.md) e fechamento |

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

Definir `length` dentro de `xdm.mediaCollection.advertisingDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        length: 15
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Passe a duração do anúncio em segundos como o quarto argumento para `createAdObject`.

```swift
let adObject = Media.createAdObjectWith(name: "Ford F-150",
                                          id: "ad-2125",
                                    position: 0,
                                      length: 15)

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: nil)
```

>[!TAB Android]

Passe a duração do anúncio em segundos como o quarto argumento para `createAdObject`.

```kotlin
val adObject = Media.createAdObject("Ford F-150",
                                    "ad-2125",
                                    0L,
                                    15.0)

tracker.trackEvent(Media.Event.AdStart, adObject, null)
```

>[!TAB Roku Edge]

Definir `length` dentro de `xdm.mediaCollection.advertisingDetails` ao chamar `sendMediaEvent` para `media.adStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "length": 15,
                "podPosition": 0,
                "playerName": "Roku Player"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB API do Media Edge]

Chame o ponto de extremidade [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) com `length` dentro de `xdm.mediaCollection.advertisingDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.adStart",
      "mediaCollection": {
        "advertisingDetails": {
          "name": "ad-2125",
          "length": 15,
          "playerName": "Freewheel",
          "podPosition": 0
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

Passe a duração do anúncio em segundos como o quarto argumento para `ADB.Media.createAdObject`:

```javascript
var adInfo = ADB.Media.createAdObject(
  "Ford F-150",
  "ad-2125",
  0,
  15
);

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

>[!TAB Chromecast]

Passe a duração do anúncio em segundos como o quarto argumento para `ADBMobile.media.createAdObject`:

```javascript
var adInfo = ADBMobile.media.createAdObject(
  "Ford F-150",
  "ad-2125",
  1,
  30
);
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, null);
```

>[!TAB Roku 2.x]

Passe a duração do anúncio em segundos como o quarto argumento para `adb_media_init_adinfo`:

```brightscript
adb = ADBMobile()
adInfo = adb_media_init_adinfo("Ford F-150", "ad-2125", 1, 30.0)  ' name, id, position, length

adb.mediaTrackEvent(adb.MEDIA_AD_START, adInfo)
```

>[!TAB API da coleção de mídia]

Inclua `media.ad.length` no objeto `params` de sua solicitação POST `adStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.length": 15
  }
}
```

Consulte a [Referência de eventos da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) para obter a estrutura de solicitação completa.

>[!ENDTABS]
