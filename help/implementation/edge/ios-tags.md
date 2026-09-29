---
title: Configurar o iOS para mídia de transmissão com tags
description: Configure a coleção de mídia de transmissão para o iOS usando a extensão de tag Adobe Streaming Media for Edge Network.
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
source-wordcount: '269'
ht-degree: 0%
---
# Configurar o iOS para mídia de transmissão com tags

É possível configurar a coleção de mídia de transmissão para o aplicativo iOS ou tvOS por meio de uma propriedade móvel Tags, com as configurações de mídia gerenciadas na interface da Coleção de dados. Esta página aborda a configuração de Tags. Para configurar a SDK no código, consulte [Configurar o iOS para mídia de streaming](ios.md).

* **Pré-requisitos**:
  * Conclua a [visão geral da implementação do Edge](overview.md) (esquema, conjunto de dados, sequência de dados com o [!UICONTROL Media Analytics] habilitado).
  * Crie uma propriedade móvel na interface da Coleção de dados. Consulte [Mídia de Streaming do Adobe para Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/).

## Configurar a extensão

1. Na interface da Coleção de dados, abra a propriedade móvel e selecione **[!UICONTROL Extensões]**.
1. Na guia **[!UICONTROL Catálogo]**, localize a extensão **Mídia de Streaming do Adobe para Edge Network** e selecione **[!UICONTROL Instalar]**.
1. Defina o seguinte e salve:
   * **[!UICONTROL Canal]**: o nome do canal relatado com cada sessão.
   * **[!UICONTROL Nome do reprodutor]**: o nome do reprodutor de mídia em uso.
   * **[!UICONTROL Versão do aplicativo]**: a versão do seu aplicativo de reprodução.
1. Publique suas alterações, adicione as dependências de `AEPCore`, `AEPEdge`, `AEPEdgeIdentity` e `AEPEdgeMedia` ao seu aplicativo e registre-as no Mobile Core.

## Rastrear eventos de mídia

Com a propriedade publicada e o rastreador criado, rastreie cada evento de mídia usando seu método de rastreador. Consulte a guia **iOS** em cada página de [evento](/help/implementation/events/overview.md) e [variável](/help/implementation/variables/overview.md) para obter as chamadas exatas.

## Próxima etapa

Uma vez concluída a implementação, você pode [Configurar relatórios para implementações do Edge](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Mídia de Streaming do Adobe para Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)
>* [Configurar o iOS para mídia de streaming (no código)](ios.md)
>* [Visão geral dos eventos](/help/implementation/events/overview.md)
