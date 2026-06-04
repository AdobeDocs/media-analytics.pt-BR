---
title: Configurar o Web SDK para mídia de transmissão
description: Configure o Adobe Experience Platform Web SDK (alloy.js) para enviar dados de streaming de mídia para a Edge Network.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 5%

---

# Configurar o Web SDK para mídia de transmissão

O componente `streamingMedia` do Adobe Experience Platform [Web SDK](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/js-overview) (`alloy.js`, versão 2.20.0 ou posterior) coleta dados da sessão de mídia em seu site e os envia para a Edge Network. Esta página aborda a configuração no código (`alloy.js`). Para configurar o Web SDK por meio de Marcas, consulte [Configurar a extensão de marca do Web SDK para mídia de streaming](web-sdk-tags.md).

* **Pré-requisitos**:
   * Conclua a [visão geral da implementação do Edge](overview.md) (esquema, conjunto de dados, sequência de dados com o [!UICONTROL Media Analytics] habilitado).
   * Instale o Web SDK 2.20.0 ou posterior. Consulte [Instalar o Web SDK](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/install/overview).

## Configurar o componente streamingMedia

Adicionar o componente `streamingMedia` à sua configuração `alloy`:

```js
alloy("configure", {
  edgeConfigId: "<datastreamID>",
  streamingMedia: {
    channel: "sample_channel",
    playerName: "player_name",
    appVersion: "app_version",
    mainPingInterval: 10,
    adPingInterval: 10
  }
});
```

Para obter detalhes completos sobre a configuração, consulte o [`streamingMedia` comando](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/configure/streamingmedia).

### Migração do Media JS SDK

Se você estiver movendo do Media JS (3.x) SDK, o comando [`getMediaAnalyticsTracker`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/getmediaanalyticstracker) do Web SDK retornará uma instância do rastreador que expõe as mesmas APIs que o [3.x Media SDK](/help/implementation/analytics-only/javascript.md), de modo que as chamadas de rastreamento existentes continuem a funcionar.

## Rastrear eventos de mídia

Com o SDK configurado, envie cada evento de mídia chamando [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview). Consulte a guia **Web SDK** em cada página de [evento](/help/implementation/events/overview.md) e [variável](/help/implementation/variables/overview.md) para obter as cargas exatas.

## Próxima etapa

Uma vez concluída a implementação, você pode [Configurar relatórios para implementações do Edge](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Visão geral do SDK da Web](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/js-overview)
>* [Visão geral dos eventos](/help/implementation/events/overview.md)
>* [Visão geral das variáveis](/help/implementation/variables/overview.md)
