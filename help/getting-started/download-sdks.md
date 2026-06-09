---
title: Obter SDKs, extensões e APIs de mídia
description: Links de download de SDKs para plataformas disponíveis, incluindo Android, iOS, JavaScript, Chromecast e Roku.
uuid: a619fbb8-693e-4583-8dad-0ff875e715f8
exl-id: d211fa2e-d5b0-4e9f-bdb7-eda838194f3d
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/-L2tSDNue-GheYE-krKkpnOh05s5GKZZBz5sFXsBJ3I
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: c77ba355-6681-41fe-b719-563d3f507fdb
  - id: df312454-73c4-43f6-a90e-18f5043f074c
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: 625
ht-degree: 30%

---

# Obter SDKs, extensões e APIs de mídia

## Implementações do Edge (recomendado) {#edge-sdks}

As implementações do Edge coletam dados uma vez e os fornecem por meio do Adobe Experience Platform Edge Network para vários destinos: Adobe Analytics, Customer Journey Analytics, Adobe Journey Optimizer e Real-Time CDP. Para plataformas sem um SDK nativo (como Smart TVs, consoles de jogos e decodificadores de sinais), use a API do Media Edge.

| | Documentação | Amostra |
|:---:|---|---|
| [![Ícone do JavaScript](assets/javascript-icon.png)](https://experienceleague.adobe.com/pt-br/docs/experience-platform/web-sdk/install/overview)<br>[Web SDK](https://experienceleague.adobe.com/pt-br/docs/experience-platform/web-sdk/install/overview) | [Configurar o Web SDK para mídia de streaming](/help/implementation/edge/web-sdk.md) | [Amostra](https://github.com/adobe/alloy-samples/blob/main/media-collection/STANDALONE.md) |
| [![Ícone de extensão](assets/plug.svg)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/web-sdk/overview.html?lang=pt-BR)<br>[extensão de marca do Web SDK](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/web-sdk/overview.html?lang=pt-BR) | [Configurar a extensão de marca do Web SDK para mídia de streaming](/help/implementation/edge/web-sdk-tags.md) | [Amostra](https://github.com/adobe/alloy-samples/blob/main/media-collection/TAGS_IMPL.md) |
| [![Ícone do Android](assets/android.png)](https://github.com/adobe/aepsdk-media-android)<br>[Android SDK](https://github.com/adobe/aepsdk-media-android) | [Configurar o Android para mídia de streaming](/help/implementation/edge/android.md) | [Amostra](https://github.com/adobe/aepsdk-media-android/tree/main/code/testapp) |
| [![Ícone do Apple iOS](assets/apple.png)](https://github.com/adobe/aepsdk-media-ios)<br>[iOS / tvOS SDK](https://github.com/adobe/aepsdk-media-ios) | [Configurar o iOS para mídia de streaming](/help/implementation/edge/ios.md) | [Amostra](https://github.com/adobe/aepsdk-media-ios/tree/main/TestApp) |
| [![Ícone de extensão](assets/plug.svg)](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)<br>[extensão de tag do Android](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Configurar a extensão de tag do Android para mídia de streaming](/help/implementation/edge/android-tags.md) | |
| [![Ícone de extensão](assets/plug.svg)](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)<br>[extensão de tag do iOS/tvOS](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Configurar a extensão de tag do iOS para mídia de streaming](/help/implementation/edge/ios-tags.md) | |
| [![Ícone do Roku](assets/roku-icon.png)](https://github.com/adobe/aepsdk-roku)<br>[Roku Edge SDK](https://github.com/adobe/aepsdk-roku) | [Configurar Roku Edge para mídia de streaming](/help/implementation/edge/roku.md) | [Amostra](https://github.com/adobe/aepsdk-roku/tree/main/sample/simple-videoplayer-channel) |
| [![Ícone de API](assets/api.png)](https://developer.adobe.com/data-collection-apis/docs/api/media-edge)<br>[API do Media Edge](https://developer.adobe.com/data-collection-apis/docs/api/media-edge) | [Configurar a API do Media Edge](/help/implementation/edge/media-edge-api.md) | [Amostra](https://developer.adobe.com/data-collection-apis/docs/getting-started/media-edge-examples) |

## Implementações somente do Analytics {#analytics-only-sdks}

Esses SDKs e extensões enviam dados diretamente para a Adobe Analytics. Para novas implementações, use as implementações do Edge acima. Para trazer os dados existentes do Analytics para o Customer Journey Analytics ou outros aplicativos da Experience Platform, use o [Conector de origem do Analytics](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sources/connectors/adobe-applications/analytics).

| | Documentação | Amostra |
|:---:|---|---|
| [![Ícone do JavaScript](assets/javascript-icon.png)](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2)<br>[Media SDK 3.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2) | [Configurar o JavaScript para mídia de streaming](/help/implementation/analytics-only/javascript.md) | [Amostra](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/js/3.x) |
| [![Ícone de extensão](assets/plug.svg)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=pt-BR)<br>[Extensão de mídia](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=pt-BR) | [Configurar o JavaScript usando marcas para mídia de streaming](/help/implementation/analytics-only/javascript-tags.md) | [Amostra](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x) |
| [![Ícone do Chromecast](assets/chromecast-icon.png)](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3)<br>[Chromecast SDK 3.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3) | [Configurar Chromecast para mídia de streaming](/help/implementation/analytics-only/chromecast.md) | [Amostra](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/chromecast/samples/BasicPlayerSample) |
| [![Ícone do Roku](assets/roku-icon.png)](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.7)<br>[Roku SDK 2.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.7) | [Configurar Roku 2.x para mídia de streaming](/help/implementation/analytics-only/roku-2x.md) | [Amostra](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/roku/samples) |
| [![Ícone de API](assets/api.png)](/help/implementation/media-collection-api/mc-api-overview.md)<br>[API da coleção de mídia](/help/implementation/media-collection-api/mc-api-overview.md) | [Configurar a API da coleção de mídia](/help/implementation/analytics-only/media-collection-api.md) | |
