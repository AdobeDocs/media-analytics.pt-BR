---
title: ID da campanha
description: Defina o identificador de campanha para cada anúncio para que o engajamento possa ser agregado pela campanha.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 10%

---


# ID da campanha

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados para a variável **ID da Campanha**. Consulte [ID da campanha](/help/reporting/dimensions/campaign-id.md) para a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A variável ID da campanha identifica a campanha publicitária à qual o criativo pertence. Qualquer valor da string (normalmente uma ID de campanha da plataforma do servidor de anúncios) é aceitável. Use a variável para acumular engajamento em várias criações que compartilham uma campanha.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.ad.campaign` |
| **Campo da coleção XDM** | [`xdm.mediaCollection.advertisingDetails.campaignID`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Característica do Audience Manager** | `c_contextdata.a.media.ad.campaign` |
| **Obrigatório** | Não |
| **Enviado com** | [Início do anúncio](/help/implementation/events/ads/ad-start.md) e fechamento |

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

Definir `campaignID` dentro de `xdm.mediaCollection.advertisingDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        campaignID: "fall-2024"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Passe a ID da campanha como uma chave de metadados no argumento HashMap para `trackEvent(AdStart)`. Use `MediaConstants.AdMetadataKeys.CAMPAIGN_ID`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.CAMPAIGN_ID] = "fall-2024"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

>[!TAB Android]

Passe a ID da campanha como uma chave de metadados no argumento HashMap para `trackEvent(AdStart)`. Use `MediaConstants.AdMetadataKeys.CAMPAIGN_ID`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.CAMPAIGN_ID] = "fall-2024"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

>[!TAB Roku]

Definir `campaignID` dentro de `xdm.mediaCollection.advertisingDetails` ao chamar `sendMediaEvent` para `media.adStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "campaignID": "fall-2024"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB API do Media Edge]

Chame o ponto de extremidade [adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart) com `campaignID` dentro de `xdm.mediaCollection.advertisingDetails`:

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
          "campaignID": "fall-2024"
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

Passe a ID da campanha no objeto `contextData` usando `ADB.Media.AdMetadataKeys.CampaignId`:

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.CampaignId] = "fall-2024";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

>[!TAB Chromecast]

Defina a ID da campanha usando `ADBMobile.media.AdMetadataKeys.CAMPAIGN_ID` no objeto de metadados de anúncio padrão:

```javascript
var adInfo = ADBMobile.media.createAdObject("Ford F-150", "ad-2125", 1, 30);
var standardAdMetadata = {};
standardAdMetadata[ADBMobile.media.AdMetadataKeys.CAMPAIGN_ID] = "fall-2024";
adInfo[ADBMobile.media.MediaObjectKey.StandardAdMetadata] = standardAdMetadata;
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, null);
```

>[!TAB API da coleção de mídia]

Incluir `media.ad.campaignId` no objeto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.campaignId": "fall-2024"
  }
}
```

Consulte a [Referência de eventos da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) para obter a estrutura de solicitação completa.

>[!ENDTABS]
