---
title: Esquema de relatório XDM
description: Saiba quais eventos de API do Media Edge geram eventos de experiência no Adobe Experience Platform e como validar sua implementação usando o esquema XDM do mediaReporting.
feature: Streaming Media
role: User, Admin, Developer
exl-id: c3a4d31b-8f9e-4d7a-9b2e-1a5f0e8c7d39
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 267532dfbe6dc3f7bcff0991536ae3baf6eff053
workflow-type: tm+mt
source-wordcount: 763
ht-degree: 4%

---


# Esquema de relatório XDM

Ao enviar eventos de rastreamento de mídia usando o Adobe Experience Platform Edge Network, o back-end do Media Analytics processa esses eventos e grava eventos de experiência computados em conjuntos de dados da plataforma. Entender quais eventos atingem a Platform e o que o back-end calcula para você ajuda a validar sua implementação e criar relatórios precisos no Customer Journey Analytics ou no Adobe Analytics.

Dois esquemas XDM distintos são usados em partes diferentes do pipeline de coleta e relatórios:

| Esquema | Namespace | Direção | Propósito |
|---|---|---|---|
| Coleção de mídia | `xdm.mediaCollection` | Cliente → Adobe | O que o reprodutor envia para cada evento de rastreamento. Usado por [variáveis](/help/implementation/variables/). |
| Relatórios de mídia | `xdm.mediaReporting` | Adobe → Plataforma | O que o back-end grava nos conjuntos de dados após o processamento. Usado por [dimensões](/help/reporting/dimensions/overview.md) e [métricas](/help/reporting/metrics/overview.md). |

Os campos presentes em `mediaReporting`, mas ausentes na carga `mediaCollection`, são derivados da sequência completa de eventos em uma sessão. Esses campos nunca são enviados; o Adobe os gera.

## Eventos que gravam em conjuntos de dados da plataforma

Dos 12 tipos de evento rastreáveis, apenas cinco geram gravações de Evento de experiência individuais em conjuntos de dados:

| Tipo de evento | Incluído nos conjuntos de dados | Notas |
|---|---|---|
| [Início da sessão](/help/implementation/events/session/session-start.md) | Sim | Gravado quando a sessão é inicializada |
| [Início do anúncio](/help/implementation/events/ads/ad-start.md) | Sim | Escrito quando um anúncio individual começa |
| [Anúncio concluído](/help/implementation/events/ads/ad-complete.md) | Sim | Escrito quando um anúncio é reproduzido até a conclusão |
| [Capítulo concluído](/help/implementation/events/chapters/chapter-complete.md) | Sim | Escrito quando um capítulo é reproduzido até a conclusão |
| [Sessão concluída](/help/implementation/events/session/session-complete.md) | Sim | Gravado quando a sessão termina; conjunto de campos calculados mais avançado |
| [Reproduzir](/help/implementation/events/playback/play.md) | Não | Usado para computar `timePlayed` |
| [Início da pausa](/help/implementation/events/playback/pause-start.md) | Não | Usado para computar `pauseCount` e `pauseTime` |
| [Ping](/help/implementation/events/playback/ping.md) | Não | Heartbeat; usado para detectar a inatividade da sessão |
| [Início do buffer](/help/implementation/events/playback/buffer-start.md) | Não | Usado para calcular métricas de buffer de QoE |
| [Alteração na taxa de bits](/help/implementation/events/playback/bitrate-change.md) | Não | Usado para calcular métricas de taxa de bits de QoE |
| [Início do estado](/help/implementation/events/player-state/state-start.md) | Não | Usado para calcular métricas do estado do player |
| [Erro](/help/implementation/events/error.md) | Não | Usado para computar `errorCount` em QoE |

## Campos calculados de backend

Os campos a seguir aparecem nas cargas de `mediaReporting`, mas nunca fazem parte da carga da coleção. O back-end os deriva da sequência completa de eventos.

**Nível de sessão** (aparecer em `sessionComplete`):

