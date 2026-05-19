---
title: ID do ativo
description: Defina a ID do ativo, um identificador estável do setor para o ativo de mídia, como um EIDR ou ID do TMS/Gracenote.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 12%

---


# ID do ativo

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados para a variável **ID do ativo**. Consulte [ID do ativo](/help/reporting/dimensions/asset-id.md) para a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A variável ID do ativo é o identificador exclusivo do ativo de mídia subjacente (por exemplo, uma ID de episódio, uma ID de filme ou uma ID de evento em tempo real). Normalmente obtidos de autoridades de metadados, como EIDR, TMS/Gracenote ou Rovi, mas IDs proprietárias ou internas também são aceitas. Use-a quando precisar comparar o envolvimento em plataformas de distribuição que podem atribuir IDs de conteúdo diferentes para o mesmo ativo subjacente.

>[!NOTE]
>
>O campo de coleção XDM usa maiúsculas `ID`: `assetID`.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.asset` |
| **Campo da coleção XDM** | [`mediaCollection.sessionDetails.assetID`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Característica do Audience Manager** | `c_contextdata.a.media.asset` |
| **Obrigatório** | Não |
| **Enviado com** | [Início da sessão](/help/implementation/events/session/session-start.md), fechamento da sessão |

## SDK da web

Definir `assetID` dentro de `mediaCollection.sessionDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        assetID: "89745363"
      },
      playhead: 0
    }
  }
});
```

## SDK móvel

Passe a ID do ativo como uma chave de metadados no argumento HashMap para `trackSessionStart`. Use `MediaConstants.VideoMetadataKeys.ASSET_ID`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.ASSET_ID] = "89745363"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.ASSET_ID] = "89745363"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Use `createMediaSession` para definir `assetID` dentro de `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "assetID": "89745363"
            },
            "playhead": 0
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) com `assetID` dentro de `mediaCollection.sessionDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "length": 128,
          "contentType": "vod",
          "playerName": "HTML5 Player",
          "channel": "Sports",
          "assetID": "89745363"
        },
        "playhead": 0
      }
    }
  }]
}
```

## SDK de mídia

Passar a ID do ativo no objeto `contextData` usando `ADB.Media.VideoMetadataKeys.AssetId`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.AssetId] = "89745363";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API da coleção de mídia

Incluir `media.assetId` no objeto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.assetId": "89745363"
  }
}
```

Consulte a [Referência de sessões da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obter a estrutura de solicitação completa.
