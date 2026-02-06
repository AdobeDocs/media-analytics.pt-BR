---
title: Pré-requisitos para implementações somente do Adobe Analytics
description: Saiba mais sobre os pré-requisitos para usar a coleção de mídia de transmissão com implementações somente do Adobe Analytics ou do Edge
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
exl-id: 7b042e45-e35a-43d6-b59e-282573c6a326
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 10%

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
