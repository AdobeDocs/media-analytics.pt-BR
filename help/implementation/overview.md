---
title: Implementar o complemento Coleção de mídia de transmissão
description: Saiba mais sobre os caminhos de implementação para o complemento Coleção de mídia de streaming.
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: ed9297b1-6487-4099-bc62-0c3a40572255
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 69%

---

# Implementar o complemento Coleção de mídia de transmissão

Há várias maneiras de implementar o complemento Adobe Streaming Media Collection. Para obter uma comparação detalhada dos dispositivos e plataformas compatíveis com os métodos de implementação descritos nesta página, consulte [Dispositivos e plataformas compatíveis](/help/getting-started/supported-devices.md).

## Métodos de implementação do Edge

Recomendamos usar o Edge ao implementar o Complemento de coleção de mídia de transmissão para todos os novos clientes do Adobe Analytics ou Customer Journey Analytics.

* **Mídia para SDK do Edge Network / Extensão:** Coleta dados da Web, de dispositivos iOS e Android ou de dispositivos Roku e os envia para o Edge Network. Os dados poderão então ser enviados para o Customer Journey Analytics ou Adobe Analytics.

  Para obter mais informações sobre o Media for Edge Network SDK / Extension, consulte [Implementar o complemento de coleção de mídia de streaming usando o Edge Network](/help/implementation/edge/implementation-edge.md).

* **API do Media Edge:** Pode ser personalizado para coletar dados de qualquer dispositivo ou formato (incluindo dispositivos móveis, da Web e over-the-top) e enviar dados para o Edge Network. Os dados poderão então ser enviados para o Customer Journey Analytics ou Adobe Analytics.

  Para obter mais informações sobre a API do Media Edge, consulte [Visão geral da API do Media Edge](https://developer.adobe.com/cja-apis/docs/endpoints/media-edge/).

![Fluxo de trabalho do CJA](assets/streaming-media-edge.png)

## Métodos de implementação somente do Adobe Analytics

Os métodos de implementação do Edge descritos acima são recomendados para Customer Journey Analytics e Adobe Analytics, especialmente para novas implementações.

Além dos métodos de implementação do Edge, outros métodos de implementação estão disponíveis. Esses métodos de implementação foram projetados para uso com o Adobe Analytics. No entanto, clientes com qualquer um dos métodos de implementação a seguir ainda podem disponibilizar dados no Customer Journey Analytics, criando uma [Conexão de origem do Analytics](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/adobe-applications/analytics.html?lang=pt-BR).

* **Extensão de mídia com tags:** a extensão do Adobe Media Analytics para áudio e vídeo fornece a funcionalidade para adicionar a instância do rastreador de mídia a sites ou projetos que tenham tags habilitadas. Os dados são enviados para o Adobe Analytics.

  Para obter informações sobre como instalar, configurar e implementar a Extensão de mídia com tags, consulte [Visão geral da extensão Adobe Media Analytics (SDK 3.x) para áudio e vídeo](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/media-analytics-3x/overview.html?lang=pt-BR).

* **SDK de mídia:** o SDK de mídia permite medir várias plataformas de mídia, incluindo sites, celulares, TVs conectadas, tablets, dispositivos OTT, decodificadores de sinais e consoles de jogos. (Para obter mais informações, consulte [Dispositivos e plataformas compatíveis](/help/getting-started/supported-devices.md)).

  Os SDKs de Mídia usam as APIs de coleção de mídia para rastreamento. Os dados são enviados para o Adobe Analytics.

  Para obter informações sobre como baixar e instalar SDKs e extensões de mídia, consulte [Obter SDKs de mídia, extensões usando tags e SDKs OTT](/help/getting-started/download-sdks.md).

* **APIs de coleção de mídia:** como as APIs de Coleção de mídia são personalizáveis, elas podem ser usadas para aplicativos que exigem recursos de rastreamento personalizados e para dispositivos não compatíveis com os SDKs de mídia. As APIs de coleção de mídia rastreiam eventos de áudio e vídeo usando chamadas RESTful HTTP. Os dados são enviados para o Adobe Analytics.

  Para obter informações sobre como usar as APIs da coleção de mídia, consulte [APIs da coleção de mídia](media-collection-api/mc-api-overview.md).


![Fluxo de trabalho do Analytics](assets/analytics-implementation.png)

<!--
(Not sure if we need the following paragraph and graphic. Paragraph is somewhat redundant with the intro paragraph of this article)
Choose the implementation method depending on the supported platforms. Some players are not supported by the Media SDKs or the Adobe Experience Platform Media Extensions. The Media Collection APIs provide a way to support those players. For information on supported devices, see [Supported devices and platforms](/help/getting-started/supported-devices.md).

![Media Flow](media-sdk/assets/choose-media-flow2.png)
-->
