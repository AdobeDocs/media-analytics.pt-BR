---
title: Autorizado
description: Sinalizar uma sessão como autenticada por meio do Adobe Pass para que seja contabilizada para o evento Autorizado.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 15%

---


# Autorizado

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados da variável **Autorizada**. Consulte [Autorizado](/help/reporting/metrics/authorized.md) para obter a métrica de relatório correspondente.*

>[!ENDSHADEBOX]

A variável autorizada sinaliza uma sessão cujo usuário foi autorizado por meio do Adobe Pass/TV-Everywhere. Defina-o como `"TRUE"` quando a autorização for confirmada; caso contrário, deixe-o indefinido. Emparelhe com [MVPD](/help/implementation/variables/standard-metadata/mvpd.md) para interromper a autenticação por provedor.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.pass.auth` |
| **Campo da coleção XDM** | [`mediaCollection.sessionDetails.authorized`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Característica do Audience Manager** | `c_contextdata.a.media.pass.auth` |
| **Obrigatório** | Não |
| **Enviado com** | [Início da sessão](/help/implementation/events/session/session-start.md), fechamento da sessão |

## SDK da web

Definir `authorized` dentro de `mediaCollection.sessionDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        authorized: "TRUE"
      },
      playhead: 0
    }
  }
});
```

## SDK móvel

Passe o sinalizador autorizado como uma chave de metadados no argumento HashMap para `trackSessionStart`. Use `MediaConstants.VideoMetadataKeys.AUTHORIZED`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.AUTHORIZED] = "TRUE"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.AUTHORIZED] = "TRUE"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Use `createMediaSession` para definir `authorized` dentro de `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "authorized": "TRUE"
            },
            "playhead": 0
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) com `authorized` dentro de `mediaCollection.sessionDetails`:

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
          "authorized": "TRUE"
        },
        "playhead": 0
      }
    }
  }]
}
```

## SDK de mídia

Passar o sinalizador autorizado no objeto `contextData` usando `ADB.Media.VideoMetadataKeys.Authorized`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Authorized] = "TRUE";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API da coleção de mídia

Incluir `media.pass.auth` no objeto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.pass.auth": "TRUE"
  }
}
```

Consulte a [Referência de sessões da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obter a estrutura de solicitação completa.
