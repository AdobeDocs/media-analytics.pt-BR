---
title: Pré-requisitos para implementações exclusivas do Adobe Analytics
description: Saiba mais sobre os pré-requisitos para usar mídia de transmissão com implementações somente do Adobe Analytics
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: 8a0f2c0b367b48ee5ac94e7fc6bcd0eadafbc5d8
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 13%

---

# Pré-requisitos para implementações do Edge

Os pré-requisitos descritos nesta seção são específicos para implementar a mídia de transmissão com implementações de borda.

1. **Conclua os pré-requisitos gerais**<br>
Se você implementar a Mídia de transmissão somente para implementações do Adobe Analytics ou para implementações do Edge, certifique-se de atender aos [pré-requisitos gerais](/help/getting-started/prereqs.md).

1. **Confirme se você está implementando uma solução de Adobe compatível com Edge e mídia de transmissão**<br>
Ao implementar a Mídia de transmissão com o Edge, você também deve ter uma implementação de Customer Journey Analytics, Adobe Analytics, Adobe Journey Optimizer ou Real-time Customer Data Platform em funcionamento. Consulte os seguintes recursos de documentação para obter mais informações:
   * [Guia do Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=pt-BR)
   * [Implementação do Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=pt-BR)
   * [Documentação do Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=pt-BR)
   * [Documentação do Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html)

1. **Obter o URL do servidor de rastreamento de mídia**<br>
Solicite ao representante do Customer Journey Analytics o URL do servidor de rastreamento de mídia. <!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **Instalar o Media Analytics com o Edge**<br>
Siga as etapas em [Instale o Media Analytics com Experience Platform Edge](/help/implementation/edge/implementation-edge.md).