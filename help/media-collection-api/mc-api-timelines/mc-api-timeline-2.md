---
title: Linha do tempo 2 - Usuário abandona a sessão
description: null
uuid: 74b89e8f-ef56-4e0c-b9a8-40739e15b4cf
translation-type: ht
source-git-commit: c86c7932f932af0a121e0b757921973d6f4084e8
workflow-type: ht
source-wordcount: '634'
ht-degree: 100%

---


# Linha do tempo 2 - Usuário abandona a sessão {#timeline--2-user-abandons-session}

## VOD, anúncios precedentes, anúncios intermediários, usuário abandona o conteúdo antecipadamente

Os diagramas a seguir ilustram a linha do tempo do indicador de reprodução e a linha do tempo correspondente das ações de um usuário. Os pormenores de cada ação e os pedidos que a acompanham são apresentados a seguir.


![](assets/va_api_content_2.png)


![](assets/va_api_actions_2.png)


## Detalhes da ação

### Ação 1 — Iniciar sessão {#Action-1}

| Ação | Linha do tempo de ação (segundos) | Posição do indicador de reprodução (segundos) | Solicitação de cliente |
| --- | :---: | :---: | --- |
| Botão Reproduzir automaticamente ou Reproduzir pressionado | 0 | 0 | `/api/v1/sessions` |

**Detalhes da implementação**

Essa chamada sinaliza _a intenção do usuário de reproduzir_ um vídeo. Retorna uma ID de sessão (`{sid}`) ao cliente usada para identificar todas as chamadas de rastreamento subsequentes na sessão. O estado do reprodutor ainda não é &quot;reproduzindo&quot;, mas &quot;iniciando&quot;.  [Os parâmetros obrigatórios da sessão](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) devem ser incluídos no mapa `params` no corpo da solicitação.  No back-end, essa chamada gera uma chamada de inicialização do Adobe Analytics.

**Exemplo de corpo da solicitação**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:sessionStart, params: {
        "media.playerName": "sample-html5-api-player",
        "analytics.trackingServer": "[ _YOUR-TS_ ]",
        "analytics.reportSuite": "[ _YOUR-RSID_ ]",
        "analytics.visitorId": "[ _YOUR-VISITOR-ID_ ]",
        "media.contentType": "VOD",
        "media.length": 60.3333333333333,
        "media.id": "VA API Sample Player",
        "visitor.marketingCloudOrgId": "[YOUR-MCID]",
        "media.name": "ClickMe",
        "media.channel": "sample-channel",
        "media.sdkVersion": "va-api-0.0.0",
        "analytics.enableSSL": false
    }
}
```

### Ação 2 — Início do temporizador de ping {#Action-2}

| Ação | Linha do tempo de ação (segundos) | Posição do indicador de reprodução (segundos) | Solicitação de cliente |
| --- | :---: | :---: | --- |
| Temporizador do evento ping de início do aplicativo | 0 | 0 |  |

**Detalhes da implementação**

Inicie o temporizador de ping do aplicativo. O primeiro evento de ping deve disparar 1 segundo se houver anúncios precedentes, 10 segundos se não houver.

### Ação 3 — Início de quebra de anúncio {#Action-3}

| Ação | Linha do tempo de ação (segundos) | Posição do indicador de reprodução (segundos) | Solicitação de cliente |
| --- | :---: | :---: | --- |
| Rastrear início de ad break antes da exibição | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

Os anúncios antes da exibição devem ser rastreados. Os anúncios somente podem ser rastreados em um ad break.

**Exemplo de corpo da solicitação**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adBreakStart, params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.podIndex": 0,
        "media.ad.podSecond": 0
    }
}
```

### Ação 4 — Início do anúncio {#Action-4}

| Ação | Linha do tempo de ação (segundos) | Posição do indicador de reprodução (segundos) | Solicitação de cliente |
| --- | :---: | :---: | --- |
| Rastrear início do anúncio nº 1 antes da exibição | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

Um anúncio de 12 segundos é iniciado.

**Exemplo de corpo da solicitação**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adStart, params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 1",
        "media.ad.id": "002",
        "media.ad.length": 7,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "1",
        "media.ad.creativeId": "42",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz-creative.com",
        "media.ad.placementId": "sample-placement2"
    },
}
```

### Ação 5 — Pings de anúncios {#Action-5}

| Ação | Linha do tempo de ação (segundos) | Posição do indicador de reprodução (segundos) | Solicitação de cliente |
| --- | :---: | :---: | --- |
| O aplicativo envia o evento de ping | 1 | 0 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

Envie um ping ao back-end a cada 1 segundo. (Pings de anúncios subsequentes não mostrados, por motivos de brevidade.)

**Exemplo de corpo da solicitação**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Ação 6 — Anúncio concluído {#Action-6}

| Ação | Linha do tempo de ação (segundos) | Posição do indicador de reprodução (segundos) | Solicitação de cliente |
| --- | :---: | :---: | --- |
| Rastrear conclusão do anúncio nº 1 antes da exibição | 12 | 0 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

O primeiro anúncio precedente terminou.

**Exemplo de corpo da solicitação**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adComplete
}
```

### Ação 7 — Ad break concluído {#Action-7}

