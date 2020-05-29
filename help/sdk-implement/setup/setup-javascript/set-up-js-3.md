---
title: Configurar o JavaScript 3.x
description: Configuração do aplicativo SDK de mídia para implementação no JavaScript 3.x.
translation-type: tm+mt
source-git-commit: b642bd1a136e62901847f2a8cf004d05282fca01
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 47%

---


# Configurar o JavaScript 3.x{#set-up-javascript}

## Pré-requisitos

* **Obter parâmetros de configuração válidos**
Esses parâmetros podem ser obtidos de um representante da Adobe após a configuração da sua conta do Analytics.
* **Implementação`AppMeasurement`e`Experience Cloud Identity Service`para JavaScript no aplicativo** de mídia. Para obter mais informações, consulte [Implementação do Analytics usando JavaScript](https://docs.adobe.com/content/help/pt-BR/analytics/implementation/js/overview.html) e [Implementação do Serviço de identidade da Experience Cloud.](https://docs.adobe.com/content/help/en/id-service/using/implementation/setup-analytics.html)

* **Forneça os seguintes recursos no player de mídia:**

   * *Uma API para assinar eventos do player* - O SDK de mídia exige que você chame um conjunto de APIs simples quando eventos ocorrem no player.
   * *Uma API que fornece informações* sobre o player - isso inclui informações sobre mídia, anúncios e capítulos reproduzidos no momento.

1. Adicione a biblioteca [baixada](/help/sdk-implement/download-sdks.md#download-3x-sdks) ao projeto. Para conveniência, crie referências locais para as classes.

   1. Expanda o arquivo `MediaSDK-js-v3*.zip` que você baixou.
   1. Verifique se o arquivo `MediaSDK.js` existe no diretório `libs`.

   1. Hospede o arquivo `MediaSDK.js`.

      Esse arquivo JavaScript principal deve ser hospedado em um servidor da Web acessível a todas as páginas do site. Você precisa do caminho para esses arquivos para a próxima etapa.

   1. Referencie `MediaSDK.js` em todas as páginas do site.

      Inclua `MediaSDK` para o JavaScript ao adicionar a seguinte linha de código na tag `<head>` ou `<body>` em cada página. Por exemplo:

      ```html
      <script type="text/javascript" src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.js"></script>
      ```

   1. Para verificar rapidamente se a biblioteca foi importada com êxito, verifique se `ADB.Media` é exportada no objeto Window.

      >[!NOTE]
      >
      >The JavaScript SDK is compliant with the AMD and CommonJS module specifications, and `MediaSDK.js` can also be used with compatible module loaders.

1. Crie uma instância de `AppMeasurement` e configure `visitor`.

   A configuração do SDK de mídia requer uma instância de `AppMeasurement` com `visitor` configurado.

   ```js
    var appMeasurement = new AppMeasurement(“<rsid>”);
    appMeasurement.visitor = visitor;
    appMeasurement.trackingServer = “<visitor_namespace>.sc.omtrdc.net”;
   ```

1. Configurar o SDK de mídia

   O SDK de mídia deve ser configurado uma vez por página da Web e a configuração se aplica a todas as instâncias do rastreador criadas.

   >[!IMPORTANT]
   >
   > O SDK de mídia (3.x) usa a API Media Collection para rastrear mídia diferente do ponto de extremidade HB usado nos SDKs 2.x. Entre em contato com seu representante da Adobe para obter mais informações.

   Aqui está uma amostra de inicialização `MediaConfig`:

   ```js
    // Create MediaConfig object (same as above)
    var mediaConfig = new ADB.MediaConfig();
    mediaConfig.trackingServer = Configuration.MEDIA_COLLECTION_ENDPOINT;
    mediaConfig.playerName = Configuration.PLAYER_NAME;
    mediaConfig.channel = Configuration.CHANNEL;
    mediaConfig.appVersion = Configuration.APP_VERSION;
    mediaConfig.debugLogging = false;
    mediaConfig.ssl = true;
   
    ADB.Media.configure(mediaConfig, appMeasurement);
   ```

1. Crie a instância `MediaTracker`.

   Depois de configurar o SDK de mídia, as instâncias do rastreador para rastrear conteúdo de mídia podem ser criadas usando a `getInstance` API.

   ```js
   var tracker = ADB.Media.getInstance();
   ```

   >[!IMPORTANT]
   >
   >Certifique-se de que a instância do `tracker` possa ser acessada e não seja desalocada até o final da sessão de mídia. Essa instância será usada para rastrear todos os eventos a seguir para essa sessão.

## Migrar do JavaScript 2.x para o 3.x

Para obter informações detalhadas sobre a migração de 2.x para 3.x, consulte [Migração do 2.x para 3.x.](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/MigrationGuide.html)
