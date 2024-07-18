---
title: Pré-requisitos para implementações somente do Adobe Analytics
description: Saiba mais sobre os pré-requisitos para usar o complemento Coleção de mídia de transmissão com implementações somente do Adobe Analytics ou do Edge
feature: Media Analytics, System Requirements
role: User, Admin, Data Engineer
exl-id: 7b042e45-e35a-43d6-b59e-282573c6a326
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 10%

---

# Pré-requisitos para implementações do Edge

Os pré-requisitos descritos nesta seção são específicos para implementar o complemento Adobe Streaming Media Collection com implementações do Edge.

1. **Concluir os pré-requisitos gerais**<br>
Se você implementar o Complemento de Coleção de mídia de streaming para implementações exclusivas do Adobe Analytics ou para implementações do Edge, verifique se atende aos [pré-requisitos gerais](/help/getting-started/prereqs.md).

1. **Confirme se você está implementando uma solução de Adobe compatível com o Edge Network e o Complemento de Coleção de Mídia de Streaming**<br>
Ao implementar o Complemento de coleção de mídia de transmissão com o Edge, você também deve ter uma implementação de Customer Journey Analytics, Adobe Analytics, Adobe Journey Optimizer ou Real-time Customer Data Platform em funcionamento. Consulte os seguintes recursos de documentação para obter mais informações:
   * [Guia do Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=pt-BR)
   * [Implementação do Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=pt-BR)
   * [Documentação do Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=pt-BR)
   * [Documentação do Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html)

1. **Obter a URL do servidor de rastreamento de mídia**<br>
Peça ao representante do Customer Journey Analytics a URL do servidor de rastreamento de mídia. <!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **Implementar o Complemento de Coleção de Mídia de Streaming usando o Edge Network**<br>
Siga as etapas em [Implementar o Complemento de Coleção de Mídia de Streaming usando o Edge Network](/help/implementation/edge/implementation-edge.md).
