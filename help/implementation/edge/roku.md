---
title: Configurar Roku para mídia de transmissão
description: Configure o Adobe Experience Platform Roku SDK para enviar dados de streaming de mídia para a Edge Network.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# Configurar Roku para mídia de transmissão

O [Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku) (BrightScript) coleta dados da sessão de mídia no canal Roku e os envia para a Edge Network. O Roku está configurado no código; ele não usa tags.

* **Pré-requisitos**:
   * Conclua a [visão geral da implementação do Edge](overview.md) (esquema, conjunto de dados, sequência de dados com o [!UICONTROL Media Analytics] habilitado).
   * Baixe a SDK das [versões do GitHub](https://github.com/adobe/aepsdk-roku/releases) e adicione-a ao seu canal, conforme descrito no [guia de introdução](https://github.com/adobe/aepsdk-roku/blob/main/Documentation/getting-started.md).

## Configurar o AEP Roku SDK para mídia

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
>Enviar um evento `media.ping` pelo menos uma vez por segundo com o valor mais recente do indicador de reprodução durante a reprodução. O AEP Roku SDK depende desses pings para funcionar corretamente.

Para obter as chaves de configuração e a API completa, consulte a [Referência da API do AEP Roku SDK](https://github.com/adobe/aepsdk-roku/blob/main/Documentation/api-reference.md).

## Rastrear eventos de mídia

Depois que a sessão estiver aberta, envie cada evento de mídia com `sendMediaEvent`. Consulte a guia **Roku** em cada página de [evento](/help/implementation/events/overview.md) e [variável](/help/implementation/variables/overview.md) para obter as cargas exatas.

## Próxima etapa

Uma vez concluída a implementação, você pode [Configurar relatórios para implementações do Edge](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku)
>* [Visão geral dos eventos](/help/implementation/events/overview.md)
>* [Visão geral das variáveis](/help/implementation/variables/overview.md)