| Campo | Descrição |
|---|---|
| `xdm.mediaReporting.sessionDetails.timePlayed` | Total de segundos do conteúdo principal reproduzido, excluindo anúncios |
| `xdm.mediaReporting.sessionDetails.totalTimePlayed` | Total de segundos decorridos, incluindo anúncios |
| `xdm.mediaReporting.sessionDetails.uniqueTimePlayed` | Segundos desduplicados — intervalos exibidos mais de uma vez são contados apenas uma vez |
| `xdm.mediaReporting.sessionDetails.averageMinuteAudience` | `timePlayed` dividido pela duração do conteúdo |
| `xdm.mediaReporting.sessionDetails.estimatedStreams` | Fluxos simultâneos estimados |
| `xdm.mediaReporting.sessionDetails.adCount` | Número de anúncios iniciados |
| `xdm.mediaReporting.sessionDetails.chapterCount` | Número de capítulos iniciados |
| `xdm.mediaReporting.sessionDetails.pauseCount` / `xdm.mediaReporting.sessionDetails.pauseTime` | Frequência de pausa e duração total da pausa |
| `xdm.mediaReporting.sessionDetails.hasProgress10` ... `xdm.mediaReporting.sessionDetails.hasProgress95` | Sinalizadores de marcos de progresso (10%, 25%, 50%, 75%, 95%) |
| `xdm.mediaReporting.sessionDetails.hasSegmentView` | Se pelo menos um quadro do conteúdo foi exibido |
| `xdm.mediaReporting.sessionDetails.isCompleted` / `xdm.mediaReporting.sessionDetails.isPlayed` | Sinalizadores de conclusão e início |
| `xdm.mediaReporting.sessionDetails.secondsSinceLastCall` | Tempo entre o último ping e o fechamento da sessão |
| `xdm.mediaReporting.sessionDetails.segment` | Colchete de segmento de conteúdo (por exemplo, `[0-1]`) |

**Nível de anúncio** (aparecer em `adComplete`):

| Campo | Descrição |
|---|---|
| `xdm.mediaReporting.advertisingDetails.timePlayed` | Segundos do conteúdo do anúncio reproduzido |
| `xdm.mediaReporting.advertisingDetails.isCompleted` | Se o anúncio foi reproduzido até a conclusão |

**Nível de capítulo** (aparecer em `chapterComplete`):

| Campo | Descrição |
|---|---|
| `xdm.mediaReporting.chapterDetails.timePlayed` | Segundos do conteúdo do capítulo reproduzido |
| `xdm.mediaReporting.chapterDetails.isCompleted` | Se o capítulo foi reproduzido até a conclusão |
| `xdm.mediaReporting.chapterDetails.isStarted` | Se o capítulo foi iniciado |

**QoE** (agregado em `sessionComplete`):

| Campo | Descrição |
|---|---|
| `xdm.mediaReporting.qoeDataDetails.bitrateAverage` | Taxa média de bits na sessão |
| `xdm.mediaReporting.qoeDataDetails.bitrateAverageBucket` | Intervalo da taxa média de bits |
| `xdm.mediaReporting.qoeDataDetails.bitrateChangeCount` | Número de alterações da taxa de bits |
| `xdm.mediaReporting.qoeDataDetails.errorCount` | Número de erros |
| `xdm.mediaReporting.qoeDataDetails.droppedFrames` | Total de quadros soltos |
| `xdm.mediaReporting.qoeDataDetails.playerSdkErrors` | Matriz de códigos de erro do player |
| `xdm.mediaReporting.qoeDataDetails.hasErrorImpactedStreams` | Se ocorreu algum erro |
| `xdm.mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams` | Se ocorreram quadros soltos |
| `xdm.mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams` | Se ocorreram alterações na taxa de bits |

## Conteúdo baixado

Para sessões rastreadas usando o [ponto de extremidade baixado](/help/use-cases/track-downloaded-content.md), o back-end define automaticamente `xdm.mediaReporting.sessionDetails.isDownloaded` como `true` no evento de relatório `sessionStart`. Todos os outros eventos de relatórios para sessões baixadas seguem o mesmo esquema das sessões ativas. Use esse campo no CJA ou Adobe Analytics para filtrar ou segmentar a reprodução baixada.

Consulte [Ponto de extremidade baixado](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/downloaded/) na referência da API do Media Edge para obter detalhes sobre a implementação da coleção.

## Validar a sua implementação

Depois de enviar eventos por meio da API do Media Edge, verifique se os dados foram inseridos corretamente usando um dos seguintes métodos:

**visualização do conjunto de dados do Adobe Experience Platform**

