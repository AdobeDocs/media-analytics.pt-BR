---
title: URL da arte
description: Defina o URL do criativo do anúncio para cada anúncio.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 16%

---


# URL da arte

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados para a variável **URL do Creative**. Consulte [URL do Creative](/help/reporting/dimensions/creative-url.md) para a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A variável creative URL é o URL da campanha criativa. Use a variável para rastrear a localização do ativo de cada criação quando o próprio URL for significativo para a análise (por exemplo, distinção entre caminhos CDN ou versões criativas).

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.ad.creativeURL` |
| **Campo da coleção XDM** | [`mediaCollection.advertisingDetails.creativeURL`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Característica do Audience Manager** | `c_contextdata.a.media.ad.creativeURL` |
| **Obrigatório** | Não |
| **Enviado com** | [Início do anúncio](/help/implementation/events/ads/ad-start.md) e fechamento |

## SDK da web

Definir `creativeURL` dentro de `mediaCollection.advertisingDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        creativeURL: "https://cdn.example.com/ads/creative-987.mp4"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## SDK móvel

Passe a URL criativa como uma chave de metadados no argumento HashMap para `trackEvent(AdStart)`. Use `MediaConstants.AdMetadataKeys.CREATIVE_URL`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.CREATIVE_URL] = "https://cdn.example.com/ads/creative-987.mp4"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.CREATIVE_URL] = "https://cdn.example.com/ads/creative-987.mp4"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

## Roku (BrightScript)

Definir `creativeURL` dentro de `mediaCollection.advertisingDetails` ao chamar `sendMediaEvent` para `media.adStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "creativeURL": "https://cdn.example.com/ads/creative-987.mp4"
            },
            "playhead": 0
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) com `creativeURL` dentro de `mediaCollection.advertisingDetails`:

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
          "creativeURL": "https://cdn.example.com/ads/creative-987.mp4"
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## SDK de mídia

Passar a URL criativa no objeto `contextData` usando `ADB.Media.AdMetadataKeys.CreativeUrl`:

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.CreativeUrl] = "https://cdn.example.com/ads/creative-987.mp4";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

## API da coleção de mídia

Incluir `media.ad.creativeURL` no objeto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.creativeURL": "https://cdn.example.com/ads/creative-987.mp4"
  }
}
```

Consulte a [Referência de eventos da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) para obter a estrutura de solicitação completa.
