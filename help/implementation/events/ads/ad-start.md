---
title: Início do anúncio
description: Sinal de que um anúncio individual começou a ser reproduzido.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 7%

---


# Início do anúncio

O evento de início do anúncio sinaliza que um anúncio individual começou a ser reproduzido. Isso deve ocorrer dentro de um par [Ad break start](ad-break-start.md) / [Ad break complete](ad-break-complete.md).

* **Pré-requisitos**: [Início da sessão](../session/session-start.md), [Início de quebra de anúncio](ad-break-start.md)
* **Métrica associada**: [[!UICONTROL Início do anúncio]](/help/reporting/metrics/ad-starts.md)

>[!IMPORTANT]
>
>Este evento deve estar entre `adBreakStart` e `adBreakComplete` delimitadores, mesmo quando um único anúncio é reproduzido. Sem esses delimitadores, os eventos de anúncio são ignorados e a duração do anúncio é contada como a duração do conteúdo principal.

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

Chame [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview) com `eventType: "media.adStart"` e o `advertisingDetails` necessário:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        friendlyName: "Ford F-150",
        length: 15,
        playerName: "Freewheel",
        podPosition: 0
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Passe o nome do anúncio, a ID, a posição do pod e o comprimento para `createAdObject`, depois chame `trackEvent`.

```swift
let adObject = Media.createAdObjectWith(name: "Ford F-150",
                                          id: "ad-2125",
                                    position: 0,
                                      length: 15)

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: nil)
```

>[!TAB Android]

Passe o nome do anúncio, a ID, a posição do pod e o comprimento para `createAdObject`, depois chame `trackEvent`.

```kotlin
val adObject = Media.createAdObject("Ford F-150",
                                    "ad-2125",
                                    0,
                                    15)

tracker.trackEvent(Media.Event.AdStart, adObject, null)
```

>[!TAB Roku Edge]

Chame `sendMediaEvent` com `eventType: "media.adStart"` e o(a) `advertisingDetails` necessário(a):

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "friendlyName": "Ford F-150",
                "length": 15,
                "playerName": "Roku Player",
                "podPosition": 0
            },
            "playhead": 0
        }
    }
})
```

>[!TAB API do Media Edge]

Chame o ponto de extremidade [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) com o `advertisingDetails` necessário:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0,
        "advertisingDetails": {
          "name": "ad-2125",
          "length": 15,
          "playerName": "Freewheel",
          "podPosition": 0
        }
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

>[!ENDTABS]

## Tipos de implementação herdada (somente Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Passar o nome, a ID, a posição e o comprimento do anúncio para `ADB.Media.createAdObject`:

```javascript
var adInfo = ADB.Media.createAdObject(
  "Ford F-150",  // name (friendly name)
  "ad-2125",     // ad ID
  0,             // position in pod
  15             // length (seconds)
);

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, null);
```

>[!TAB Chromecast]

Passar o nome, a ID, a posição e o comprimento do anúncio para `ADBMobile.media.createAdObject`:

```javascript
var adInfo = ADBMobile.media.createAdObject(
  "Ford F-150",  // name (friendly name)
  "ad-2125",     // ad ID
  0,             // position in pod
  15             // length (seconds)
);

ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, null);
```

>[!TAB Roku 2.x]

Crie um objeto de anúncio com `adb_media_init_adinfo` e acompanhe o evento. A posição do anúncio no pod é baseada em 1.

```brightscript
adb = ADBMobile()
adInfo = adb_media_init_adinfo("Ford F-150", "ad-2125", 1, 15.0)  ' name, id, position, length

adb.mediaTrackEvent(adb.MEDIA_AD_START, adInfo)
```

>[!TAB API da coleção de mídia]

Enviar uma POSTAGEM `adStart` para o [ponto de extremidade de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.id": "ad-2125",
    "media.ad.name": "Ford F-150",
    "media.ad.length": 15,
    "media.ad.podPosition": 0
  }
}
```

>[!ENDTABS]
