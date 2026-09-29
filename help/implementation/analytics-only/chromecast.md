---
title: Configurar Chromecast para mídia de transmissão
description: Instale e configure o Media SDK para Chromecast para implementações de mídia de transmissão exclusivas do Analytics.
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
source-wordcount: '180'
ht-degree: 10%
---
# Configurar Chromecast para mídia de transmissão

O Media SDK para Chromecast envia dados de mídia de transmissão de aplicativos receptores Chromecast diretamente para o Adobe Analytics. O SDK e sua documentação estão hospedados no GitHub.

* **Pré-requisitos**:
  * Conclua a [visão geral da implementação somente do Analytics](overview.md).
  * [Baixe o Media SDK para Chromecast](/help/getting-started/download-sdks.md).

## Instalar e configurar o SDK

Adicione o SDK ao aplicativo receptor do Chromecast e configure o rastreador conforme descrito nas referências canônicas:

* [Configurar o Chromecast SDK](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/docs/2.x/chromecast-setup.md)
* [Referência da API do SDK do Chromecast](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/)

## Rastrear eventos de mídia

Com o rastreador criado, rastreie cada evento de mídia usando seu método de rastreador. Consulte a guia **Chromecast** em cada página [evento](/help/implementation/events/overview.md) e [variável](/help/implementation/variables/overview.md) para obter as chamadas exatas.

## Próxima etapa

Uma vez concluída a implementação, você pode [Configurar relatórios para implementações somente do Analytics](/help/reporting/setup/analytics-reporting.md).

>[!MORELIKETHIS]
>
>* [Referência da API SDK do Chromecast](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/)
>* [Visão geral dos eventos](/help/implementation/events/overview.md)
>* [Visão geral das variáveis](/help/implementation/variables/overview.md)
