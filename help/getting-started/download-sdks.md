---
title: Acesse links para baixar SDKs do Media Analytics
description: Links de download de SDKs para plataformas disponíveis, incluindo Android, iOS, JavaScript, Chromecast e Roku.
uuid: a619fbb8-693e-4583-8dad-0ff875e715f8
exl-id: d211fa2e-d5b0-4e9f-bdb7-eda838194f3d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 81%

---

# Obter SDKs de mídia, extensões que utilizam tags e SDKs OTT {#download-sdks}

As informações nesta página incluem links para baixar os SDKs de mídia atuais e obter as extensões de mídia que utilizam tags.

As tags da Adobe Experience Platform são a próxima geração de recursos de gerenciamento de tags de site e de SDKs móveis da Adobe. As tags oferecem uma forma simples de implantar e gerenciar todas as soluções de análise, de marketing e de anúncios necessárias para potencializar experiências de cliente relevantes. Para obter mais informações sobre tags, consulte [Visão geral das tags](https://experienceleague.adobe.com/docs/platform-learn/data-collection/overview.html?lang=pt-BR).


>[!NOTE]
>
>Para obter informações sobre como baixar SDKs herdadas, consulte [Herdados - Baixar SDKs](/help/legacy/legacy-download-sdks.md).<br>
>Para obter informações importantes sobre o fim do suporte, consulte [Perguntas frequentes sobre o fim do suporte](/help/additional-resources/end-of-support-faqs.md).

## SDKs de mídia e bibliotecas móveis {#media-sdks-libraries}

### Implementação da Web {#download-web-sdk}

| Plataforma compatível | Soluções compatíveis | Método de implementação | Versão |  APIs   |  Documentação  |  Amostra  |
|:---:|---|---|---|---| ---| ---|
| ![Ícone do JavaScript ](assets/javascript-icon.png)</br>**API do JavaScript** | Adobe Analytics | Somente do Analytics | Web - [SDK de mídia para JS v3.0.2](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2) | [Referência da API JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) | [Instalar o SDK de Mídia usando o JavaScript](/help/implementation/media-sdk/setup/web-implementation.md) | [Amostra do SDK de mídia para JS v3.0.2](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/js/3.x) |
| ![Ícone do JavaScript ](assets/javascript-icon.png)</br>**API do JavaScript** | Adobe Analytics | Somente do Analytics | Web - Extensão de mídia |  | [Extensão do Adobe Media Analytics (SDK 3.x) para áudio e vídeo com o uso de tags (coleção de dados)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=pt-BR) | [Amostra da extensão do Adobe Media Analytics (SDK 3.x) para áudio e vídeo](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x) |
| </br>**Web** | Adobe Analytics<p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | Web - Experience Platform Edge |  | [Implementar o Complemento de Coleção de Mídia de Streaming usando o Edge Network](/help/implementation/edge/implementation-edge.md) <p>e</p><p>[Enviar dados da Web para a Edge com o SDK da Web da Adobe Experience Platform](/help/implementation/edge/edge-web-sdk.md)</p> | |

### Implementação móvel {#get-mobile-extension}

| Plataforma compatível | Soluções compatíveis | Método de implementação | Versão |  Documentação   |  Amostras  |
|:---:|---|---|---|---|---|
| ![Ícone do Android ](assets/android-icon.png)</br>**Android** | Adobe Analytics | Somente do Analytics | Android - Extensão de mídia | [Documentação do SDK móvel](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Adobe Analytics - Amostra do Media Analytics para áudio e vídeo](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/mobile/android) |
| ![Ícone do Apple iOS ](assets/ios-icon.png)<br>**tvOS** | Adobe Analytics | Somente do Analytics | iOS/tvOS - Extensão de mídia | [Documentação do SDK móvel](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Adobe Analytics - Amostra do Media Analytics para áudio e vídeo](https://github.com/adobe/aepsdk-media-ios/tree/main/TestApp) |
| ![Ícone do Android ](assets/android-icon.png)</br>**Android** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | Android - Experience Platform Edge | [Instalar o SDK de Mídia usando o JavaScript](/help/implementation/edge/implementation-edge.md) | |
| ![Ícone do Apple iOS ](assets/ios-icon.png)<br>**tvOS** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | iOS / tvOS - Experience Platform Edge | [Instalar o SDK de Mídia usando o JavaScript](/help/implementation/edge/implementation-edge.md) |  |

### Implementação Over-the-top (OTT) {#download-ott-libraries}

| Plataforma compatível | Soluções compatíveis | Método de implementação | Versão |  APIs   |  Documentação  |
|:---:|---|---|---|---|---|
| ![Ícone do Chromecast ](assets/chromecast-icon.png)</br>**Chromecast** | Adobe Analytics | Somente do Analytics | [SDK para Chromecast v3.0.3](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3) | [Referência da API do Chromecast](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/) | [Configurar o SDK móvel v3.x para Chromecast](/help/implementation/media-sdk/setup/set-up-chromecast.md) |
| ![Ícone do Roku ](assets/roku-icon.png)</br>**Roku** | Adobe Analytics | Somente do Analytics | [SDK para Roku v2.2.6](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.6) |  | [Configurar o SDK móvel v2.x para Roku](/help/implementation/media-sdk/setup/set-up-roku.md) |
| ![Ícone do Roku ](assets/roku-icon.png)</br>**Roku** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | [SDK do Adobe Experience Platform Roku](https://github.com/adobe/aepsdk-roku/tree/main) |  | [Instalar o SDK de Mídia usando o JavaScript](/help/implementation/edge/implementation-edge.md) |
