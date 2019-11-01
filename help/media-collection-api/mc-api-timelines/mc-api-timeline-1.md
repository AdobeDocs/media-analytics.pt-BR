---
title: Linha do tempo 1 - Visualização do conteúdo até o fim
description: null
uuid: 0ff591d3-fa99-4123-9e09-c4e71ea1060b
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Linha do tempo 1 - Visualização do conteúdo até o fim{#timeline-view-to-end-of-content}

## VOD, anúncios precedentes, pausa, buffer, visualização até o fim do conteúdo

Os diagramas a seguir ilustram a linha do tempo do indicador de reprodução e a linha do tempo correspondente das ações de um usuário. Apresentam-se seguidamente os pormenores de cada ação e os pedidos que a acompanham.


![](assets/va_api_content.png)


![](assets/va_api_actions.png)


## Detalhes da ação

### Ação 1 - Iniciar sessão {#Action-1}

| Ação | Linha do tempo da ação (segundos) | Posição do indicador de reprodução (Segundos) | Solicitação do cliente |
| --- | :---: | :---: | --- |
| Botão Reprodução automática ou Reprodução pressionado, o vídeo começa a ser carregado. | 0 | 0 | `/api/v1/sessions` |

**Detalhes da implementação**

Essa chamada sinaliza _a intenção do usuário de reproduzir_ um vídeo. <br/><br/>Ele retorna uma ID de sessão ( `{sid}`) para o cliente que é usado para identificar todas as chamadas de rastreamento subsequentes na sessão. O estado do reprodutor ainda não é "reproduzindo", mas "iniciando". <br/><br/>[Os parâmetros obrigatórios da sessão](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) devem ser incluídos no mapa `params` no corpo da solicitação. <br/><br/>No back-end, essa chamada gera uma chamada de inicialização do Adobe Analytics.

**Exemplo de corpo da solicitação**

```
{
    playerTime: {
        playhead: 0, ts: <timestamp>
    },
    eventType:sessionStart, params: {
        "media.playerName": "sample-html5-api-player",
        "analytics.trackingServer": "[ _YOUR_TS_ ]",
        "analytics.reportSuite": "[ _YOUR_RSID_ ]",
        "analytics.visitorId": "[ _YOUR_VISITOR_ID_ ]",
        "media.contentType": "VOD",
        "media.length": 60.3333333333333,
        "media.id": "VA API Sample Player",
        "visitor.marketingCloudOrgId": "[YOUR_MCID]",
        "media.name": "ClickMe",
        "media.channel": "sample-channel",
        "media.sdkVersion": "va-api-0.0.0",
        "analytics.enableSSL": false
    }
}
```

### Ação 2 - Início do temporizador de ping {#Action-2}

| Ação | Linha do tempo da ação (segundos) | Posição do indicador de reprodução (Segundos) | Solicitação do cliente |
| --- | :---: | :---: | --- |
| O aplicativo inicia o temporizador de evento de ping | 0 | 0 | `/api/v1/sessions/{sid}/events` |  |

**Detalhes da implementação**

Inicie o temporizador ping do aplicativo. O primeiro evento ping deve disparar 1 segundo se houver anúncios precedentes, 10 segundos se não houver.

### Ação 3 - Início da quebra de anúncio {#Action-3}

| Ação | Linha do tempo da ação (segundos) | Posição do indicador de reprodução (Segundos) | Solicitação do cliente |
| --- | :---: | :---: | --- |
| Rastrear o início do ad break precedente | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

Os anúncios somente podem ser rastreados em um ad break.

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

### Ação 4 - Início do anúncio {#Action-4}

| Ação | Linha do tempo da ação (segundos) | Posição do indicador de reprodução (Segundos) | Solicitação do cliente |
| --- | :---: | :---: | --- |
| Rastrear o início do anúncio nº 1 precedente | 0 | 0 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

Comece a rastrear o primeiro anúncio precedente, que tem 15 segundos de duração. Incluindo metadados personalizados com este `adStart` .

**Exemplo de corpo da solicitação**

```
{
    playerTime: {
        playhead: 0,
        ts: &lt;timestamp&gt;
    },
    eventType:adStart,
    params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 1",
        "media.ad.id": "001",
        "media.ad.length": 15,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "1",
        "media.ad.creativeId": "42",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz_creative.com",
        "media.ad.placementId": "sample_placement"
    },
    customMetadata: {
        "myCustomData1": "CustomData1",
        "myCustomData2": "CustomData2"
    }
}
```

### Ação 5 - Ads {#Action-5}

#### Ação 5.1 - Anúncio ping 1 {#Action-5-1}

| Ação | Linha do tempo da ação (segundos) | Posição do indicador de reprodução (Segundos) | Solicitação do cliente |
| --- | :---: | :---: | --- |
| O aplicativo envia o evento de ping | 1 | 0 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

Faça o ping do backend a cada 1 segundo enquanto estiver dentro de um anúncio.

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

#### Ação 5.2 - Anúncio ping 2 {#Action-5-2}

| Ação | Linha do tempo da ação (segundos) | Posição do indicador de reprodução (Segundos) | Solicitação do cliente |
| --- | :---: | :---: | --- |
| O aplicativo envia o evento de ping | 2 | 0 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

Faça o ping do backend a cada 1 segundo enquanto estiver dentro de um anúncio.

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

#### Ação 5.3 - Anúncio ping 3 {#Action-5-3}


| Ação | Linha do tempo da ação (segundos) | Posição do indicador de reprodução (Segundos) | Solicitação do cliente |
| --- | :---: | :---: | --- |
| O aplicativo envia o evento de ping | 3 | 0 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

Faça o ping do backend a cada 1 segundo enquanto estiver dentro de um anúncio.

>[!NOTE]
>
>Anúncios subsequentes na linha do tempo ignorarão a exibição da série de pings de um segundo
>por razões de brevidade...

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

### Ação 6 - Anúncio concluído {#Action-6}

| Ação | Linha do tempo da ação (segundos) | Posição do indicador de reprodução (Segundos) | Solicitação do cliente |
| --- | :---: | :---: | --- |
| Rastrear o anúncio nº 1 precedente concluído | 15 | 0 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

Rastreie o final do primeiro anúncio precedente.

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

### Ação 7 - Início do anúncio {#Action-7}

| Ação | Linha do tempo da ação (segundos) | Posição do indicador de reprodução (Segundos) | Solicitação do cliente |
| --- | :---: | :---: | --- |
| Rastrear o início do anúncio nº 2 precedente | 15 | 0 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

Rastreie o início do segundo anúncio precedente, que tem 7 segundos de duração.

**Exemplo de corpo da solicitação**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:adStart, params: {
        "media.ad.podFriendlyName": "ad_pod1",
        "media.ad.name": "Ad 2",
        "media.ad.id": "002",
        "media.ad.length": 7,
        "media.ad.podPosition": 1,
        "media.ad.playerName": "Sample Player",
        "media.ad.advertiser": "Ad Guys",
        "media.ad.campaignId": "2",
        "media.ad.creativeId": "44",
        "media.ad.siteId": "XYZ",
        "media.ad.creativeURL": "https://xyz_creative.com",
        "media.ad.placementId": "sample_placement2"
    },
}
```

### Ação 8 - Ads {#Action-8}

| Ação | Linha do tempo da ação (segundos) | Posição do indicador de reprodução (Segundos) | Solicitação do cliente |
| --- | :---: | :---: | --- |
| O aplicativo envia o evento de ping | 20 | 0 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

Faça o ping do backend a cada 1 segundo.

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

### Ação 9 - Anúncio concluído {#Action-9}

| Ação | Linha do tempo da ação (segundos) | Posição do indicador de reprodução (Segundos) | Solicitação do cliente |
| --- | :---: | :---: | --- |
| Rastrear o anúncio nº 2 precedente concluído | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

Rastreie o final do segundo anúncio precedente.

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

### Ação 10 - Conclusão do intervalo de anúncios {#Action-10}

| Ação | Linha do tempo da ação (segundos) | Posição do indicador de reprodução (Segundos) | Solicitação do cliente |
| --- | :---: | :---: | --- |
| Rastrear o ad break precedente concluído | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

O ad break terminou. Durante o ad break, o reprodutor permaneceu no estado "reproduzindo".

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

### Ação 11 - Reproduzir conteúdo {#Action-11}

| Ação | Linha do tempo da ação (segundos) | Posição do indicador de reprodução (Segundos) | Solicitação do cliente |
| --- | :---: | :---: | --- |
| Rastrear evento de reprodução | 22 | 0 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

Depois do evento `adBreakComplete`, coloque o reprodutor no estado "reproduzindo" usando o evento `play`.

**Exemplo de corpo da solicitação**

```
{
    playerTime: {
        playhead: 0,
        ts: <timestamp>
    },
    eventType:play
}
```

### Ação 12 - Ping {#Action-12}

| Ação | Linha do tempo da ação (segundos) | Posição do indicador de reprodução (Segundos) | Solicitação do cliente |
| --- | :---: | :---: | --- |
| O aplicativo envia o evento de ping | 30 | 8 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

Envie um ping ao back-end a cada 10 segundos.

**Exemplo de corpo da solicitação**

```
{
    playerTime: {
        playhead: 8,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Ação 13 - Início do buffer {#Action-13}

| Ação | Linha do tempo da ação (segundos) | Posição do indicador de reprodução (Segundos) | Solicitação do cliente |
| --- | :---: | :---: | --- |
| Evento de início de buffer ocorrido | 33 | 11 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

Rastreie o movimento do reprodutor para o estado de "buffering".

**Exemplo de corpo da solicitação**

```
{
    playerTime: {
        playhead: 11,
        ts: <timestamp>
    }, eventType:bufferStart
}
```

### Ação 14 - Fim do buffer {#Action-14}

| Ação | Linha do tempo da ação (segundos) | Posição do indicador de reprodução (Segundos) | Solicitação do cliente |
| --- | :---: | :---: | --- |
| O buffering terminou, o aplicativo rastreia a retomada do conteúdo | 36 | 11 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

O buffering termina após 3 segundos; coloque o reprodutor no estado "reproduzindo". Você deve enviar outro evento de rastreamento de reprodução a partir do buffering.  **A`play`chamada após uma`bufferStart`infere uma chamada "bufferEnd" para o back-end,** portanto não há necessidade de um `bufferEnd` evento.

**Exemplo de corpo da solicitação**

```
{
    playerTime: {
        playhead: 11,
        ts: <timestamp>
    },
    eventType:play
}
```

### Ação 15 - Ping {#Action-15}

| Ação | Linha do tempo da ação (segundos) | Posição do indicador de reprodução (Segundos) | Solicitação do cliente |
| --- | :---: | :---: | --- |
| O aplicativo envia o evento de ping | 40 | 15 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

Envie um ping ao back-end a cada 10 segundos.

**Exemplo de corpo da solicitação**

```
{
    playerTime: {
        playhead: 15,
        ts: <timestamp>
    }, eventType:ping
}
```

### Ação 16 - Início do intervalo de anúncios {#Action-16}

| Ação | Linha do tempo da ação (segundos) | Posição do indicador de reprodução (Segundos) | Solicitação do cliente |
| --- | :---: | :---: | --- |
| Rastrear o início do ad break intermediário | 46 | 21 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

Anúncio intermediário de 8 segundos: envie `adBreakStart` .

**Exemplo de corpo da solicitação**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adBreakStart,
    params: {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.podIndex": 1,
        "media.ad.podSecond": 21
    }
}
```

### Ação 17 - Início do anúncio {#Action-17}

| Ação | Linha do tempo da ação (segundos) | Posição do indicador de reprodução (Segundos) | Solicitação do cliente |
| --- | :---: | :---: | --- |
| Rastrear o início do anúncio nº 3 intermediário | 46 | 21 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

Rastreie o anúncio intermediário.

**Exemplo de corpo da solicitação**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adStart, params: {
        "media.ad.podFriendlyName": "ad_pod2",
        "media.ad.name": "Ad 3",
        "media.ad.id": "003",
        "media.ad.length": 8,
        "media.ad.podPosition": 2,
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

### Ação 18 - Ad ping {#Action-18}

| Ação | Linha do tempo da ação (segundos) | Posição do indicador de reprodução (Segundos) | Solicitação do cliente |
| --- | :---: | :---: | --- |
| O aplicativo envia o evento de ping | 50 | 21 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

Envie um ping ao back-end a cada 10 segundos.

**Exemplo de corpo da solicitação**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    }, eventType:ping
}
```

### Ação 19 - Anúncio concluído {#Action-19}

| Ação | Linha do tempo da ação (segundos) | Posição do indicador de reprodução (Segundos) | Solicitação do cliente |
| --- | :---: | :---: | --- |
| Rastrear a conclusão do anúncio nº 1 intermediário | 54 | 21 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

O anúncio intermediário está concluído.

**Exemplo de corpo da solicitação**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adComplete
}
```

### Ação 20 - Conclusão do intervalo de anúncios {#Action-20}

| Ação | Linha do tempo da ação (segundos) | Posição do indicador de reprodução (Segundos) | Solicitação do cliente |
| --- | :---: | :---: | --- |
| Rastrear o ad break intermediário concluído | 54 | 21 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

O ad break está concluído.

**Exemplo de corpo da solicitação**

```
{
    playerTime: {
        playhead: 21,
        ts: <timestamp>
    },
    eventType:adBreakComplete
}
```

### Ação 21 - Ping {#Action-21}

| Ação | Linha do tempo da ação (segundos) | Posição do indicador de reprodução (Segundos) | Solicitação do cliente |
| --- | :---: | :---: | --- |
| O aplicativo envia o evento de ping | 60 | 27 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

Envie um ping ao back-end a cada 10 segundos.

**Exemplo de corpo da solicitação**

```
{
    playerTime: {
        playhead: 27,
        ts: <timestamp>
    },
    eventType:ping
}
```

### Ação 22 - Pausar {#Action-22}

| Ação | Linha do tempo da ação (segundos) | Posição do indicador de reprodução (Segundos) | Solicitação do cliente |
| --- | :---: | :---: | --- |
| O usuário pressionou Pausar | 64 | 31 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

A ação do usuário move o estado de reprodução para "pausado".

**Exemplo de corpo da solicitação**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    },
    eventType:pauseStart
}
```

### Ação 23 - Ping {#Action-23}

| Ação | Linha do tempo da ação (segundos) | Posição do indicador de reprodução (Segundos) | Solicitação do cliente |
| --- | :---: | :---: | --- |
| O aplicativo envia o evento de ping | 70 | 31 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

Envie um ping ao back-end a cada 10 segundos. O reprodutor ainda está no estado "buffering"; o usuário está parado em 20 segundos do conteúdo. Irritado...

**Exemplo de corpo da solicitação**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    }, eventType:ping
}
```

### Ação 24 - Reproduzir {#Action-24}

| Ação | Linha do tempo da ação (segundos) | Posição do indicador de reprodução (Segundos) | Solicitação do cliente |
| --- | :---: | :---: | --- |
| O usuário pressionou Reproduzir para retomar o conteúdo principal | 74 | 31 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

Mova o estado de reprodução para "reproduzindo".  **A`play`chamada após uma`pauseStart`infere uma chamada de "retomada" para o back-end,** portanto não há necessidade de um `resume` evento.

**Exemplo de corpo da solicitação**

```
{
    playerTime: {
        playhead: 31,
        ts: <timestamp>
    }, eventType:play
}
```

### Ação 25 - Ping {#Action-25}

| Ação | Linha do tempo da ação (segundos) | Posição do indicador de reprodução (Segundos) | Solicitação do cliente |
| --- | :---: | :---: | --- |
| O aplicativo envia o evento de ping | 80 | 37 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

Envie um ping ao back-end a cada 10 segundos.

**Exemplo de corpo da solicitação**

```
{
    playerTime: {
        playhead: 37,
        ts: <timestamp>
    }, eventType:ping
}
```

### Ação 26 - Sessão concluída {#Action-26}

| Ação | Linha do tempo da ação (segundos) | Posição do indicador de reprodução (Segundos) | Solicitação do cliente |
| --- | :---: | :---: | --- |
| O usuário termina de assistir ao conteúdo até o final. | 88 | 45 | `/api/v1/sessions/{sid}/events` |

**Detalhes da implementação**

Envie `sessionComplete` ao back-end para indicar que o usuário terminou de assistir todo o conteúdo.

**Exemplo de corpo da solicitação**

```
{
    playerTime: {
        playhead: 45,
        ts: <timestamp>
    }, eventType:sessionComplete
}
```

>[!NOTE]
>
>**Nenhum evento de busca? -** Não há suporte explícito na API da coleção de mídia para eventos `seekStart` ou `seekComplete`. Isso ocorre porque determinados reprodutores geram um grande número desses eventos quando o usuário final movimenta o indicador de reprodução e várias centenas de usuários podem congestionar facilmente a largura de banda da rede de um serviço de back-end. A Adobe resolve o suporte explícito a eventos de busca computando a duração do heartbeat com base no carimbo de data e hora do dispositivo, em vez de na posição do indicador de reprodução.

