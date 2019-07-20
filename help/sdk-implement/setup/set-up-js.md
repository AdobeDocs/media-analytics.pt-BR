---
seo-title: Configurar JavaScript
title: Configurar JavaScript
uuid: 0269 d 8 ad -0 af 8-4 bf 1-9 d 15-e 06 c 2952 a 005
translation-type: tm+mt
source-git-commit: 63fb6332694675cd03843995f8f86ae45973d399

---


# Configurar JavaScript{#set-up-javascript}

## Pré-requisitos

* **Obter parâmetros
de configuração válidos** Esses parâmetros podem ser obtidos a partir de um representante da Adobe depois que você configurar sua conta de análise.
* **Implementação`AppMeasurement`do javascript no aplicativo
de mídia** Para obter mais informações sobre a documentação do SDK do Adobe Mobile, consulte [Implementação do Analytics usando javascript.](https://marketing.adobe.com/resources/help/en_US/sc/implement/js_implementation.html)

* **Forneça os seguintes recursos no reprodutor de mídia:**

   * *Uma API para assinar os eventos do reprodutor* - O SDK do Media exige a chamada de um conjunto de APIs simples quando ocorrerem eventos no reprodutor.
   * *Uma API que fornece informações sobre o reprodutor* - Essas informações incluem detalhes como o nome da mídia e a posição do indicador de reprodução.

1. Adicione a biblioteca [baixada](../../sdk-implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211) ao projeto. Para conveniência, crie referências locais para as classes.

   1. Expand the `MediaSDK-js-v2.*.zip` file that you downloaded.
   1. Verify that the `MediaSDK.min.js` file exists in the `libs` directory:

   1. Host the `MediaSDK.min.js` file.

      Esse arquivo JavaScript principais deve ser hospedado em um servidor Web acessível para todas as páginas em seu site. Você precisará do caminho para esses arquivos na próxima etapa.

   1. Referencie `MediaSDK.min.js` em todas as páginas do site.

      Include `MediaSDK` for JavaScript by adding the following line of code in the `<head>` or `<body>` tag on each page. Por exemplo:

      ```
      <script type="text/javascript" 
      src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.min.js"></script>
      ```

   1. Para verificar rapidamente se a biblioteca do foi importada com sucesso, exemplifique a classe `ADB.va.MediaHeartbeatConfig`.

      >[!NOTE]
      >
      >From Version 2.1.0, the JavaScript SDK is compliant with the AMD and CommonJS module specifications, and `VideoHeartbeat.min.js` can also be used with compatible module loaders.

1. Para obter acesso fácil às APIs, crie uma referência local para as classes `MediaHeartbeat`. 

   ```js
   var MediaHeartbeat = ADB.va.MediaHeartbeat; 
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig; 
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate; 
   ```

1. Create a `MediaHeartbeatConfig` instance.

   Essa seção ajuda você a entender os parâmetros de configuração do `MediaHeartbeat` e definir corretamente os valores de configuração na sua instância `MediaHeartbeat`, de modo a permitir um rastreamento preciso.

   Aqui está uma amostra de inicialização `MediaHeartbeatConfig`:

   ```js
   //Media Heartbeat initialization 
   var mediaConfig = new MediaHeartbeatConfig(); 
   mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER; 
   mediaConfig.playerName = Configuration.PLAYER.NAME; 
   mediaConfig.channel = Configuration.HEARTBEAT.CHANNEL; 
   mediaConfig.debugLogging = true; 
   mediaConfig.appVersion = Configuration.HEARTBEAT.SDK; 
   mediaConfig.ssl = false; 
   mediaConfig.ovp = Configuration.HEARTBEAT.OVP; 
   ```

1. Implement the `MediaHeartbeatDelegate` protocol.

   ```js
   var mediaDelegate = new MediaHeartbeatDelegate(); 
   
   // Replace <currentPlaybackTime> with the video player current playback time 
   mediaDelegate.getCurrentPlaybackTime = function() { 
       return <currentPlaybackTime>; 
   }; 
   
   // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames> with the current playback QoS values.  
   mediaDelegate.getQoSObject = function() { 
       return MediaHeartbeat.createQoSObject(<bitrate>, <startuptime>, <fps>, <droppedFrames>); 
   };
   ```

1. Create the `MediaHeartbeat` instance.

   Use the `MediaHeartbeatConfig` and `MediaHeartbeatDelegate` to create the `MediaHeartbeat` instance.

   ```js
   this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
   ```

   >[!IMPORTANT]
   >
   >Make sure that your `MediaHeartbeat` instance is accessible and does not get deallocated until the end of the media session. Essa instância será usada para todos os eventos de rastreamento a seguir.

   >[!TIP]
   >
   >`MediaHeartbeat` requer uma instância de `AppMeasurement` envio de chamadas para o Adobe Analytics. A seguir, há um exemplo de uma instância `AppMeasurement`:

   ```js
   var appMeasurement = new AppMeasurement(); 
   appMeasurement.visitor = visitor; 
   appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net"; 
   appMeasurement.account = <rsid>; 
   appMeasurement.pageName = <page_name>; 
   appMeasurement.charSet = "UTF­8";
   ```

## Migração da versão 1.x para 2.x do JavaScript

Na versão 2.x, todos os métodos públicos foram consolidados na classe `ADB.va.MediaHeartbeat` para facilitar o trabalho dos desenvolvedores. Além disso, todas as configurações foram consolidadas na classe `ADB.va.MediaHeartbeatConfig`

Para obter informações detalhadas sobre a migração de 1.x para 2.x, consulte [Migração do VHL 1.x para 2.x.](../../sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
