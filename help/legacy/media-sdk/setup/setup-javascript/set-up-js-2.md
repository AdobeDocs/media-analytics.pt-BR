---
title: Como configurar o SDK de mídia usando o JavaScript 2.x
description: Siga estas etapas para configurar o aplicativo do SDK de mídia no JavaScript 2.x.
uuid: 0269d8ad-0af8-4bf1-9d15-e06c2952a005
exl-id: 33976096-8b86-4353-906b-e25bf4693471
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/mYfKt95xUE59MuMFOzGro6fPsJsdy4wcy2F2J--JaW8
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 408
ht-degree: 89%

---

# Configurar o JavaScript 2.x{#set-up-javascript}

## Pré-requisitos

* **Obter parâmetros de configuração válidos**
Esses parâmetros podem ser obtidos de um representante da Adobe após a configuração da sua conta do Analytics.
* **Implementar o `AppMeasurement` for JavaScript no aplicativo de mídia**
Para obter mais informações sobre a documentação do Adobe Mobile SDK, consulte [Implementação do Analytics usando o JavaScript.](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=pt-BR)

* **Forneça os seguintes recursos no player de mídia:**

   * *Uma API para assinar eventos do player* - O SDK de mídia exige que você chame um conjunto de APIs simples quando eventos ocorrem no player.
   * *Uma API que fornece informações sobre o player* - Essas informações incluem detalhes como o nome da mídia e a posição do indicador de reprodução.

1. Adicione a biblioteca [baixada](/help/getting-started/download-sdks.md) ao projeto. Para conveniência, crie referências locais para as classes.

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

Para obter informações sobre a migração da versão 1.x para a 2.x, consulte a documentação de Implementação herdada.
