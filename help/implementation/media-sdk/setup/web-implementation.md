---
title: Como configurar uma implementação da Web para o Analytics para mídia de streaming
description: Saiba como implementar a mídia de streaming da Adobe para aplicativos web.
feature: Streaming Media
role: User, Admin, Developer
exl-id: aed561d0-defc-4be5-87d3-0f331cdfab34
TQID: https://experienceleague.adobe.com/UBY26SeGZbGWHjwOm6-YZNET8fe5Gvvco7aIZ9Z7rZg
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: df312454-73c4-43f6-a90e-18f5043f074c
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 472
ht-degree: 93%

---

# Instale o Media SDK usando o JavaScript {#install-web-sdks}

As informações nesta página descrevem como instalar o SDK independente da Web e configurar o JavaScript.

Como alternativa, você pode usar a extensão do Adobe Media Analytics para implementar serviços de mídia de streaming, conforme descrito em [Instalar serviços de mídia de streaming usando a extensão do Media Analytics](/help/implementation/media-sdk/setup/web-implementation-tags.md).

## Pré-requisitos {#prerequesites}

* **Obter parâmetros de configuração válidos**

  Esses parâmetros podem ser obtidos com um representante da Adobe após a configuração da conta do Analytics.

* **Implementar o `AppMeasurement` e `Experience Cloud Identity Service` para JavaScript no aplicativo de mídia**

  Para obter mais informações, consulte [Implementação do Analytics usando JavaScript](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=pt-BR) e [Implementação do serviço de identidade da Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-analytics.html?lang=pt-BR).

* **Inclua as seguintes APIs em seu reprodutor de mídia**

   * *Uma API para assinar eventos do player* - O SDK de mídia exige que você chame um conjunto de APIs simples quando eventos ocorrem no player.
   * *Uma API que fornece informações sobre o player* - Inclui informações sobre anúncios, capítulos e mídias que estão sendo reproduzidas no momento.

## Configurar o JavaScript 3.x {#set-up-javascript}

1. Adicione a biblioteca [baixada](/help/getting-started/download-sdks.md) ao projeto. Para conveniência, crie referências locais para as classes.

   1. Expanda o arquivo `MediaSDK-js-v3*.zip` que você baixou.
   1. Verifique se o arquivo `MediaSDK.js` existe no diretório `libs`.

   1. Hospede o arquivo `MediaSDK.js`.

      Esse arquivo JavaScript principal deve ser hospedado em um servidor da Web acessível a todas as páginas do site. Você precisa do caminho para esses arquivos para a próxima etapa.

   1. Referencie `MediaSDK.js` em todas as páginas do site.

      Inclua `MediaSDK` para o JavaScript ao adicionar a seguinte linha de código na tag `<head>` ou `<body>` em cada página. Por exemplo:

      ```html
      <script type="text/javascript" src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.js"></script>
      ```

   1. Para verificar rapidamente se a biblioteca foi importada, verifique se `ADB.Media` foi exportado no objeto Window.

      >[!NOTE]
      >
      >O SDK do JavaScript é compatível com as especificações dos módulos AMD e CommonJS, e o `MediaSDK.js` também pode ser usado com carregadores de módulo compatíveis.

1. Crie uma instância de `AppMeasurement` e configure o `visitor`.

   A configuração do Media SDK requer uma instância de `AppMeasurement` com o `visitor` configurado.

   ```js
    var appMeasurement = new AppMeasurement("<rsid>");
    appMeasurement.visitor = visitor;
    appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net";
   ```

1. Configurar o Media SDK

   O Media SDK deve ser configurado uma vez por página da Web e a configuração se aplica a todas as instâncias do rastreador criadas.

   >[!IMPORTANT]
   >
   > O Media SDK (3.x) usa a API Media Collection para rastrear mídia diferente do ponto de extremidade HB usado nos SDKs 2.x. Entre em contato com seu representante da Adobe para obter mais informações.

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

   Depois de configurar o Media SDK, as instâncias do rastreador para rastrear conteúdo de mídia podem ser criadas usando a API `getInstance`.

   ```js
   var tracker = ADB.Media.getInstance();
   ```

   >[!IMPORTANT]
   >
   >Certifique-se de que a instância do `tracker` possa ser acessada e não seja desalocada até o final da sessão de mídia. Essa instância será usada para rastrear todos os eventos a seguir para essa sessão.

## Migrar do JavaScript 2.x para o 3.x

Para obter informações detalhadas sobre a migração de 2.x para 3.x, consulte [Migração do 2.x para 3.x.](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/MigrationGuide.html)

Para conteúdo herdado, consulte [Implementações herdadas](/help/legacy/media-sdk/setup/setup-overview.md)