1. No [CX Enterprise](https://experience.adobe.com), navegue até **[!UICONTROL Conjuntos de Dados]** e selecione seu conjunto de dados de mídia de streaming.
2. Selecione **[!UICONTROL Visualizar conjunto de dados]** para ver os Eventos de Experiência assimilados mais recentemente.
3. Confirme se `eventType` valores como `media.sessionStart` e `media.sessionComplete` aparecem com campos `mediaReporting` preenchidos.

**inspeção do conjunto de dados do Customer Journey Analytics**

1. No CJA, abra a conexão associada ao conjunto de dados de mídia de transmissão.
2. Selecione **Adicionar conjuntos de dados** e inspecione o esquema para confirmar se os campos `mediaReporting` estão mapeados para as dimensões e métricas esperadas.

**Regras de processamento do Adobe Analytics (se estiver usando o destino do Analytics)**

Para conjuntos de relatórios do Adobe Analytics que recebem dados por meio do conector de origem do Analytics, você pode usar Regras de processamento para mapear variáveis de dados de contexto do `mediaReporting` para props ou eVars personalizadas. O sinalizador `isDownloaded` está disponível como `a.media.downloaded`.

## Exemplos de carga XDM

Os exemplos a seguir mostram a estrutura XDM `mediaReporting` completa para cada evento de relatório conforme é gravado nos conjuntos de dados da plataforma. A propriedade `_{tenantName}` representa o namespace de locatário de sua organização para quaisquer campos personalizados.

+++media.sessionStart

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "mediaReporting": {
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "isViewed": true,
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "hasResume": false,
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.sessionStart",
    "_id": "0[...]0",
    "timestamp": "YYYY-11-20T12:43:35Z"
  }
}
```

+++

+++media.adStart

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "environment": {
      "browserDetails": {},
      "ipV4": "130.248.81.10"
    },
    "mediaReporting": {
      "advertisingDetails": {
        "advertiser": "Adobe Marketing",
        "podPosition": 1,
        "placementID": "placementID",
        "example": "https://example.com",
        "playerName": "HTML5 player",
        "campaignID": "Adobe Analytics",
        "name": "/uri-reference/001",
        "length": 10,
        "siteID": "siteID",
        "isStarted": true,
        "creativeID": "creativeID",
        "friendlyName": "Ad 1"
      },
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "pev3": "videoAd",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      },
      "advertisingPodDetails": {
        "offset": 0,
        "ID": "3d594614f445f6b00014e9b77730b833_1",
        "friendlyName": "Mid-ad"
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.adStart",
    "_id": "d[...]0",
    "timestamp": "YYYY-11-20T12:43:56Z"
  }
}
```

+++

+++media.adComplete

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "mediaReporting": {
      "advertisingDetails": {
        "advertiser": "Adobe Marketing",
        "podPosition": 1,
        "placementID": "placementID",
        "example": "https://example.com",
        "playerName": "HTML5 player",
        "campaignID": "Adobe Analytics",
        "length": 10,
        "creativeID": "creativeID",
        "timePlayed": 7,
        "name": "/uri-reference/001",
        "siteID": "siteID",
        "friendlyName": "Ad 1",
        "isCompleted": true
      },
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "pev3": "videoAd",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      },
      "advertisingPodDetails": {
        "offset": 0,
        "ID": "3d594614f445f6b00014e9b77730b833_1",
        "friendlyName": "Mid-ad"
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.adComplete",
    "_id": "f[...]0",
    "timestamp": "YYYY-11-20T12:44:03Z"
  }
}
```

+++

+++media.chapterComplete

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2",
      "customTest": "myCustomValue1"
    },
    "environment": {
      "browserDetails": {},
      "ipV4": "130.248.81.10"
    },
    "mediaReporting": {
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "artist": "test-artist",
        "pev3": "video",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "episode": "4933",
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "season": "1521",
        "showType": "sitcom",
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "friendlyName": "test-friendly-name",
        "playerName": "HTML5 player",
        "album": "test-album",
        "author": "test-author",
        "length": 100,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "feed": "sourceFeed",
        "assetID": "/uri-reference",
        "name": "test-name",
        "publisher": "test-media-publisher",
        "firstDigitalDate": "releaseDate"
      },
      "chapterDetails": {
        "timePlayed": 10,
        "offset": 0,
        "length": 10,
        "index": 1,
        "ID": "3d594614f445f6b00014e9b77730b833_1",
        "isStarted": true,
        "friendlyName": "Chapter 1",
        "isCompleted": true
      }
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.chapterComplete",
    "_id": "a[...]0",
    "timestamp": "YYYY-11-20T12:44:24Z"
  }
}
```

+++

+++media.sessionComplete

