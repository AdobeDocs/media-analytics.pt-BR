---
title: Migração do SDK do Media independente para o Adobe Launch - Web (JS)
description: Instruções e exemplos de código para auxiliar na migração do SDK do Media para o Launch.
translation-type: ht
source-git-commit: bc896cc403923e2f31be7313ab2ca22c05893c45

---


# Migração do SDK do Media independente para o Adobe Launch - Web (JS)

## Diferenças nos recursos

* *Launch* - o Launch fornece uma interface do usuário que orienta você na instalação, configuração e implantação de suas soluções de rastreamento de mídia baseadas na Web. O Launch melhora com o Dynamic Tag Management (DTM).
* *SDK do Media* - o SDK do Media fornece bibliotecas de rastreamento de mídia criadas para plataformas específicas (por exemplo: Android, iOS, etc.). A Adobe recomenda o SDK do Media para rastrear o uso de mídia em aplicativos móveis.

## Configuração

### SDK do Media independente

No SDK do Media independente, é possível configurar o rastreamento no aplicativo
e transmiti-lo para o SDK ao criar o rastreador.

```javascript
//Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
mediaConfig.trackingServer = "namespace.hb.omtrdc.net";
mediaConfig.playerName = "html5-player";
mediaConfig.channel = "sample-channel";
mediaConfig.ovp = "video-provider";
mediaConfig.appVersion = "v2.0.0"
mediaConfig.ssl = true;
mediaConfig.debugLogging = true;
```

Além da configuração do `MediaHeartbeat`, a página deve configurar e transmitir
a instância `AppMeasurement` e a instância `VisitorAPI` para que o rastreamento de mídia funcione corretamente.

### Extensão do Launch

1. No Experience Platform Launch, clique na guia [!UICONTROL Extensões] para sua
propriedade da Web.
1. Na guia [!UICONTROL Catálogo], localize a extensão Adobe Media Analytics para áudio e
vídeo e clique em [!UICONTROL Instalar].
1. Na página de configurações da extensão, defina os parâmetros de rastreamento. A extensão do Media usa os parâmetros configurados para rastreamento.

   ![](assets/launch_config_js.png)

[Guia do usuário do Launch - Instalar e configurar a extensão de mídia](https://docs.adobe.com/content/help/pt-BR/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html#install-and-configure-the-ma-extension)

## Diferenças na criação do rastreador

### SDK do Media

1. Adicione a biblioteca do Media Analytics ao projeto de desenvolvimento.
1. Criar um objeto de configuração (`MediaHeartbeatConfig`).
1. Implemente o protocolo delegado, expondo as funções `getQoSObject()` e `getCurrentPlaybackTime()`.
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

[SDK do Media - Criação do rastreador](https://docs.adobe.com/content/help/pt-BR/media-analytics/using/sdk-implement/cookbook/sdk-vs-launch-qoe.html)

### Launch

O Launch oferece duas abordagens para a criação da infraestrutura de rastreamento. Ambas as abordagens usam o Media Analytics Launch Extension:

1. Use as APIs de rastreamento de mídia em uma página da Web.

   Nesse cenário, o Media Analytics Launch Extension exporta as APIs de rastreamento de mídia para uma variável configurada no objeto de janela global:

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. Use as APIs de rastreamento de mídia de outra extensão do Launch.

   Nesse cenário, é possível usar as APIs de rastreamento de mídia expostas pelos Módulos compartilhados `get-instance` e `media-heartbeat`.

   >[!NOTE]
   >
   >Os Módulos compartilhados não estão disponíveis para uso nas páginas da Web. É possível usar os Módulos compartilhados somente em outra extensão.

   Crie uma instância `MediaHeartbeat` usando o Módulo compartilhado `get-instance`.
Transmita um objeto delegado para `get-instance` que exponha as funções `getQoSObject()` e `getCurrentPlaybackTime()`.

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   Acesse as constantes `MediaHeartbeat` pelo Módulo compartilhado `media-heartbeat`.

## Documentação relacionada

### SDK do Media

* [Configurar JS](/help/sdk-implement/setup/set-up-js.md)
* [API JS do SDK do Media](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

### Launch

* [Resumo do Launch](https://docs.adobe.com/content/help/pt-BR/launch/using/overview.html)
* [Extensão do Media Analytics](https://docs.adobe.com/content/help/pt-BR/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)
