---
title: Configurar o JavaScript para mídia de transmissão
description: Instale e configure o Media SDK for JavaScript (3.x) para implementações de mídia de transmissão exclusivas do Analytics.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 3%

---

# Configurar o JavaScript para mídia de transmissão

O Media SDK for JavaScript (3.x) envia dados de mídia de transmissão diretamente para a Adobe Analytics. Esta página aborda a instalação manual do JavaScript. Para implantar a SDK por meio de Marcas, consulte [Configurar a extensão de marca do Media Analytics](javascript-tags.md). Para novas implementações, considere usar o [Web SDK](/help/implementation/edge/web-sdk.md) para enviar dados à Adobe Analytics por meio de uma sequência de dados do Edge Network.

* **Pré-requisitos**:
   * Conclua a [visão geral da implementação somente do Analytics](overview.md).
   * Implemente o [AppMeasurement](https://experienceleague.adobe.com/pt-br/docs/analytics/implementation/js/overview) e o [Serviço de ID de Visitante](https://experienceleague.adobe.com/en/docs/analytics/implementation/id/appmeasurement).
   * [Baixe o Media SDK para JavaScript](/help/getting-started/download-sdks.md).

## Instalar e configurar o SDK

1. Hospede `MediaSDK.js` (do diretório `libs` baixado) em um servidor Web acessível a todas as páginas e referencie-o em cada página:

   ```html
   <script type="text/javascript" src="https://INSERT-DOMAIN-AND-PATH/MediaSDK.js"></script>
   ```

1. Configure o Media SDK uma vez por página, transmitindo a instância `appMeasurement` que você configurou como pré-requisito:

   ```js
   var mediaConfig = new ADB.MediaConfig();
   mediaConfig.trackingServer = "<media_collection_server>";
   mediaConfig.playerName = "player_name";
   mediaConfig.channel = "sample_channel";
   mediaConfig.appVersion = "app_version";
   mediaConfig.ssl = true;
   
   ADB.Media.configure(mediaConfig, appMeasurement);
   ```

   >[!NOTE]
   >
   >A variável `mediaConfig.trackingServer` é seu **servidor de coleção de mídia** (por exemplo, `[namespace].hb-api.omtrdc.net`). Esse servidor de coleção é diferente do servidor de rastreamento do Analytics configurado na instância do AppMeasurement.

1. Crie uma instância do rastreador com `getInstance`. Mantenha a instância acessível para toda a sessão de mídia:

   ```js
   var tracker = ADB.Media.getInstance();
   ```

## Rastrear eventos de mídia

Com o rastreador criado, rastreie cada evento de mídia usando seu método de rastreador. Consulte a guia **Media SDK JS 3.x** em cada página de [evento](/help/implementation/events/overview.md) e [variável](/help/implementation/variables/overview.md) para obter as chamadas exatas.

## Próxima etapa

Uma vez concluída a implementação, você pode [Configurar relatórios para implementações somente do Analytics](/help/reporting/setup/analytics-reporting.md).

>[!MORELIKETHIS]
>
>* [Referência de API do Media SDK para JavaScript 3.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/sdks/js/3.x/docs/APIReference.md)
>* [Migrar do JS SDK 2.x para o 3.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/sdks/js/3.x/docs/MigrationGuide.md)
>* [Configurar a extensão de tag do Media Analytics](javascript-tags.md)
>* [Visão geral dos eventos](/help/implementation/events/overview.md)
