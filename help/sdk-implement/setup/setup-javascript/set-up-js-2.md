---
title: Configurar o JavaScript 2.x
description: Configuração do aplicativo SDK do Media para implementação no JavaScript 2.
uuid: 0269d8ad-0af8-4bf1-9d15-e06c2952a005
translation-type: ht
source-git-commit: a73536bd7a818ac23ad322a15f109644e75ee0d5
workflow-type: ht
source-wordcount: '394'
ht-degree: 100%

---


# Configurar o JavaScript 2.x{#set-up-javascript}

## Pré-requisitos

* **Obter parâmetros de configuração válidos**
Esses parâmetros podem ser obtidos de um representante da Adobe após a configuração da sua conta do Analytics.
* **Implementar`AppMeasurement`para JavaScript no aplicativo de mídia**
Para obter mais informações sobre a documentação do SDK do Adobe Mobile, consulte [Implementar o Analytics usando JavaScript.](https://docs.adobe.com/content/help/pt-BR/analytics/implementation/js/overview.html)

* **Forneça os seguintes recursos no player de mídia:**

   * *Uma API para assinar eventos do player* - O SDK de mídia exige que você chame um conjunto de APIs simples quando eventos ocorrem no player.
   * *Uma API que fornece informações sobre o player* - Essas informações incluem detalhes como o nome da mídia e a posição do indicador de reprodução.

1. Adicione a biblioteca [baixada](/help/sdk-implement/download-sdks.md#download-2x-sdks) ao projeto. Para conveniência, crie referências locais para as classes.

   1. Expanda o arquivo `MediaSDK-js-v2.*.zip` que você baixou.
   1. Verifique se o arquivo `MediaSDK.min.js` existe no diretório `libs`:

   1. Hospede o arquivo `MediaSDK.min.js`.

      Esse arquivo JavaScript principal deve ser hospedado em um servidor da Web acessível a todas as páginas do site. Você precisa do caminho para esses arquivos para a próxima etapa.

   1. Referencie `MediaSDK.min.js` em todas as páginas do site.

      Inclua `MediaSDK` para o JavaScript ao adicionar a seguinte linha de código na tag `<head>` ou `<body>` em cada página. Por exemplo:

      ```
      <script type="text/javascript"
      src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.min.js"></script>
      ```

   1. Para verificar rapidamente se a biblioteca do foi importada com sucesso, exemplifique a classe `ADB.va.MediaHeartbeatConfig`.

      >[!NOTE]
      >
      >A partir da versão 2.1.0, o SDK do JavaScript é compatível com as especificações dos módulos AMD e CommonJS e `VideoHeartbeat.min.js` também pode ser usado com carregadores de módulo compatíveis.

1. Para obter acesso fácil às APIs, crie uma referência local para as classes `MediaHeartbeat`.

   ```js
   var MediaHeartbeat = ADB.va.MediaHeartbeat;
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig;
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate;
   ```

1. Crie uma instância `MediaHeartbeatConfig`.

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

1. Implemente o protocolo `MediaHeartbeatDelegate`.

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

1. Crie a instância `MediaHeartbeat`.

   Use `MediaHeartbeatConfig` e `MediaHeartbeatDelegate` para criar a instância `MediaHeartbeat`.

   ```js
   this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
   ```

   >[!IMPORTANT]
   >
   >Certifique-se de que a instância do `MediaHeartbeat` possa ser acessada e não seja desalocada até o final da sessão de mídia. Essa instância será usada para todos os eventos de rastreamento a seguir.

   >[!TIP]
   >
   >`MediaHeartbeat` exige uma instância do `AppMeasurement` para enviar chamadas para o Adobe Analytics. A seguir, há um exemplo de uma instância `AppMeasurement`:

   ```js
   var appMeasurement = new AppMeasurement();
   appMeasurement.visitor = visitor;
   appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net";
   appMeasurement.account = <rsid>;
   appMeasurement.pageName = <page_name>;
   appMeasurement.charSet = "UTF­8";
   ```

## Migrar do JavaScript 1.x para o 2.x

Na versão 2.x, todos os métodos públicos foram consolidados na classe `ADB.va.MediaHeartbeat` para facilitar o trabalho dos desenvolvedores. Além disso, todas as configurações foram consolidadas na classe `ADB.va.MediaHeartbeatConfig`

Para obter informações detalhadas sobre a migração de 1.x para 2.x, consulte [Migração do VHL 1.x para 2.x.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
