---
seo-title: Migração do SDK de mídia independente para o Adobe Launch - Web (JS)
title: Migração do SDK de mídia independente para o Adobe Launch - Web (JS)
seo-description: Instruções e exemplos de código para auxiliar na migração do SDK de mídia para o Launch.
description: Instruções e exemplos de código para auxiliar na migração do SDK de mídia para o Launch.
translation-type: tm+mt
source-git-commit: b479f6623566b6a6989f625b757a97bba5f6aafd

---


# Migração do SDK de mídia independente para o Adobe Launch - Web (JS)

## Diferenças de recursos

* *Launch* - o Launch fornece uma interface que orienta você na configuração, configuração e implantação das soluções de rastreamento de mídia baseadas na Web. O Launch melhora o Gerenciamento dinâmico de tags (DTM).
* *SDK* de mídia - o SDK de mídia fornece bibliotecas de rastreamento de mídia projetadas para plataformas específicas (por exemplo: Android, iOS, etc.). A Adobe recomenda o SDK de mídia para rastrear o uso de mídia em seus aplicativos móveis.

## Configuração

### Iniciar Extensão

1. Em Experience Platform Launch, clique na guia [!UICONTROL Extensões] para sua propriedade da Web.
1. Na guia [!UICONTROL Catálogo] , localize a extensão Adobe Media Analytics para áudio e vídeo e clique em [!UICONTROL Instalar].
1. Na página de configurações de extensão, defina os parâmetros de rastreamento.
A extensão de mídia usará os parâmetros configurados para rastreamento.

[Iniciar o Guia do Usuário - Instalar e configurar a extensão de mídia](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html#install-and-configure-the-ma-extension)

### SDK de mídia independente

No SDK de mídia independente, configure a configuração de rastreamento no aplicativo e passe-a para o SDK ao criar o rastreador.

```javascript
//Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
mediaConfig.trackingServer = "namespace.hb.omtrdc.net";
mediaConfig.playerName = "html5-player";
mediaConfig.channel = "sample-channe";
mediaConfig.ovp = "video-provider";
mediaConfig.appVersion = "v2.0.0"
mediaConfig.ssl = true;
mediaConfig.debugLogging = true;
```

Além da `MediaHeartbeat` configuração, a página deve configurar e passar a instância e a `AppMeasurement` `VisitorAPI` instância para que o rastreamento de mídia funcione corretamente.

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
   >Módulos compartilhados não estão disponíveis para uso em páginas da Web. Você só pode usar Módulos compartilhados de outra extensão.

   Crie uma `MediaHeartbeat` instância usando o Módulo `get-instance` compartilhado.
Passe um objeto delegado para `get-instance` que exponha `getQoSObject()` e `getCurrentPlaybackTime()` funcione.

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   Acessar `MediaHeartbeat` constantes pelo Módulo `media-heartbeat` compartilhado.

### SDK do Media

1. Adicione a biblioteca do Media Analytics ao seu projeto de desenvolvimento.
1. Criar um objeto de configuração (`MediaHeartbeatConfig`).
1. Implemente o protocolo delegado, expondo as funções `getQoSObject()` e `getCurrentPlaybackTime()` .
1. Crie uma instância Media Heartbeat (`MediaHeartbeat`).

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

[SDK de mídia - Criação do rastreador](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/cookbook/sdk-vs-launch-qoe.html)

## Documentação relacionada

### Launch

* [Visão geral do lançamento](https://docs.adobe.com/content/help/en/launch/using/overview.html)
* [Extensão do Media Analytics](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)

### SDK do Media

* [Configurar JS](/help/sdk-implement/setup/set-up-js.md)
* [API JS do SDK de mídia](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

