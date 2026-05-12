---
title: MVPD
description: Defina o distribuidor de programação de vídeo multicanal quando o usuário se autenticar via Adobe Pass.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 15%

---


# MVPD

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados da variável **MVPD**. Consulte [MVPD](/help/reporting/dimensions/mvpd.md) para a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A variável MVPD (distribuidor de programação de vídeo multicanal) é o cabo, satélite ou provedor de MVPD virtual pelo qual o usuário se autenticou (por exemplo, `"Comcast"`, `"DirecTV"` ou `"YouTubeTV"`). Defina-o quando o conteúdo estiver protegido por autenticação Adobe Pass ou TV-Everywhere. Emparelhe com [Autorizado](/help/implementation/variables/standard-metadata/authorized.md) para rastrear quais sessões concluíram a autenticação.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.pass.mvpd` |
| **Campo da coleção XDM** | [`mediaCollection.sessionDetails.mvpd`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Obrigatório** | Não |
| **Enviado com** | Início da sessão, fechamento da sessão |

## SDK da web

Definir `mvpd` dentro de `mediaCollection.sessionDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        mvpd: "Comcast"
      },
      playhead: 0
    }
  }
});
```

## SDK móvel

Passe a MVPD como uma chave de metadados no argumento HashMap para `trackSessionStart`. Use `MediaConstants.VideoMetadataKeys.MVPD`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.MVPD] = "Comcast"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.MVPD] = "Comcast"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Use `createMediaSession` para definir `mvpd` dentro de `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "mvpd": "Comcast"
            },
            "playhead": 0
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) com `mvpd` dentro de `mediaCollection.sessionDetails`:

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
          "mvpd": "Comcast"
        },
        "playhead": 0
      }
    }
  }]
}
```

## SDK de mídia

Passar a MVPD no objeto `contextData` usando `ADB.Media.VideoMetadataKeys.MVPD`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.MVPD] = "Comcast";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API da coleção de mídia

Incluir `media.pass.mvpd` no objeto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.pass.mvpd": "Comcast"
  }
}
```

Consulte a [Referência de sessões da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obter a estrutura de solicitação completa.