```json
{
  "xdm": {
    "_{tenantName}": {
      "customField1": "c1",
      "customField2": "c2"
    },
    "environment": {
      "browserDetails": {},
      "ipV4": "130.248.81.10"
    },
    "mediaReporting": {
      "qoeDataDetails": {
        "playerSdkErrors": ["test-buffer-start"],
        "bitrateAverageBucket": "0-99",
        "bitrateChangeCount": 1,
        "droppedFrames": 30,
        "hasErrorImpactedStreams": true,
        "hasBitrateChangeImpactedStreams": true,
        "hasDroppedFrameImpactedStreams": true,
        "bitrateAverage": 35,
        "timeToStart": 1,
        "errorCount": 1
      },
      "sessionDetails": {
        "adLoad": "adLoadType",
        "appVersion": "sdk-1.0",
        "hasProgress10": true,
        "pev3": "video",
        "channel": "broadcastChannel",
        "rating": "4.8/5",
        "episode": "4933",
        "pauseTime": 3,
        "streamType": "video",
        "pccr": true,
        "authorized": "true",
        "segment": "[0-1]",
        "season": "1521",
        "showType": "sitcom",
        "pauseCount": 1,
        "ID": "cd7b[...]6f",
        "contentType": "VOD",
        "uniqueTimePlayed": 47,
        "totalTimePlayed": 55,
        "author": "test-author",
        "hasProgress25": true,
        "feed": "sourceFeed",
        "timePlayed": 48,
        "name": "test-name",
        "publisher": "test-media-publisher",
        "hasPauseImpactedStreams": true,
        "averageMinuteAudience": 0.48,
        "artist": "test-artist",
        "show": "test-name Series",
        "genreList": ["Comedy"],
        "originator": "Tokala Clementine",
        "network": "test-network",
        "firstAirDate": "firstAirDate",
        "hasSegmentView": true,
        "streamFormat": "streamFormat",
        "genre": "Comedy",
        "station": "test-station",
        "friendlyName": "test-friendly-name",
        "isCompleted": true,
        "playerName": "HTML5 player",
        "album": "test-album",
        "chapterCount": 1,
        "length": 100,
        "adCount": 1,
        "dayPart": "dayPart",
        "label": "test-label",
        "mvpd": "test-mvpd",
        "secondsSinceLastCall": 51,
        "assetID": "/uri-reference",
        "isPlayed": true,
        "estimatedStreams": 1,
        "firstDigitalDate": "releaseDate"
      },
      "states": [
        {
          "isSet": true,
          "name": "mute",
          "count": 1,
          "time": 3
        },
        {
          "isSet": true,
          "name": "pictureInPicture",
          "count": 1,
          "time": 3
        }
      ]
    },
    "implementationDetails": {
      "environment": "server",
      "name": "https://ns.adobe.com/experience/edge",
      "version": "0.0.0"
    },
    "identityMap": {
      "ECID": [
        {
          "id": "5191[...]21",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    },
    "eventType": "media.sessionComplete",
    "_id": "a[...]0",
    "timestamp": "YYYY-11-20T12:44:40Z"
  }
}
```

+++

+++media.sessionStart (conteúdo baixado)

As sessões rastreadas com o [ponto de extremidade baixado](/help/use-cases/track-downloaded-content.md) seguem o mesmo esquema de relatório com uma diferença de chave: `xdm.mediaReporting.sessionDetails.isDownloaded` está definido como `true` no evento de relatório `sessionStart`. Todos os outros tipos de evento são idênticos aos exemplos de conteúdo ao vivo acima.

```json
{
  "xdm": {
    "mediaReporting": {
      "customMetadata": [
        {
          "name": "customData",
          "value": "example"
        }
      ],
      "playhead": 0,
      "sessionDetails": {
        "ID": "d8a25708a6b0be83975e32e2f422105ed62f51ff67e6d82d898657534ab9244f",
        "channel": "channel",
        "contentType": "VOD",
        "length": 100,
        "name": "123456789",
        "playerName": "playerName",
        "isDownloaded": true
      }
    },
    "eventType": "media.sessionStart",
    "timestamp": "YYYY-09-26T15:52:24Z",
    "identityMap": {
      "ECID": [
        {
          "id": "51910389753901685456014889838591030721"
        }
      ]
    },
    "implementationDetails": {
      "version": "0.0.1",
      "environment": "browser",
      "name": "https://ns.adobe.com/experience/edge"
    }
  }
}
```

+++
