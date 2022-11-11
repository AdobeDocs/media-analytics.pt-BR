---
title: Como configurar um SDK móvel usando tags para mídia de transmissão
description: Saiba como implementar o Adobe Streaming Media para aplicativos móveis.
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 31%

---

# Instalar SDKs móveis {#install-mobile-sdks}

Para implementar a mídia de transmissão para aplicativos móveis no Android ou iOS, instale e configure o seguinte:

* **SDK móvel da Adobe Experience Platform**

   Para coletar dados, use Tags no Adobe Experience Platform. Tags na Adobe Experience Platform é uma solução de gerenciamento de tags que permite implantar o código do Analytics junto com outros requisitos de marcação.

* **SDK do Media para Android** ou **SDK do Media para iOS**

* **Extensão Adobe Media Analytics for Audio and Video**

Para baixar os SDKs e obter recursos adicionais de documentação, consulte [Obter SDKs do Media, extensões usando tags e SDKs OTT](/help/getting-started/download-sdks.md)

* **Obter parâmetros de configuração válidos**

   Esses parâmetros podem ser obtidos de um representante do Adobe após a configuração da sua conta do Analytics.

* **Inclua as seguintes APIs no reprodutor de mídia**

   * *Uma API para assinar eventos do player* - O SDK de mídia exige que você chame um conjunto de APIs simples quando eventos ocorrem no player.

   * *Uma API que fornece informações sobre o reprodutor* - Isso inclui informações sobre a reprodução no momento, como o nome da mídia, a posição do indicador de reprodução, os anúncios ou o capítulo.