| Ação | Linha do tempo de ação (segundos) | Posição do indicador de reprodução (segundos) | Solicitação de cliente |
| --- | :---: | :---: | --- |
| Rastrear conclusão de ad break antes da exibição | 12 | 0 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

O ad break está concluído. Durante todo o ad break, o player permaneceu no estado de &quot;reprodução&quot;.

**Exemplo de corpo da solicitação**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adBreakComplete
}
```

### Ação 8 — Reproduzir conteúdo {#Action-8}

| Ação | Linha do tempo de ação (segundos) | Posição do indicador de reprodução (segundos) | Solicitação de cliente |
| --- | :---: | :---: | --- |
| Rastrear evento de reprodução | 12 | 0 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

Mova o reprodutor para o estado &quot;reproduzindo&quot;; comece a rastrear o início da reprodução do conteúdo.

**Exemplo de corpo da solicitação**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:play,
    qoeData: { bitrate: 10000 }
}
```

### Ação 9 — Ping {#Action-9}

| Ação | Linha do tempo de ação (segundos) | Posição do indicador de reprodução (segundos) | Solicitação de cliente |
| --- | :---: | :---: | --- |
| O aplicativo envia o evento de ping | 20 | 8 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

Envie um ping ao back-end a cada 10 segundos.

**Exemplo de corpo da solicitação**

```
{
    playerTime: {
        playhead: 8ß,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Ação 10 — Ping {#Action-10}

| Ação | Linha do tempo de ação (segundos) | Posição do indicador de reprodução (segundos) | Solicitação de cliente |
| --- | :---: | :---: | --- |
| O aplicativo envia o evento de ping | 30 | 18 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

Envie um ping ao back-end a cada 10 segundos.

**Exemplo de corpo da solicitação**

```
{
    playerTime: {
        playhead: 18,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Ação 11 — Erro {#Action-11}

| Ação | Linha do tempo de ação (segundos) | Posição do indicador de reprodução (segundos) | Solicitação de cliente |
| --- | :---: | :---: | --- |
| Ocorre um erro, o aplicativo envia informações de erro. | 32 | 20 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**


**Exemplo de corpo da solicitação**

```
{
    playerTime: {
        playhead: 20,
        ts: <timestamp>
    },
    eventType:error
}
```

### Ação 12 — Reproduzir conteúdo {#Action-12}

| Ação | Linha do tempo de ação (segundos) | Posição do indicador de reprodução (segundos) | Solicitação de cliente |
| --- | :---: | :---: | --- |
| O aplicativo se recupera do erro, o usuário pressiona Play | 37 | 20 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**



**Exemplo de corpo da solicitação**

```
{
    playerTime: {
        playhead: 18,
        ts: <timestamp>
    },
    eventType:play, qoeData: { bitrate: 10000 }
}
```

### Ação 13 — Ping {#Action-13}

| Ação | Linha do tempo de ação (segundos) | Posição do indicador de reprodução (segundos) | Solicitação de cliente |
| --- | :---: | :---: | --- |
| O aplicativo envia o evento de ping | 40 | 28 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

Envie um ping ao back-end a cada 10 segundos.

**Exemplo de corpo da solicitação**

```
{
    playerTime: {
        playhead: 28,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Ação 14 — Início de quebra de anúncio {#Action-14}

| Ação | Linha do tempo de ação (segundos) | Posição do indicador de reprodução (segundos) | Solicitação de cliente |
| --- | :---: | :---: | --- |
| Rastrear início de ad break durante a exibição | 45 | 33 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

Anúncio intermediário de 8 segundos: envie `adBreakStart` .

**Exemplo de corpo da solicitação**

```
{
    playerTime: {
        playhead: 33,
        ts: <timestamp>
    },
    eventType:adBreakStart, params: {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.podIndex": 1,
        "media.ad.podSecond": 33
    }
}
```

### Ação 15 — Início do anúncio {#Action-15}

| Ação | Linha do tempo de ação (segundos) | Posição do indicador de reprodução (segundos) | Solicitação de cliente |
| --- | :---: | :---: | --- |
| Rastrear início do anúncio nº 1 durante a exibição | 45 | 33 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

Rastreie o anúncio intermediário.

**Exemplo de corpo da solicitação**

```
{
    playerTime: { playhead: 33, ts: <timestamp>
    },
    eventType:adStart, params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 1",
        "media.ad.id": "002",
        "media.ad.length": 8,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "7",
        "media.ad.creativeId": "40",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz_creative.com",
        "media.ad.placementId": "sample_placement2"
    },
}
```

### Ação 16 — Fechar aplicativo {#Action-16}

| Ação | Linha do tempo de ação (segundos) | Posição do indicador de reprodução (segundos) | Solicitação de cliente |
| --- | :---: | :---: | --- |
| O usuário fecha o aplicativo. O aplicativo determina que o usuário abandonou a visualização e não retornou para esta sessão. | 48 | 33 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

Envie `sessionEnd` para o back-end do VA para indicar que a sessão deve ser encerrada imediatamente, sem processamento adicional.

**Exemplo de corpo da solicitação**

```
{
    playerTime: {
        playhead: 33,
        ts: <timestamp>
    },
    eventType:sessionEnd
}
```
