---
title: Nome do player do anúncio
description: Defina o nome do reprodutor que renderiza os anúncios. O reprodutor de anúncios pode ser diferente do reprodutor de conteúdo principal.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 11%

---


# Nome do player do anúncio

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados para a variável **Nome do player do anúncio**. Consulte [Nome do player do anúncio](/help/reporting/dimensions/ad-player-name.md) para a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A variável de nome do player de anúncio identifica qual player renderizou cada anúncio (por exemplo, `"Freewheel"`, `"Google IMA"`). O reprodutor de anúncios pode diferir do reprodutor de conteúdo principal quando os anúncios são compilados por um serviço de inserção de anúncios do lado do servidor. Use essa variável para comparar a qualidade e a conclusão entre pilhas de veiculação de anúncios.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.ad.playerName` |
| **Campo da coleção XDM** | [`mediaCollection.advertisingDetails.playerName`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Obrigatório** | Sim |
| **Enviado com** | Início do anúncio, fechamento do anúncio |

## SDK da web

Definir `playerName` dentro de `mediaCollection.advertisingDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        playerName: "Freewheel"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## SDK móvel

Passe o nome do player de anúncio como a chave `MediaConstants.AdMetadataKeys.AD_PLAYER` no argumento HashMap de metadados para `trackEvent(AdStart)`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.AD_PLAYER] = "Freewheel"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.AD_PLAYER] = "Freewheel"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

## Roku (BrightScript)

Definir `playerName` dentro de `mediaCollection.advertisingDetails` ao chamar `sendMediaEvent` para `media.adStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "playerName": "Freewheel",
                "length": 15,
                "podPosition": 0
            },
            "playhead": 0
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) com `playerName` dentro de `mediaCollection.advertisingDetails`:

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

## SDK de mídia

Passar o nome do player de anúncio no objeto `contextData` usando `ADB.Media.AdMetadataKeys.AdPlayer`:

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.AdPlayer] = "Freewheel";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

## API da coleção de mídia

Inclua `media.ad.playerName` no objeto `params` de sua solicitação POST `adStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.playerName": "Freewheel"
  }
}
```

Consulte a [Referência de eventos da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) para obter a estrutura de solicitação completa.
