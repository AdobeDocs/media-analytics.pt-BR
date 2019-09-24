---
seo-title: Visão geral
title: Visão geral
uuid: c14bdbef-5846-4d31-8a14-8e9e0e9c9861
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Visão geral{#overview}

A API da coleção de mídia é a alternativa RESTful da Adobe para o SDK do Media no lado do cliente. Com a API da coleção de mídia, o reprodutor pode rastrear eventos de áudio e vídeo usando chamadas RESTful HTTP. A API Media Collection oferece o mesmo rastreamento em tempo real do SDK de mídia, além de um recurso adicional:

* **Rastreamento de conteúdo baixado**

   Este recurso fornece a você a capacidade de rastrear mídia enquanto um usuário está offline, por meio do armazenamento local de dados do evento até que o dispositivo do usuário retorne online. (Consulte [Rastrear o conteúdo baixado](track-downloaded-content.md) para obter detalhes.)

A API da coleção de mídia é essencialmente um adaptador e atua como uma versão no lado do servidor do SDK do Media. Isso significa que alguns aspectos da documentação do SDK de mídia também são relevantes para a API de coleta de mídia. Por exemplo, ambas as soluções usam os mesmos Parâmetros [de](/help/metrics-and-metadata/audio-video-parameters.md)áudio e vídeo, e os dados coletados de rastreamento de áudio e vídeo levam aos mesmos [Relatórios e análises.](/help/media-reports/media-reports-enable.md)

## Fluxos de dados de rastreamento de mídia {#section_pwq_n34_qbb}

A media player implementing the Media Collection API makes RESTful API tracking calls directly to the media tracking back-end server, whereas a player implementing the Media SDK makes tracking calls to the SDK APIs inside the player app. Um resultado de fazer chamadas pela Web é que o reprodutor que implementa a API da coleção de mídia precisa lidar com parte do processamento que o SDK do Media realiza automaticamente. (Detalhes na implementação da coleção [de mídia.](mc-api-impl/mc-api-quick-start.md))

The tracking data captured with the Media Collection API is sent and initially processed differently than the tracking data captured in a Media SDK player, but the same processing engine on the back-end is used for both solutions.

![](assets/col_api_overview_simple.png)

## Visão geral da API {#section_y4n_mcl_kcb}

**URI:** obtenha essa informação do seu representante da Adobe.

**Método HTTP:** POST, com corpo de solicitação JSON.

### Chamadas à APIs {#mc-api-calls}

* **`sessions`-** Estabelece uma sessão com o servidor e retorna uma ID de sessão que será usada nas chamadas de `events` subsequentes. Seu aplicativo realiza essa chamada uma vez no início de uma sessão de rastreamento.

   ```
   {uri}/api/v1/sessions
   ```

* **`events`-** Envia dados de rastreamento de mídia.

   ```
   {uri}/api/v1/sessions/{session-id}/events
   ```

### Corpo da solicitação {#mc-api-request-body}

```
{ 
    "playerTime": { 
        "playhead": {playhead position in seconds}, 
        "ts": {timestamp in milliseconds} 
    }, 
    "eventType": {event-type}, 
    "params": { 
        {parameter-name}: {parameter-value}, 
        ... 
        {parameter-name}: {parameter-value} 
    }, 
    "qoeData" : { 
        {parameter-name}: {parameter-value}, 
        ... 
        {parameter-name}: {parameter-value} 
    }, 
    "customMetadata": { 
        {parameter-name}: {parameter-value}, 
        ... 
        {parameter-name}: {parameter-value} 
    } 
} 
```

* `playerTime` - Obrigatória para todos os pedidos.
* `eventType` - Obrigatória para todos os pedidos.
* `params` - Obrigatório para determinados `eventTypes`; verifique o [esquema de validação JSON](mc-api-ref/mc-api-json-validation.md) para determinar quais eventTypes são obrigatórios e quais são opcionais.

* `qoeData` - Opcional para todas as solicitações.
* `customMetadata` - Opcional para todas as solicitações, mas enviado somente com `sessionStart`, `adStart`e tipos `chapterStart` de eventos.

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

