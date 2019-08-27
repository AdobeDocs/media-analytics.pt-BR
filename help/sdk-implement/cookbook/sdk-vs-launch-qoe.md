---
seo-title: Entender Launch versus diferenças de SDK de mídia
title: Entender Launch versus diferenças de SDK de mídia
uuid: null
translation-type: tm+mt
source-git-commit: 932af09a0692ef35ab46fb6f34b2dec5f2e1e562

---


# Entender Launch versus diferenças de SDK de mídia

## Diferenças de recursos

* *Launch* - O Launch fornece uma interface do usuário que o orienta a configurar, configurar e implantar suas soluções de rastreamento de mídia baseadas na Web. O Launch aprimora o Gerenciamento dinâmico de tags (DTM).
* *SDK de mídia* - o SDK de mídia fornece bibliotecas de rastreamento de mídia projetadas para plataformas específicas (por exemplo: Android, iOS, etc.). A Adobe recomenda o SDK de mídia para rastrear o uso de mídia em seus aplicativos móveis.

## Diferenças de criação do rastreador

### Launch

O Launch oferece duas abordagens para a criação da infraestrutura de rastreamento. Ambas as abordagens usam a Extensão de inicialização do Media Analytics:

1. Use as apis de rastreamento de mídia de uma página da Web.

   Neste cenário, a Extensão do Analytics Extension exporta as apis de rastreamento de mídia para uma variável configurada no objeto da janela global:

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. Use as apis de rastreamento de mídia de outra extensão do Launch.

   Neste cenário, você usa as apis de rastreamento de mídia expostas pelos Módulos e `get-instance` Módulos `media-heartbeat` compartilhados.

   >[!NOTE]
   >
   >Módulos compartilhados não estão disponíveis para uso em páginas da Web. Você só pode usar Módulos compartilhados de outra extensão.

   Crie `MediaHeartbeat` uma instância usando o Módulo `get-instance` compartilhado.
Passe um objeto delegado para `get-instance` esse exposto `getQoSObject()` e `getCurrentPlaybackTime()` funções.

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   Acesse `MediaHeartbeat` constantes por meio do `media-heartbeat` Módulo compartilhado.

### SDK do Media

1. Adicione a biblioteca do Analytics ao seu projeto de desenvolvimento.
1. Crie um objeto config (`MediaHeartbeatConfig`).
1. Implemente o protocolo delegado, exposição de funções `getQoSObject()` e `getCurrentPlaybackTime()` funções.
1. Crie uma instância do Media Heartbeat (`MediaHeartbeat`).

```
// Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
...
// Configuration settings
mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER;
...
// Implement Media Delegate (Quality of Service and Playhead)
var mediaDelegate = new MediaHeartbeatDelegate();
...
mediaDelegate.getQoSObject = function() {
    return MediaHeartbeat.createQoSObject(<bitrate>, <startuptime>, <fps>, <droppedFrames>);
    ...
}
...
// Create your tracker
this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
```

## Documentação relacionada

### Launch

* [Visão geral do lançamento](https://docs.adobe.com/content/help/en/launch/using/overview.html)
* [Extensão MA](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)

### SDK do Media

* [Configurar JS](/help/sdk-implement/setup/set-up-js.md)
* [API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

