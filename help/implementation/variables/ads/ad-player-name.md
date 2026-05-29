---
title: Nome do player do anúncio
description: Defina o nome do reprodutor que renderiza os anúncios. O reprodutor de anúncios pode ser diferente do reprodutor de conteúdo principal.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 7%

---


# Nome do player do anúncio

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados para a variável **Nome do player do anúncio**. Consulte [Nome do player do anúncio](/help/reporting/dimensions/ad-player-name.md) para a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A variável de nome do player de anúncio identifica qual player renderizou cada anúncio (por exemplo, `"Freewheel"`, `"Google IMA"`). O reprodutor de anúncios pode diferir do reprodutor de conteúdo principal quando os anúncios são compilados por um serviço de inserção de anúncios do lado do servidor. Use essa variável para comparar a qualidade e a conclusão entre pilhas de veiculação de anúncios.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.ad.playerName` |
| **Campo da coleção XDM** | [`xdm.mediaCollection.advertisingDetails.playerName`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Característica do Audience Manager** | `c_contextdata.a.media.ad.playerName` |
| **Obrigatório** | Sim |
| **Enviado com** | [Início do anúncio](/help/implementation/events/ads/ad-start.md) e fechamento |

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

Definir `playerName` dentro de `xdm.mediaCollection.advertisingDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

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

>[!TAB iOS]

Passe o nome do player de anúncio como a chave `MediaConstants.AdMetadataKeys.AD_PLAYER` no argumento HashMap de metadados para `trackEvent(AdStart)`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.AD_PLAYER] = "Freewheel"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

>[!TAB Android]

Passe o nome do player de anúncio como a chave `MediaConstants.AdMetadataKeys.AD_PLAYER` no argumento HashMap de metadados para `trackEvent(AdStart)`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.AD_PLAYER] = "Freewheel"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

>[!TAB Roku]

Definir `playerName` dentro de `xdm.mediaCollection.advertisingDetails` ao chamar `sendMediaEvent` para `media.adStart`:

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

>[!TAB API do Media Edge]

Chame o ponto de extremidade [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) com `playerName` dentro de `xdm.mediaCollection.advertisingDetails`:

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

Passar o nome do player de anúncio no objeto `contextData` usando `ADB.Media.AdMetadataKeys.AdPlayer`:

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.AdPlayer] = "Freewheel";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

>[!TAB Chromecast]

Passe o nome do reprodutor de anúncios no objeto de metadados de contexto ao rastrear o evento de início do anúncio:

```javascript
var adInfo = ADBMobile.media.createAdObject("Ford F-150", "ad-2125", 1, 30);
var metadata = { "a.media.ad.playerName": "Chromecast Player" };
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, metadata);
```

>[!TAB API da coleção de mídia]

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

>[!ENDTABS]
