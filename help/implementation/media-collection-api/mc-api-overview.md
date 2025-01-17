---
seo-title: Overview
title: Visão geral da API de coleção de mídia de streaming
description: Saiba mais sobre a API de coleção de mídia e como o reprodutor pode rastrear eventos de áudio e vídeo usando chamadas RESTful HTTP.
uuid: c14bdbef-5846-4d31-8a14-8e9e0e9c9861
exl-id: 58430636-7fab-433a-8ead-52ccaa45d920
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 7a1ae72af231659bd794fb18ce9e76685e6beff4
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 93%

---

# Visão geral da API de coleção de mídia {#overview}

A API Media Collection é a alternativa RESTful da Adobe para o SDK do Media no lado do cliente. Com a API Media Collection, o reprodutor pode rastrear eventos de áudio e vídeo usando chamadas RESTful HTTP.

A API Media Collection é essencialmente um adaptador e atua como uma versão no lado do servidor do SDK do Media. Isso significa que alguns aspectos da documentação do SDK do Media também são relevantes para a API Media Collection. Por exemplo, ambas as soluções usam os mesmos [Parâmetros de streaming de mídia](../variables/audio-video-parameters.md), e os dados de rastreamento de streaming de mídia coletados levam aos mesmos [Relatórios e Análises.](/help/reporting/media-reports-enable.md)

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
