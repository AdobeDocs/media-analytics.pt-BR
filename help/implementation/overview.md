---
title: Implementar serviços de mídia de transmissão para Adobe Analytics ou Customer Journey Analytics
description: Saiba mais sobre os caminhos de implementação para os serviços de streaming de mídia do Adobe.
uuid: null
feature: Streaming Media
role: User, Admin, Developer
exl-id: ed9297b1-6487-4099-bc62-0c3a40572255
TQID: https://experienceleague.adobe.com/aFrxbzBLlf1ngetaM-GsNFXz6TUXi6Pic3quLVI297c
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: c8add8f2-4250-4fd9-9cde-9707036c567d
  - id: df312454-73c4-43f6-a90e-18f5043f074c
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 522
ht-degree: 65%

---

# Implementar serviços de mídia de transmissão para Adobe Analytics ou Customer Journey Analytics

Há várias maneiras de implementar os serviços de streaming de mídia da Adobe. Para obter uma comparação detalhada dos dispositivos e plataformas compatíveis com os métodos de implementação descritos nesta página, consulte [Dispositivos e plataformas compatíveis](/help/getting-started/supported-devices.md).

## Métodos de implementação do Edge

Recomendamos usar o Edge ao implementar serviços de mídia de transmissão para todos os novos clientes da Adobe Analytics ou da Customer Journey Analytics.

Os métodos de implementação do Edge usam o complemento Coleção de mídia de streaming.

* **Media para Edge Network SDK / Extension:** Coleta dados de dispositivos da Web, iOS e Android ou Roku e os envia para a Edge Network. Os dados poderão então ser enviados para o Customer Journey Analytics ou Adobe Analytics.

  Para obter mais informações sobre o Media for Edge Network SDK / Extensão, consulte [Implementar a Coleção de Mídia de Streaming usando o Edge Network](/help/implementation/edge/implementation-edge.md).

* **API do Media Edge:** pode ser personalizada para coletar dados de qualquer dispositivo ou formato (incluindo dispositivos móveis, da Web e dispositivos OTT) e enviar dados para a Edge Network. Os dados poderão então ser enviados para o Customer Journey Analytics ou Adobe Analytics.

  Para obter mais informações sobre a API do Media Edge, consulte [Visão geral da API do Media Edge](https://developer.adobe.com/cja-apis/docs/endpoints/media-edge/).

![Fluxo de trabalho do CJA](assets/streaming-media-edge.png)

## Métodos de implementação somente do Adobe Analytics

Os métodos de implementação do Edge descritos acima são recomendados para Customer Journey Analytics e Adobe Analytics, especialmente para novas implementações.

Além dos métodos de implementação do Edge, outros métodos de implementação estão disponíveis. Esses métodos de implementação foram projetados para uso com o Adobe Analytics. No entanto, clientes com qualquer um dos métodos de implementação a seguir ainda podem disponibilizar dados no Customer Journey Analytics, criando uma [Conexão de origem do Analytics](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/adobe-applications/analytics.html?lang=pt-BR).

Os métodos de implementação exclusivos do Adobe Analytics usam o complemento Adobe Analytics para mídia de streaming.

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
