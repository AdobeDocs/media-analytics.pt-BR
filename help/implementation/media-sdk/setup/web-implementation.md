---
title: Como configurar uma implementação da Web para o Analytics for Streaming Media
description: Saiba como implementar o Adobe Streaming Media para aplicativos Web.
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 71%

---


# Instalar SDKs da Web {#install-web-sdks}

Configure o SDK do Media v3.x para JavaScript >> o que Calise deseja na página/link de download

Esta seção inclui informações sobre como instalar o SDK da Web e configurar o JavaScript.


## Pré-requisitos  {#prerequesites}

* **Obter parâmetros de configuração válidos**

   Esses parâmetros podem ser obtidos de um representante do Adobe após a configuração da sua conta do Analytics.

* **Implementar `AppMeasurement` e `Experience Cloud Identity Service` para JavaScript no aplicativo de mídia**

   Para obter mais informações, consulte [Implementação do Analytics usando JavaScript](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=pt-BR) e [Implementação do serviço de identidade do Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-analytics.html?lang=pt-BR).

* **Inclua as seguintes APIs no reprodutor de mídia**

   * *Uma API para assinar eventos do player* - O SDK de mídia exige que você chame um conjunto de APIs simples quando eventos ocorrem no player.
   * *Uma API que fornece informações sobre o reprodutor* - Inclui informações sobre mídia, anúncios e capítulos reproduzidos no momento.

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
