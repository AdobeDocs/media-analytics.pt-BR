---
title: Configurar o iOS para mídia de transmissão
description: Configure o Adobe Experience Platform Mobile SDK no iOS para enviar dados de mídia de transmissão para o Edge Network.
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
source-wordcount: '239'
ht-degree: 0%
---
# Configurar o iOS para mídia de transmissão

A extensão de Streaming de Mídia do Adobe para Edge Network (`AEPEdgeMedia`) coleta dados da sessão de mídia no aplicativo iOS ou tvOS e os envia para a Edge Network. Esta página aborda a configuração no código. Para configurar a SDK por meio de uma propriedade móvel de Marcas, consulte [Configurar a iOS para mídia de streaming com Marcas](ios-tags.md).

* **Pré-requisitos**:
  * Conclua a [visão geral da implementação do Edge](overview.md) (esquema, conjunto de dados, sequência de dados com o [!UICONTROL Media Analytics] habilitado).
  * Adicione as extensões do `AEPCore`, `AEPEdge`, `AEPEdgeIdentity` e `AEPEdgeMedia` ao seu aplicativo. Consulte [Mídia de Streaming do Adobe para Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/) para instalação e registro.

## Configurar mídia para o iOS

Defina as chaves de configuração de mídia ao inicializar o SDK:

```swift
let configuration = [
  "edgeMedia.channel": "sample_channel",
  "edgeMedia.playerName": "player_name",
  "edgeMedia.appVersion": "app_version"
]
MobileCore.updateConfiguration(configuration)
```

Em seguida, crie um rastreador para gerenciar uma sessão de mídia:

```swift
let tracker = Media.createTracker()
```

Para obter as chaves de configuração e a API completa do rastreador, consulte a [Referência da API do Media for Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/api-reference/).

## Rastrear eventos de mídia

Com o rastreador criado, rastreie cada evento de mídia usando seu método de rastreador. Consulte a guia **iOS** em cada página de [evento](/help/implementation/events/overview.md) e [variável](/help/implementation/variables/overview.md) para obter as chamadas exatas.

## Próxima etapa

Uma vez concluída a implementação, você pode [Configurar relatórios para implementações do Edge](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Mídia de Streaming do Adobe para Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)
>* [Configurar o iOS para mídia de streaming com Marcas](ios-tags.md)
>* [Visão geral dos eventos](/help/implementation/events/overview.md)
