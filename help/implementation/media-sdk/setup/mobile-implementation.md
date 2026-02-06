---
title: Como configurar uma SDK móvel usando tags para serviços de mídia de transmissão
description: Saiba como implementar os serviços de mídia de transmissão da Adobe para aplicativos móveis.
feature: Streaming Media
role: User, Admin, Developer
exl-id: b4944b5f-cbae-4efc-9ef7-962d3f342240
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 70%

---

# Instalar SDKs móveis {#install-mobile-sdks}

Para implementar os serviços de mídia de transmissão da Adobe para aplicativos móveis no Android ou iOS, instale e configure o seguinte:

* **SDK móvel da Adobe Experience Platform**

  Para coletar dados, use uma das seguintes opções:
   * Tags no Adobe Experience Platform. Tags na Adobe Experience Platform é uma solução de gerenciamento de tags que permite implantar o código do Analytics junto com outros requisitos de marcação.
   * Adobe Experience Platform Edge

* **SDK de mídia para Android** ou **SDK de mídia para iOS**

* **Extensão do Adobe Media Analytics para áudio e vídeo**

Para baixar os SDKs e obter recursos adicionais de documentação, consulte [Obter SDKs de mídia, extensões usando tags e SDKs OTT](/help/getting-started/download-sdks.md)

* **Obter parâmetros de configuração válidos**

  Esses parâmetros podem ser obtidos com um representante da Adobe após a configuração da conta do Analytics.

* **Inclua as seguintes APIs em seu reprodutor de mídia**

   * *Uma API para assinar eventos do player* - O SDK de mídia exige que você chame um conjunto de APIs simples quando eventos ocorrem no player.

   * *Uma API que fornece informações sobre o reprodutor* - Isto inclui informações sobre a reprodução no momento, como o nome da mídia, a posição do indicador de reprodução, os anúncios ou o capítulo.
