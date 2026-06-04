---
title: Versão do aplicativo
description: Configure a sequência de caracteres da versão do aplicativo de reprodução de mídia.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 2%

---


# Versão do aplicativo

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados da variável **Versão do aplicativo**. Consulte [Versão do aplicativo](/help/reporting/dimensions/app-version.md) para a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A variável de versão do aplicativo identifica a versão do aplicativo de reprodutor de mídia. Defina-o uma vez durante a inicialização do SDK; o valor é incluído automaticamente em cada solicitação de início de sessão subsequente. Use uma cadeia de caracteres de versão que corresponda ao ciclo de lançamento do aplicativo (por exemplo, `"2.1.0"` ou `"prod-YYYY-03-15"`).

>[!NOTE]
>
>Este campo captura a versão do seu **aplicativo de reprodutor de mídia**, não a biblioteca SDK da Adobe. A própria versão da biblioteca SDK do Adobe é coletada automaticamente como um campo interno separado.

| Propriedade | Valor |
| --- | --- |
| **Campo da coleção XDM** | [`xdm.mediaCollection.sessionDetails.appVersion`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Parâmetro da API da coleção de mídia** | `media.sdkVersion` |
| **Obrigatório** | Não |
| **Enviado com** | [Início da sessão](/help/implementation/events/session/session-start.md) |

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

Definir `appVersion` no objeto de configuração `streamingMedia` ao chamar [`configure`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/configure/streamingmedia):

```javascript
alloy("configure", {
  streamingMedia: {
    channel: "Sports Channel",
    playerName: "HTML5 Player",
    appVersion: "2.1.0",
    mainPingInterval: 10,
    adPingInterval: 10
  }
});
```

>[!TAB iOS]

Defina `edgeMedia.appVersion` na configuração do aplicativo antes de inicializar o rastreador de mídia:

```swift
var config: [String: Any] = [:]
config["edgeMedia.channel"] = "sample_channel"
config["edgeMedia.playerName"] = "player_name"
config["edgeMedia.appVersion"] = "2.1.0"
MobileCore.updateConfiguration(config)
```

>[!TAB Android]

Defina `edgeMedia.appVersion` na configuração do aplicativo antes de inicializar o rastreador de mídia:

```kotlin
val config: Map<String, Any> = mapOf(
    "edgeMedia.channel" to "sample_channel",
    "edgeMedia.playerName" to "player_name",
    "edgeMedia.appVersion" to "2.1.0"
)
MobileCore.updateConfiguration(config)
```

>[!TAB Roku]

Defina a versão do aplicativo na configuração do SDK usando `ADB_CONSTANTS.CONFIGURATION.MEDIA_APP_VERSION`:

```brightscript
ADB_CONSTANTS = AdobeAEPSDKConstants()
configuration = {}
configuration[ADB_CONSTANTS.CONFIGURATION.EDGE_CONFIG_ID] = "<YOUR_CONFIG_ID>"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_CHANNEL] = "channel_name"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_PLAYER_NAME] = "player_name"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_APP_VERSION] = "2.1.0"
m.aepSdk.updateConfiguration(configuration)
```

>[!TAB API do Media Edge]

Incluir `appVersion` no objeto `sessionDetails` da solicitação [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart):

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "length": 300,
          "contentType": "vod",
          "playerName": "HTML5 Player",
          "channel": "Sports",
          "appVersion": "2.1.0"
        },
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

Defina `appVersion` no objeto `MediaConfig` antes de chamar `ADB.Media.configure`:

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.playerName = "player_name";
mediaConfig.channel = "sample_channel";
mediaConfig.appVersion = "2.1.0";
ADB.Media.configure(mediaConfig, appMeasurement);
```

>[!TAB Chromecast]

Defina `sdkVersion` na seção `mediaHeartbeat` da configuração do ADBMobile. Esse campo captura a versão do aplicativo do player, não a versão da biblioteca SDK do Chromecast.

```javascript
var ADBMobileConfig = {
  "mediaHeartbeat": {
    "server": "obumobile5.hb-api.omtrdc.net",
    "publisher": "<YOUR_PUBLISHER_ID>@AdobeOrg",
    "channel": "sample-channel",
    "ssl": true,
    "playerName": "Chromecast Player",
    "sdkVersion": "2.1.0"
  }
};
```

>[!TAB API da coleção de mídia]

Inclua `media.sdkVersion` no objeto `params` de sua solicitação POST `sessionStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.playerName": "sample-html5-api-player",
    "media.sdkVersion": "2.1.0",
    "media.channel": "sample-channel"
  }
}
```

Consulte a [Referência de sessões da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obter a estrutura de solicitação completa.

>[!ENDTABS]
