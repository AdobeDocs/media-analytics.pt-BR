---
title: ID de criação
description: Defina o identificador criativo de cada anúncio.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 10%

---


# ID de criação

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados da variável **Creative ID**. Consulte [Creative ID](/help/reporting/dimensions/creative-id.md) para a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A variável da ID criativa identifica o criativo do anúncio específico. Qualquer valor da string (normalmente uma ID criativa da plataforma do servidor de anúncios) é aceitável.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.ad.creative` |
| **Campo da coleção XDM** | [`xdm.mediaCollection.advertisingDetails.creativeID`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Característica do Audience Manager** | `c_contextdata.a.media.ad.creative` |
| **Obrigatório** | Não |
| **Enviado com** | [Início do anúncio](/help/implementation/events/ads/ad-start.md) e fechamento |

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

Definir `creativeID` dentro de `xdm.mediaCollection.advertisingDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        creativeID: "creative-987"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Passe a ID criativa como uma chave de metadados no argumento HashMap para `trackEvent(AdStart)`. Use `MediaConstants.AdMetadataKeys.CREATIVE_ID`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.CREATIVE_ID] = "creative-987"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

>[!TAB Android]

Passe a ID criativa como uma chave de metadados no argumento HashMap para `trackEvent(AdStart)`. Use `MediaConstants.AdMetadataKeys.CREATIVE_ID`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.CREATIVE_ID] = "creative-987"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

>[!TAB Roku Edge]

Definir `creativeID` dentro de `xdm.mediaCollection.advertisingDetails` ao chamar `sendMediaEvent` para `media.adStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "creativeID": "creative-987"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB API do Media Edge]

Chame o ponto de extremidade [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) com `creativeID` dentro de `xdm.mediaCollection.advertisingDetails`:

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
          "creativeID": "creative-987"
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

Passe a ID criativa no objeto `contextData` usando `ADB.Media.AdMetadataKeys.CreativeId`:

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.CreativeId] = "creative-987";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

>[!TAB Chromecast]

Defina a ID criativa usando `ADBMobile.media.AdMetadataKeys.CREATIVE_ID` no objeto de metadados de anúncio padrão:

```javascript
var adInfo = ADBMobile.media.createAdObject("Ford F-150", "ad-2125", 1, 30);
var standardAdMetadata = {};
standardAdMetadata[ADBMobile.media.AdMetadataKeys.CREATIVE_ID] = "creative-987";
adInfo[ADBMobile.media.MediaObjectKey.StandardAdMetadata] = standardAdMetadata;
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, null);
```

>[!TAB Roku 2.x]

Defina a ID criativa usando `MEDIA_AdMetadataKeyCREATIVE_ID` no objeto de metadados de anúncio padrão:

```brightscript
adb = ADBMobile()
adInfo = adb_media_init_adinfo("Ford F-150", "ad-2125", 1, 30.0)

standardAdMetadata = {}
standardAdMetadata[adb.MEDIA_AdMetadataKeyCREATIVE_ID] = "creative-987"
adInfo[adb.MEDIA_STANDARD_AD_METADATA] = standardAdMetadata

adb.mediaTrackEvent(adb.MEDIA_AD_START, adInfo)
```

>[!TAB API da coleção de mídia]

Incluir `media.ad.creativeId` no objeto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.creativeId": "creative-987"
  }
}
```

Consulte a [Referência de eventos da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) para obter a estrutura de solicitação completa.

>[!ENDTABS]
