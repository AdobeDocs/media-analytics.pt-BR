---
title: Configurar a extensão de tag do Web SDK para mídia de transmissão
description: Configure a coleção de mídia de transmissão na extensão de tag da Adobe Experience Platform Web SDK.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Configurar a extensão de tag do Web SDK para mídia de transmissão

A extensão de tag do Adobe Experience Platform Web SDK permite configurar a coleção de mídia de transmissão na interface da Coleção de dados, sem código de configuração `alloy.js`. Esta página aborda a configuração de Tags. Para configurar o Web SDK em código, consulte [Configurar o Web SDK para mídia de streaming](web-sdk.md).

* **Pré-requisitos**:
   * Conclua a [visão geral da implementação do Edge](overview.md) (esquema, conjunto de dados, sequência de dados com o [!UICONTROL Media Analytics] habilitado).
   * Instale e configure a extensão de tag do Web SDK. Consulte a [visão geral da extensão de marca do Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/web-sdk/overview).

## Configurar mídia de transmissão na extensão

1. Na interface da Coleção de dados, abra a propriedade da Web e selecione **[!UICONTROL Extensões]**.
1. Na extensão **Adobe Experience Platform Web SDK** instalada, selecione **[!UICONTROL Configurar]**.
1. Expanda a seção **[!UICONTROL Mídia de Streaming]** e defina o seguinte:
   * **[!UICONTROL Canal]**: o nome do canal relatado com cada sessão.
   * **[!UICONTROL Nome do reprodutor]**: o nome do reprodutor de mídia em uso.
   * **[!UICONTROL Versão do aplicativo]**: a versão do seu aplicativo de reprodução.
   * **[!UICONTROL Intervalo de ping principal]** e **[!UICONTROL Intervalo de ping do anúncio]**: a cadência de ping (em segundos) do conteúdo principal e dos anúncios.
1. Salve a configuração da extensão e publique as alterações.

## Rastrear eventos de mídia

Com a extensão configurada, envie cada evento de mídia com a ação **[!UICONTROL Enviar Evento]** (ou o comando `sendEvent`). Consulte a guia **Web SDK** em cada página de [evento](/help/implementation/events/overview.md) e [variável](/help/implementation/variables/overview.md) para obter as cargas exatas.

## Próxima etapa

Uma vez concluída a implementação, você pode [Configurar relatórios para implementações do Edge](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [visão geral da extensão de marca do Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/web-sdk/overview)
>* [Configurar o Web SDK para mídia de streaming (no código)](web-sdk.md)
>* [Visão geral dos eventos](/help/implementation/events/overview.md)
