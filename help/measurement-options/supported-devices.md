---
title: Saiba mais sobre dispositivos e plataformas compatíveis
description: '"Saiba mais sobre os principais dispositivos, como iOS, Android, dispositivos OTT e navegadores JavaScript compatíveis com o Adobe Analytics para mídia de streaming."'
exl-id: 169ff7b9-e577-45b7-8927-74bdcccc0a77
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: f0abffb48a6c0babb37f16aff2e3302bf5dd0cb4
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 98%

---

# Dispositivos e plataformas compatíveis {#devices-supported}

>[!IMPORTANT]
>
>Com o fim do suporte para SDKs móveis da versão 4 em 31 de agosto de 2021, a Adobe também encerrará o suporte para o SDK do Media Analytics para iOS e Android.  Para obter mais informações, consulte [Perguntas frequentes sobre o fim do suporte do SDK do Media Analytics](/help/sdk-implement/end-of-support-faqs.md).

O Adobe Analytics para streaming de mídia é compatível com todos os principais dispositivos, inclusive:

* Smartphones e tablets iOS e Android
* Dispositivos OTT para ROKU, AppleTV, FireTV e Android TV
* Navegador JavaScript para desktop e laptop

Os SDKs de mídia são atualizados regularmente quando novas versões de dispositivos são lançadas, e você pode usar o SDK para integrar a maioria dos maiores players de mídia de hoje, incluindo Brightcove e Ooyala.

Para dispositivos ou plataformas que não têm suporte para SDK no momento ou em situações em que você não deseja usar um SDK, é possível implementar a API da coleção de mídia. A API da coleção de mídia permite fazer chamadas RESTful API diretamente de um dispositivo ou plataforma para o backend do Media Analytics.

A tabela abaixo lista os dispositivos e as plataformas compatíveis no momento. Para baixar a versão mais recente do SDK, consulte [Baixar SDKs](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/download-sdks.html?lang=pt-BR). Se um dispositivo não estiver listado, entre em contato com o Atendimento ao cliente ou com o consultor de soluções para saber o status desse dispositivo.

| Plataformas e dispositivos de transmissão |  | Coleta de dados com o SDK do AEP Mobile | SDK do Media | API da coleção de mídia |
|:---------------------------:|:-----------------------------------------------:|:----------------------------:|:-------------------:|:--------------------:|
| Web/Web móvel |  |  |  |  |
|  | Navegadores JavaScript | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png)    | ![](/help/assets/icon-blue-check.png) |
| Aplicativo móvel |  |  |  |  |
|  | Dispositivos iOS | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Dispositivos Android | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Dispositivos Windows |  |  | ![](/help/assets/icon-blue-check.png) |
| OTT |  |  |  |  |
|  | Apple TV (tvOS) | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | ROKU |  | ![](/help/assets/icon-blue-check.png)   <br>(BrightScript)    | ![](/help/assets/icon-blue-check.png)<br>(nativo) |
|  | Fire TV (Fire OS) | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Android TV | ![](/help/assets/icon-blue-check.png) | ![](/help/assets/icon-blue-check.png) <sup>1</sup> | ![](/help/assets/icon-blue-check.png) |
|  | Chromecast |  | ![](/help/assets/icon-blue-check.png)    | ![](/help/assets/icon-blue-check.png) |
|  | Consoles de jogos (ex: Xbox ONE, PS3/PS4 Sony) |  |  | ![](/help/assets/icon-blue-check.png) |
|  | Conversores (ex: xfinity X1) |  |  | ![](/help/assets/icon-blue-check.png) |
|  | Smart TVs (ex: Samsung, LG, Sony, Vizio) |  | ![](/help/assets/icon-blue-check.png)   <br>(baseado na Web)    | ![](/help/assets/icon-blue-check.png) |
| Outro |  |  |  |  |
|  | Novos dispositivos conectados |  |  | ![](/help/assets/icon-blue-check.png) |

1. O suporte para esses SDKs termina em 31 de agosto de 2021. Para obter mais informações, consulte [Perguntas frequentes sobre o fim do suporte do SDK do Media Analytics](/help/sdk-implement/end-of-support-faqs.md).

Para obter mais informações sobre as versões mínimas da plataforma compatíveis com cada SDK, consulte [Suporte à versão mínima da plataforma](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/setup/setup-overview.html?lang=pt-BR).
