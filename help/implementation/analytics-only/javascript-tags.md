---
title: Configurar a extensão de tag do Media Analytics
description: Use a extensão Adobe Media Analytics (3.x SDK) for Audio and Video tag para implementar mídia de transmissão somente no Analytics.
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 12%
---
# Configurar a extensão de tag do Media Analytics

A extensão de tag do Adobe Media Analytics (3.x SDK) para áudio e vídeo implanta o Media SDK para JavaScript (3.x) por meio de tags, sem instalação manual do JavaScript. Esta página aborda a configuração de Tags. Para instalar o SDK no código, consulte [Configurar JavaScript para mídia de streaming](javascript.md). Para novas implementações, considere a [extensão de tag do Web SDK](/help/implementation/edge/web-sdk-tags.md) recomendada para o caminho do Edge.

* **Pré-requisitos**: conclua a [visão geral da implementação somente do Analytics](overview.md).

## Instalar e configurar a extensão

Adicione a instância do Media Tracker a um site habilitado para tags, instalando e configurando a extensão na interface da Coleção de dados. Para obter detalhes sobre instalação e configuração, consulte a [Extensão Adobe Media Analytics (3.x SDK) for Audio and Video](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=pt-BR).

## Rastrear eventos de mídia

Com a extensão configurada, rastreie cada evento de mídia usando seu método de rastreador. Consulte a guia **Media SDK JS 3.x** em cada página de [evento](/help/implementation/events/overview.md) e [variável](/help/implementation/variables/overview.md) para obter as chamadas exatas.

## Próxima etapa

Uma vez concluída a implementação, você pode [Configurar relatórios para implementações somente do Analytics](/help/reporting/setup/analytics-reporting.md).

>[!MORELIKETHIS]
>
>* [Extensão Adobe Media Analytics (3.x SDK) for Audio and Video](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=pt-BR)
>* [Configurar o JavaScript para mídia de streaming (no código)](javascript.md)
>* [Visão geral dos eventos](/help/implementation/events/overview.md)
