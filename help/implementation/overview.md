---
title: Implementar mídia de transmissão para Adobe Analytics ou Customer Journey Analytics
description: Saiba mais sobre os caminhos de implementação da mídia de transmissão.
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: ed9297b1-6487-4099-bc62-0c3a40572255
source-git-commit: a26e4e283646e5ceb352f357789748f376f5c747
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 13%

---

# Implementar mídia de transmissão no Adobe Analytics ou Customer Journey Analytics

Há várias maneiras de implementar a mídia de transmissão. Para obter uma comparação detalhada dos dispositivos e plataformas compatíveis com os métodos de implementação descritos nesta página, consulte [Dispositivos e plataformas compatíveis](/help/getting-started/supported-devices.md).

## Métodos de implementação do Edge

Recomendamos o uso do Edge ao implementar o Media Analytics para todos os novos clientes do Adobe Analytics ou Customer Journey Analytics.

* **Mídia para SDK/Extensão de Rede de Borda:** Coleta dados de dispositivos iOS e Android e os envia para o Edge. Os dados podem ser enviados para o Customer Journey Analytics ou Adobe Analytics.

  Para obter mais informações sobre o SDK/Extensão do Media for Edge Network, consulte [Instale o Media Analytics com Experience Platform Edge](/help/implementation/edge/implementation-edge.md).

  >[!NOTE]
  >
  >No momento, esse método de implementação não é compatível com o SDK da Web ou Roku. No entanto, ambos são compatíveis ao implementar com a API Media Edge.

* **API Media Edge:** Pode ser personalizado para coletar dados de qualquer dispositivo ou formato (incluindo dispositivos móveis, da Web e dispositivos OTT) e enviar dados para o Edge. Os dados podem ser enviados para o Customer Journey Analytics ou Adobe Analytics.

  <!-- For more information about the Media Edge API, see (link to John's docs when they're ready) -->

![Fluxo de trabalho do CJA](assets/cja-implementation.png)

## Métodos de implementação somente do Adobe Analytics

Os métodos de implementação Edge descritos acima são recomendados para Customer Journey Analytics e Adobe Analytics, especialmente para novas implementações.

Além dos métodos de implementação do Edge, outros métodos de implementação estão disponíveis. Esses métodos de implementação foram projetados para serem usados com o Adobe Analytics. No entanto, os clientes existentes com qualquer um dos métodos de implementação a seguir ainda podem disponibilizar dados no Customer Journey Analytics criando uma [Conexão de origem do Analytics](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/adobe-applications/analytics.html?lang=pt-BR).

* **Extensão de mídia com tags:** A extensão do Adobe Medium Analytics para áudio e vídeo fornece a funcionalidade para adicionar a instância do Media Tracker a um site ou projeto habilitado para tags. Os dados são enviados para o Adobe Analytics.

  Para obter informações sobre como instalar, configurar e implementar a Extensão de mídia com tags, consulte [Visão geral da extensão do Adobe Medium Analytics (SDK 3.x) para áudio e vídeo](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/media-analytics-3x/overview.html).

* **SDK de mídia:**  Os dados são enviados para o Adobe Analytics.

  Para obter informações sobre como baixar e instalar SDKs e extensões de mídia, consulte [Obter SDKs de mídia, extensões usando tags e SDKs OTT](/help/getting-started/download-sdks.md).

* **API da coleção de mídia:** Rastreie eventos de áudio e vídeo usando chamadas RESTful HTTP. Os dados são enviados para o Adobe Analytics.

  Para obter informações sobre como usar as APIs da coleção de mídia, consulte [APIs da coleção de mídia](media-collection-api/mc-api-overview.md).


![Workflow do Analytics](assets/analytics-implementation.png)

<!--
(Not sure if we need the following paragraph and graphic. Paragraph is somewhat redundant with the intro paragraph of this article)
Choose the implementation method depending on the supported platforms. Some players are not supported by the Media SDKs or the Adobe Experience Platform Media Extensions. The Media Collection APIs provide a way to support those players. For information on supported devices, see [Supported devices and platforms](/help/getting-started/supported-devices.md).

![Media Flow](media-sdk/assets/choose-media-flow2.png)
-->
