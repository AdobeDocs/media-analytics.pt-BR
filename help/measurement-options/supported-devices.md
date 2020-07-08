---
title: Dispositivos e plataformas compatíveis
description: O Adobe Analytics para áudio e vídeo garante que cada fluxo de mídia seja coletado e relatado em todos os dispositivos.
translation-type: ht
source-git-commit: 4db4e4281ba9c7af078c18d03f73b6e1e007a0e8
workflow-type: ht
source-wordcount: '338'
ht-degree: 100%

---


# Dispositivos e plataformas compatíveis {#devices-supported}

>[!IMPORTANT]
>
>Com o fim do suporte para SDKs móveis da versão 4 em 31 de agosto de 2021, a Adobe também encerrará o suporte para o SDK do Media Analytics para iOS e Android.  Para obter mais informações, consulte [Perguntas frequentes sobre o fim do suporte do SDK do Media Analytics](/help/sdk-implement/end-of-support-faqs.md).

O Adobe Analytics para áudio e vídeo é compatível com todos os principais dispositivos, inclusive:

* Smartphones e tablets iOS e Android
* Dispositivos OTT para ROKU, AppleTV, FireTV e Android TV
* Navegador JavaScript para desktop e laptop

Os SDKs de mídia são atualizados regularmente quando novas versões de dispositivos são lançadas, e você pode usar o SDK para integrar a maioria dos maiores players de mídia de hoje, incluindo Brightcove e Ooyala.

Para dispositivos ou plataformas que não têm suporte para SDK no momento ou em situações em que você não deseja usar um SDK, é possível implementar a API da coleção de mídia. A API da coleção de mídia permite fazer chamadas RESTful API diretamente de um dispositivo ou plataforma para o backend do Media Analytics.

A tabela abaixo lista os dispositivos e as plataformas compatíveis no momento. Para baixar a versão mais recente do SDK, consulte [Baixar SDKs](https://docs.adobe.com/content/help/pt-BR/media-analytics/using/sdk-implement/download-sdks.html). Se um dispositivo não estiver listado, entre em contato com o Atendimento ao cliente ou com o consultor de soluções para saber o status desse dispositivo.

| Plataformas e dispositivos de transmissão |  | Extensão do Media Launch c/ AEP SDK | SDK do Media | API da coleção de mídia |
|:---------------------------:|:-----------------------------------------------:|:----------------------------:|:-------------------:|:--------------------:|
| Web/Web móvel |  |  |  |  |
|  | Navegadores JavaScript | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png)    | ![](/help/assets/icon-blue-check.png) |
| Aplicativo móvel |  |  |  |  |
|  | Dispositivos iOS | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Dispositivos Android | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Dispositivos Windows |  |  | ![](/help/assets/icon-blue-check.png) |
| OTT |  |  |  |  |
|  | Apple TV  (tvOS) | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | ROKU |  | ![](/help/assets/icon-blue-check.png)   <br>(BrightScript) | ![](/help/assets/icon-blue-check.png)<br>(nativo) |
|  | Fire TV (Fire OS) | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Android TV | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Chromecast |  | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) |
|  | Consoles de jogos (ex: Xbox ONE, PS3/PS4 Sony) |  |  | ![](/help/assets/icon-blue-check.png) |
|  | Conversores (ex: xfinity X1) |  |  | ![](/help/assets/icon-blue-check.png) |
|  | Smart TVs (ex: Samsung, LG, Sony, Vizio) |  | ![](/help/assets/icon-blue-check.png)   <br>(baseado na Web) | ![](/help/assets/icon-blue-check.png) |
| Outro |  |  |  |  |
|  | Novos dispositivos conectados |  |  | ![](/help/assets/icon-blue-check.png) |

1. O suporte para esses SDKs termina em 31 de agosto de 2021. Para obter mais informações, consulte [Perguntas frequentes sobre o fim do suporte do SDK do Media Analytics](/help/sdk-implement/end-of-support-faqs.md).

Para obter mais informações sobre as versões mínimas da plataforma compatíveis com cada SDK, consulte [Suporte à versão mínima da plataforma](https://docs.adobe.com/content/help/pt-BR/media-analytics/using/sdk-implement/setup/setup-overview.html).
