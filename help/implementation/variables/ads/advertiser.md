---
title: Anunciante
description: Defina a empresa ou marca em destaque em cada anúncio.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 16%

---


# Anunciante

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados para a variável **Anunciante**. Consulte [Anunciante](/help/reporting/dimensions/advertiser.md) para a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A variável do anunciante é a empresa ou marca apresentada no anúncio (por exemplo, `"Ford"` ou `"Coca-Cola"`). Use a variável para cancelar o engajamento e a conclusão pelo anunciante.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.ad.advertiser` |
| **Campo da coleção XDM** | [`mediaCollection.advertisingDetails.advertiser`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Obrigatório** | Não |
| **Enviado com** | Início do anúncio, fechamento do anúncio |

## SDK da web

Definir `advertiser` dentro de `mediaCollection.advertisingDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        advertiser: "Ford"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## SDK móvel

Passe o anunciante como uma chave de metadados no argumento HashMap para `trackEvent(AdStart)`. Use `MediaConstants.AdMetadataKeys.ADVERTISER`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.ADVERTISER] = "Ford"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.ADVERTISER] = "Ford"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

## Roku (BrightScript)

Definir `advertiser` dentro de `mediaCollection.advertisingDetails` ao chamar `sendMediaEvent` para `media.adStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "advertiser": "Ford"
            },
            "playhead": 0
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) com `advertiser` dentro de `mediaCollection.advertisingDetails`:

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
          "podPosition": 0,
          "advertiser": "Ford"
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## SDK de mídia

Passar o anunciante no objeto `contextData` usando `ADB.Media.AdMetadataKeys.Advertiser`:

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.Advertiser] = "Ford";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

## API da coleção de mídia

Incluir `media.ad.advertiser` no objeto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.advertiser": "Ford"
  }
}
```

Consulte a [Referência de eventos da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) para obter a estrutura de solicitação completa.
