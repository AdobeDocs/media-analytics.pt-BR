---
seo-title: Overview
title: Visão geral da API de coleção de mídia de streaming
description: Saiba mais sobre a API de coleção de mídia e como o reprodutor pode rastrear eventos de áudio e vídeo usando chamadas RESTful HTTP.
uuid: c14bdbef-5846-4d31-8a14-8e9e0e9c9861
exl-id: 58430636-7fab-433a-8ead-52ccaa45d920
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/79XLYzuvi3neUuCrt3LcGEwnnaR038-mWHMuSrY797M
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 331
ht-degree: 96%

---

# Visão geral da API de coleção de mídia {#overview}

A API Media Collection é a alternativa RESTful da Adobe para o SDK do Media no lado do cliente. Com a API Media Collection, o reprodutor pode rastrear eventos de áudio e vídeo usando chamadas RESTful HTTP.

A API Media Collection é essencialmente um adaptador e atua como uma versão no lado do servidor do SDK do Media. Os dados de rastreamento de streaming de mídia coletados levam aos mesmos [Relatórios e Análise](/help/reporting/media-reports-enable.md).

## Fluxos de dados de rastreamento de mídia {#media-tracking-data-flows}

Um reprodutor de mídia que implementa a API Media Collection faz chamadas de rastreamento da API RESTful diretamente para o servidor de back-end do rastreamento de mídia, enquanto um reprodutor que implementa o SDK do Media faz chamadas de rastreamento para as APIs do SDK dentro do aplicativo. Um resultado de fazer chamadas pela Web é que o reprodutor que implementa a API Media Collection precisa lidar com parte do processamento que o SDK do Media realiza automaticamente. (Detalhes em [Implementação da coleção do Media.](mc-api-impl/mc-api-quick-start.md))

Os dados de rastreamento capturados com a API Media Collection são enviados e processados inicialmente de forma diferente dos dados de rastreamento capturados em um reprodutor do SDK do Media, mas o mesmo mecanismo de processamento do no back-end é usado para ambas as soluções.

![](assets/col_api_overview_simple.png)

## Visão geral da API {#api-overview}

**URI:** solicite ao representante da Adobe.

**Método HTTP:** POST, com o corpo da solicitação JSON.

### Chamadas à APIs {#mc-api-calls}

* **`sessions`-** Estabelece uma sessão com o servidor e retorna uma ID de sessão que será usada nas chamadas de `events` subsequentes. Seu aplicativo realiza essa chamada uma vez no início de uma sessão de rastreamento.

  `{uri}/api/v1/sessions`

* **`events`-** Envia os dados de rastreamento de mídia.

  `{uri}/api/v1/sessions/{session-id}/events`

### Corpo da solicitação {#mc-api-request-body}

```json
{
    "playerTime": {
        "playhead": "{playhead position in seconds}",
        "ts": "{timestamp in milliseconds}"
    },
    "eventType": "{event-type}",
    "params": {
        "{parameter-name}": "{parameter-value}",
        "{parameter-name}": "{parameter-value}"
    },
    "qoeData" : {
        "{parameter-name}": "{parameter-value}",
        "{parameter-name}": "{parameter-value}"
    },
    "customMetadata": {
        "{parameter-name}": "{parameter-value}",
        "{parameter-name}": "{parameter-value}"
    }
}
```

* `playerTime` - Obrigatório para todas as solicitações.
* `eventType` - Obrigatório para todas as solicitações.
* `params` - Obrigatório para determinados `eventTypes`; verifique o [esquema de validação JSON](mc-api-ref/mc-api-json-validation.md) para determinar quais eventTypes são obrigatórios e quais são opcionais.

* `qoeData` - Opcional para todas as solicitações.
* `customMetadata` - Opcional para todas as solicitações, mas somente enviado com os tipos de evento `sessionStart`, `adStart` e `chapterStart`.

Para cada `eventType`, há um [esquema de validação JSON](mc-api-ref/mc-api-json-validation.md) disponível publicamente que você deve usar para verificar os tipos de parâmetros e se um parâmetro é opcional ou obrigatório para um evento específico.

### Tipos de evento {#mc-api-event-types}

* `sessionStart`
* `play`
* `ping`
* `pauseStart`
* `bufferStart`
* `adStart`
* `adComplete`
* `adSkip`
* `adBreakStart`
* `adBreakComplete`
* `chapterStart`
* `chapterSkip`
* `chapterComplete`
* `sessionEnd`
* `sessionComplete`
* `stateStart`
* `stateEnd`
