---
title: Configurar a API do Media Edge para mídia de transmissão
description: Envie dados de streaming de mídia diretamente para a Edge Network usando a API do Media Edge.
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
source-wordcount: '211'
ht-degree: 0%
---
# Configurar a API do Media Edge para mídia de transmissão

Se não conseguir usar o Web SDK, o Mobile SDK ou o Roku Edge SDK (por exemplo, em um tempo de execução personalizado ou não suportado), você poderá enviar dados de streaming de mídia diretamente para o Edge Network com a API do Media Edge. A API usa chamadas RESTful HTTP e é totalmente personalizável.

* **Pré-requisitos**: conclua a [visão geral da implementação do Edge](overview.md) (esquema, conjunto de dados, sequência de dados com o [!UICONTROL Media Analytics] habilitado).

## Enviar eventos de mídia para a Edge Network

Os eventos de mídia são enviados para os endpoints do `/ee/va/v1/`, digitados em sua sequência de dados pelo parâmetro de consulta `configId`. Por exemplo, uma sessão começa com um POST para `sessionStart`:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId=<datastreamID>" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": { "name": "video-123", "playerName": "player_name", "contentType": "vod", "length": 128, "channel": "sample_channel" },
        "playhead": 0
      }
    }
  }]
}'
```

A resposta retorna a ID da sessão que todos os eventos subsequentes devem incluir. Para obter o conjunto completo de pontos de extremidade, os formatos de solicitação/resposta e a especificação OpenAPI, consulte a [Referência da API do Media Edge](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/).

## Rastrear eventos de mídia

Consulte a guia **API do Media Edge** em cada página de [evento](/help/implementation/events/overview.md) e [variável](/help/implementation/variables/overview.md) para obter as cargas exatas.

## Próxima etapa

Uma vez concluída a implementação, você pode [Configurar relatórios para implementações do Edge](/help/reporting/setup/edge-reporting.md).

>[!MORELIKETHIS]
>
>* [Referência da API do Media Edge](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/)
>* [Visão geral dos eventos](/help/implementation/events/overview.md)
>* [Visão geral das variáveis](/help/implementation/variables/overview.md)
