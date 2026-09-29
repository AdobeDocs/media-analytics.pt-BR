---
title: Configurar o Roku Edge para mídia de transmissão
description: Configure o Adobe Experience Platform Roku SDK para enviar dados de streaming de mídia para a Edge Network.
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%
---
# Configurar o Roku Edge para mídia de transmissão

O [Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku) (BrightScript) coleta dados da sessão de mídia no canal Roku e os envia para a Edge Network. O Roku está configurado no código; ele não usa tags.

* **Pré-requisitos**:
  * Conclua a [visão geral da implementação do Edge](overview.md) (esquema, conjunto de dados, sequência de dados com o [!UICONTROL Media Analytics] habilitado).
  * Baixe a SDK das [versões do GitHub](https://github.com/adobe/aepsdk-roku/releases) e adicione-a ao seu canal, conforme descrito no [guia de introdução](https://github.com/adobe/aepsdk-roku/blob/main/Documentation/getting-started.md).

## Configurar o Roku Edge SDK para mídia

Inicialize o SDK e defina a configuração do fluxo de dados e da mídia:

```brightscript
m.aepSdk = AdobeAEPSDKInit()
ADB_CONSTANTS = AdobeAEPSDKConstants()

configuration = {}
configuration[ADB_CONSTANTS.CONFIGURATION.EDGE_CONFIG_ID] = "<datastreamID>"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_CHANNEL] = "sample_channel"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_PLAYER_NAME] = "player_name"
m.aepSdk.updateConfiguration(configuration)
```

Em seguida, abra uma sessão com `createMediaSession`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": { "name": "video-123", "length": 128, "contentType": "vod", "streamType": "video" },
            "playhead": 0
        }
    }
})
```

>[!IMPORTANT]
>
>Enviar um evento `media.ping` pelo menos uma vez por segundo com o valor mais recente do indicador de reprodução durante a reprodução. O Roku Edge SDK depende desses pings para funcionar corretamente.

Para obter as chaves de configuração e a API completa, consulte a [Referência da API do SDK do Roku Edge](https://github.com/adobe/aepsdk-roku/blob/main/Documentation/api-reference.md).

## Rastrear eventos de mídia

Depois que a sessão estiver aberta, envie cada evento de mídia com `sendMediaEvent`. Consulte a guia **Roku Edge** em cada página de [evento](/help/implementation/events/overview.md) e [variável](/help/implementation/variables/overview.md) para obter as cargas exatas.

## Próxima etapa

Uma vez concluída a implementação, você pode [Configurar relatórios para implementações do Edge](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku)
>* [Visão geral dos eventos](/help/implementation/events/overview.md)
>* [Visão geral das variáveis](/help/implementation/variables/overview.md)
