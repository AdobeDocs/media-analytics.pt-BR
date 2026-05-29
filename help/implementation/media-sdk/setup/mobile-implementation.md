---
title: Como configurar uma SDK móvel usando tags para serviços de mídia de transmissão
description: Saiba como implementar os serviços de mídia de transmissão da Adobe para aplicativos móveis.
feature: Streaming Media
role: User, Admin, Developer
exl-id: b4944b5f-cbae-4efc-9ef7-962d3f342240
TQID: https://experienceleague.adobe.com/IfnXB76Qycsic-ezOzZX4X-5RakbTQ0tlt7va6q2fZ8
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 220
ht-degree: 63%

---

# Instalar SDKs móveis {#install-mobile-sdks}

>[!IMPORTANT]
>
>Esta página aborda a implementação do Mobile SDK somente no Analytics. Para a implementação recomendada, consulte [Implementar mídia de transmissão usando o Edge Network](/help/implementation/edge/edge-mobile-sdk.md).

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
