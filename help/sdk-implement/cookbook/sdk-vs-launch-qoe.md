---
seo-title: Understand Launch versus Media SDK differences
title: Understand Launch versus Media SDK differences
uuid: null
translation-type: tm+mt
source-git-commit: 932af09a0692ef35ab46fb6f34b2dec5f2e1e562

---


# Entenda as diferenças de inicialização em relação ao SDK de mídia

## Feature differences

* *Launch* - o Launch fornece uma interface que orienta você na configuração, configuração e implantação das soluções de rastreamento de mídia baseadas na Web. O Launch melhora o Gerenciamento dinâmico de tags (DTM).
* *Media SDK - The Media SDK provides you with media tracking libraries designed for specific platforms (e.g.: Android, iOS, etc.).* A Adobe recomenda o SDK de mídia para rastrear o uso de mídia em seus aplicativos móveis.

## Diferenças na criação do rastreador

### Launch

O Launch oferece duas abordagens para a criação da infraestrutura de rastreamento. Ambas as abordagens usam a Extensão de inicialização do Media Analytics:

1. Use as APIs de rastreamento de mídia de uma página da Web.

   Nesse cenário, a Extensão do Media Analytics exporta as APIs de rastreamento de mídia para uma variável configurada no objeto de janela global:

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. Use as APIs de rastreamento de mídia de outra extensão do Launch.

   Nesse cenário, você usa as APIs de rastreamento de mídia expostas pelos módulos `get-instance` e `media-heartbeat` compartilhados.

   >[!NOTE]
   >
   >Shared Modules are not available for use in web pages. You can only use Shared Modules from another extension.

   Create a  instance using the  Shared Module.
`MediaHeartbeat``get-instance`
Pass a delegate object to  that exposes  and  functions.`get-instance``getQoSObject()``getCurrentPlaybackTime()`

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   Access  constants via the  Shared Module.`MediaHeartbeat``media-heartbeat`

### SDK do Media

1. Add the Media Analytics library to your development project.
1. Create a config object ().`MediaHeartbeatConfig`
1. Implement the delegate protocol, exposing the  and  functions.`getQoSObject()``getCurrentPlaybackTime()`
1. Create a Media Heartbeat instance ().`MediaHeartbeat`

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

* [Launch overview](https://docs.adobe.com/content/help/en/launch/using/overview.html)
* [Extensão MA](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)

### SDK do Media

* [Set up JS](/help/sdk-implement/setup/set-up-js.md)
* [API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

