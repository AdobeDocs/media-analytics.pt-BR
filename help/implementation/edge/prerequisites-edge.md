---
title: Pré-requisitos para implementações somente do Adobe Analytics
description: Saiba mais sobre os pré-requisitos para usar a coleção de mídia de transmissão com implementações somente do Adobe Analytics ou do Edge
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
exl-id: 7b042e45-e35a-43d6-b59e-282573c6a326
TQID: https://experienceleague.adobe.com/OqimGafihuirpnAaZ4AvrX2lrOmCtr0FLXk3QwoVTew
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: c77ba355-6681-41fe-b719-563d3f507fdb
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 212
ht-degree: 16%

---

# Pré-requisitos para implementações do Edge

Os pré-requisitos descritos nesta seção são específicos para implementar a coleção de mídia de streaming do Adobe com implementações do Edge.

1. **Concluir os pré-requisitos gerais**<br>
Se você implementar a Coleção de mídia de transmissão somente para implementações do Adobe Analytics ou para implementações do Edge, verifique se atende aos [pré-requisitos gerais](/help/getting-started/prereqs.md).

1. **Confirme se você está implementando uma solução da Adobe compatível com o Edge Network e a Coleção de Mídia de Streaming**<br>
Ao implementar a Coleção de mídia de transmissão com o Edge, você também deve ter uma implementação funcional do Customer Journey Analytics, Adobe Analytics, Adobe Journey Optimizer ou Real-Time Customer Data Platform. Consulte os seguintes recursos de documentação para obter mais informações:
   * [Guia do Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=pt-BR)
   * [Implementação do Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=pt-BR)
   * [Documentação do Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=pt-BR)
   * [Documentação do Real-Time Customer Data Platform](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html)

1. **Obter a URL do servidor de rastreamento de mídia**<br>
Peça ao representante da Customer Journey Analytics a URL do servidor de rastreamento de mídia. <!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **Implementar a Coleção de Mídia de Streaming usando o Edge Network**<br>
Siga as etapas em [Implementar a Coleção de Mídia de Streaming usando o Edge Network](/help/implementation/edge/implementation-edge.md).
