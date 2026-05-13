---
title: Migração do Media SDK independente para o Adobe Launch - Web (JS)
description: Saiba como migrar do Media SDK para o Launch para JS.
exl-id: 19b506b2-3070-4a5e-9732-a5cd0867afde
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/N4Fcbg3R9tT9cjUcaw-kcUm6h-QT8TYwatdCe1IdsaM
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: c069c44e-5426-4c1a-accc-8028662f2fde
  - id: df312454-73c4-43f6-a90e-18f5043f074c
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 466
ht-degree: 77%

---

# Migração do Media SDK independente para o Adobe Launch - Web (JS)

>[!NOTE]
>A Adobe Experience Platform Launch está sendo reformulada como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=pt-BR) para obter uma referência consolidada das alterações de terminologia.

## Diferenças nos recursos

* *Launch* - o Launch fornece uma interface do usuário que orienta você na instalação, configuração e implantação de suas soluções de rastreamento de mídia baseadas na Web. O Launch melhora com o Dynamic Tag Management (DTM).
* *SDK do Media* - o SDK do Media fornece bibliotecas de rastreamento de mídia criadas para plataformas específicas (por exemplo: Android, iOS, etc.). A Adobe recomenda o SDK do Media para rastrear o uso de mídia em aplicativos móveis.

## Configuração

### SDK do Media independente

No Media SDK independente, é possível configurar o rastreamento no aplicativo
e transmita-o para a SDK ao criar o rastreador.

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

Além da configuração `MediaHeartbeat`, a página deve configurar e passar
a instância `AppMeasurement` e a instância `VisitorAPI` para rastreamento de mídia em ordem
para funcionarem corretamente.

### Extensão do Launch

1. No Experience Platform Launch, clique na guia [!UICONTROL Extensões] para seu
propriedade da web.
1. Na guia [!UICONTROL Catálogo], localize o Adobe Media Analytics para áudio e
Extensão de vídeo e clique em [!UICONTROL Instalar].
1. Na página de configurações da extensão, defina os parâmetros de rastreamento.
A extensão do Media usa os parâmetros configurados para rastreamento.

   ![](assets/launch_config_js.png)

[Guia do usuário do Launch - Instalar e configurar a extensão de mídia](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=pt-BR#install-and-configure-the-ma-extension)

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

* [Configurar o JavaScript 2.x](/help/legacy/media-sdk/setup/setup-javascript/set-up-js-2.md)
* [API JS do Media SDK](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

### Launch

* [Visão geral do Launch](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR)
* [Extensão do Media Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=pt-BR)
