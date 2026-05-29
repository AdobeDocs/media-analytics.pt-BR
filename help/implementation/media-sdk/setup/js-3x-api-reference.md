---
title: Referência da API do JavaScript 3.x Media SDK
description: Referência de API para o Media SDK JavaScript 3.x (classes ADB.Media e ADB.MediaConfig).
feature: Streaming Media
role: User, Admin, Developer
exl-id: c3f8a2b5-1d4e-4f9a-8c7b-3a2d1f0e9b6c
source-git-commit: 1022e0851d58db0c9b523ebb7b52d379239a2e07
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 17%

---


# Referência da API do JavaScript 3.x Media SDK

>[!BEGINSHADEBOX]

Esta página aborda o JavaScript 3.x SDK somente para análise. Para a implementação recomendada, consulte [Implementar mídia de transmissão usando o Edge Network](/help/implementation/edge/edge-web-sdk.md).

>[!ENDSHADEBOX]

## ADB.Media

### Métodos estáticos

+++configure

Configura o MediaSDK para rastreamento. Esse método deve ser chamado uma vez antes de criar qualquer instância do rastreador em uma página.

**Sintaxe**

```javascript
ADB.Media.configure(mediaConfig, appMeasurement);
```

| Nome da variável | Tipo | Descrição |
|---|---|---|
| `mediaConfig` | `ADB.MediaConfig` | Configuração de mídia válida |
| `appMeasurement` | objeto | Instância do AppMeasurement |

**Exemplo**

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "company.hb-api.omtrdc.net";
mediaConfig.playerName = "player_name";
mediaConfig.channel = "sample_channel";
mediaConfig.appVersion = "app_version";
mediaConfig.debugLogging = true;
mediaConfig.ssl = true;

ADB.Media.configure(mediaConfig, appMeasurement);
```

+++

+++getInstance

Cria uma instância de mídia para rastrear a sessão de reprodução. Retorna `null`, se chamado, antes da configuração da mídia.

**Sintaxe**

```javascript
ADB.Media.getInstance(trackerConfig)
```

| Nome da variável | Tipo | Obrigatório | Descrição |
| :--- | :--- | :---: | :--- |
| `trackerConfig` | Configuração do rastreador | Não | Objeto de configuração do rastreador. |

**Exemplo**

```javascript
var tracker = ADB.Media.getInstance();
```

Para substituir `channel` ou `playerName` por instância do rastreador, passe os valores de substituição no objeto de configuração do rastreador.

**Exemplo com a configuração do rastreador**

```javascript
const trackerConfig = {
  [Media.TrackerConfig.Channel]: "custom_channel_name",
  [Media.TrackerConfig.PlayerName]: "custom_player_name",
}
this._mediaTracker = Media.getInstance(trackerConfig);
```

+++

+++createMediaObject

Cria um objeto contendo informações de mídia. Retorna o objeto vazio se parâmetros inválidos forem transmitidos.

**Sintaxe**

```javascript
ADB.Media.createMediaObject(name, id, length, streamType, mediaType)
```

| Nome da variável | Tipo | Descrição |
| :--- | :--- | :--- |
| `name` | string | String não vazia que indica o nome da mídia |
| `id` | string | String não vazia que indica um identificador de mídia exclusivo |
| `length` | number | Número positivo que indica a duração da mídia em segundos. Use `0` se o comprimento for desconhecido. |
| `streamType` | string | Tipo de fluxo ou cadeia de caracteres não vazia para indicar o tipo de fluxo de mídia. |
| `mediaType` | Tipo de mídia | Tipo de mídia (áudio ou vídeo) |

**Exemplo**

```javascript
var mediaObject = ADB.Media.createMediaObject("video-name",
                                              "video-id",
                                              60.0,
                                              ADB.Media.StreamType.VOD,
                                              ADB.Media.MediaType.Video);
```

+++

+++createAdBreakObject

Cria um objeto contendo informações adbreak. Retorna o objeto vazio se parâmetros inválidos forem transmitidos.

**Sintaxe**

```javascript
ADB.Media.createAdBreakObject(name, position, startTime);
```

| Nome da variável | Tipo | Descrição |
| :--- | :--- | :--- |
| `name` | string | String não vazia que indica um nome de quebra (antes da exibição, durante a exibição e após a exibição) |
| `position` | number | A posição do número do ad break no conteúdo, começando com 1 |
| `startTime` | number | Valor do indicador de reprodução no início do ad break. |

**Exemplo**

```javascript
var adbreakObject = ADB.Media.createAdBreakObject("midroll", 2, 30.0);
```

+++

+++createAdObject

Cria um objeto contendo informações de anúncios. Retorna o objeto vazio se parâmetros inválidos forem transmitidos.

**Sintaxe**

```javascript
ADB.Media.createAdObject(name, id, position, length);
```

| Nome da variável | Tipo | Descrição |
| :--- | :--- | :--- |
| `name` | string | String não vazia que indica o nome do anúncio |
| `id` | string | String não vazia que indica id do anúncio |
| `position` | number | A posição do número do anúncio dentro do adbreak, começando com 1 |
| `length` | number | Número positivo que indica a duração do anúncio |

**Exemplo**

```javascript
var adObject = ADB.Media.createAdObject("ad-name", "ad-id", 1, 15.0)
```

+++

+++createChapterObject

Cria um objeto contendo informações do capítulo. Retorna o objeto vazio se parâmetros inválidos forem transmitidos.

**Sintaxe**

```javascript
ADB.Media.createChapterObject(name, position, length, startTime)
```

| Nome da variável | Tipo | Descrição |
| :--- | :--- | :--- |
| `name` | string | String não vazia que indica o nome do capítulo |
| `position` | number | A posição do capítulo no conteúdo, começando com 1 |
| `length` | number | Número positivo que indica o comprimento do capítulo |
| `startTime` | number | Valor do indicador de reprodução no início do capítulo |

**Exemplo**

```javascript
var chapterObject = ADB.Media.createChapterObject("name", 1, 30.0, 0)
```

+++

+++createStateObject

Cria um objeto contendo informações de estado. Retorna o objeto vazio se parâmetros inválidos forem transmitidos.

**Sintaxe**

```javascript
ADB.Media.createStateObject(name)
```

| Nome da variável | Tipo | Descrição |
| :--- | :--- | :--- |
| `name` | string | Estado do player ou string não vazia que indica o nome do estado |

**Exemplo**

```javascript
var stateObject = ADB.Media.createStateObject("customstate");
```

+++

+++createQoEObject

Cria um objeto contendo informações de QoE. Retorna o objeto vazio se parâmetros inválidos forem transmitidos.

**Sintaxe**

```javascript
ADB.Media.createQoEObject(bitrate, startupTime, fps, droppedFrames)
```

| Nome da variável | Tipo | Descrição |
| :--- | :--- | :--- |
| `bitrate` | número | Número positivo que indica a taxa de bits atual (0 se desconhecido) |
| `startupTime` | number | Número positivo que indica o tempo de inicialização (0 se desconhecido) |
| `fps` | number | Número positivo que indica fps atuais (0 se desconhecido) |
| `droppedFrames` | number | Número positivo que indica o número de quadros ignorados (0 se desconhecido) |

**Exemplo**

```javascript
qoeObject = ADB.Media.createQoEObject(10000000, 2, 23, 10);
```

+++

+++version

Retorna a versão do MediaSDK.

**Sintaxe**

```javascript
ADB.Media.version
```

**Exemplo**

```javascript
console.log(ADB.Media.version);
```

+++

### Métodos de instância

+++trackSessionStart

Rastreie a intenção de iniciar a reprodução. Isso inicia uma sessão de rastreamento na instância do rastreador de mídia. Consulte também Retomada de mídia.

**Sintaxe**

```javascript
ADB.Media.trackSessionStart(mediaObject, contextData);
```

| Nome da variável | Descrição | Obrigatório |
| :--- | :--- | :---: |
| `mediaObject` | Informações de mídia criadas usando o método `createMediaObject`. | Sim |
| `contextData` | Dados de contexto de mídia opcionais. Para chaves de metadados padrão, use constantes de vídeo padrão ou constantes de áudio padrão. | Não |

**Exemplo**

```javascript
var mediaObject = ADB.Media.createMediaObject("media-name", "media-id", 60, ADB.Media.StreamType.VOD, ADB.Media.MediaType.Video);

var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Episode] = "Sample Episode";
contextData[ADB.Media.VideoMetadataKeys.Show] = "Sample Show";
contextData["isUserLoggedIn"] = "false";
contextData["tvStation"] = "Sample TV Station";

tracker.trackSessionStart(mediaObject, contextData);
```

+++

+++trackPlay

Rastrear a reprodução ou retomar a mídia após uma pausa anterior.

**Sintaxe**

```javascript
ADB.Media.trackPlay();
```

**Exemplo**

```javascript
tracker.trackPlay();
```

+++

+++trackPause

Rastrear pausa de mídia.

**Sintaxe**

```javascript
ADB.Media.trackPause();
```

**Exemplo**

```javascript
tracker.trackPause();
```

+++

+++trackComplete

Rastreamento de mídia concluído. Chame esse método somente quando a mídia tiver sido completamente visualizada.

**Sintaxe**

```javascript
ADB.Media.trackComplete();
```

**Exemplo**

```javascript
tracker.trackComplete();
```

+++

+++trackSessionEnd

Rastrear o final de uma sessão de exibição. Chame esse método mesmo se o usuário não visualizar a mídia até o fim.

**Sintaxe**

```javascript
ADB.Media.trackSessionEnd();
```

**Exemplo**

```javascript
tracker.trackSessionEnd();
```

+++

+++trackError

Rastrear um erro na reprodução de mídia.

**Sintaxe**

```javascript
ADB.Media.trackError(errorId);
```

| Nome da variável | Descrição | Obrigatório |
| :--- | :--- | :---: |
| `errorId` | Cadeia de caracteres não vazia que contém informações de erro | Sim |

**Exemplo**

```javascript
tracker.trackError("errorId");
```

+++

+++trackEvent

Método para rastrear eventos de mídia.

| Nome da variável | Descrição |
| :--- | :--- |
| `event` | Evento de mídia |
| `info` | Para o evento `AdBreakStart`, as informações de adbreak são criadas usando o método `createAdBreakObject`. Para o evento `AdStart`, as informações do anúncio são criadas com o método `createAdObject`. Para o evento `ChapterStart`, as informações do capítulo são criadas usando o método `createChapterObject`. Para eventos `StateStart` e `StateEnd`, as informações de estado são criadas usando o método `createStateObject`. Isso não é necessário para outros eventos. |
| `contextData` | Dados de contexto opcionais podem ser fornecidos para eventos `AdStart` e `ChapterStart`. Isso não é necessário para outros eventos. |

**Sintaxe**

```javascript
ADB.Media.trackEvent(event, info, contextData);
```

**Exemplos**

**Rastreamento de AdBreaks**

```javascript
// AdBreakStart
  var adBreakObject = ADB.Media.createAdBreakObject("preroll", 1, 0)
  tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakObject);

// AdBreakComplete
  tracker.trackEvent(ADB.Media.Event.AdBreakComplete);
```

**Rastreamento de anúncios**

```javascript
// AdStart
  var adObject = ADB.Media.createAdObject("ad-name", "ad-id", 1, 15.0);

  var adMetadata = {};
  // Standard metadata keys provided by adobe.
  adMetadata[ADB.Media.AdMetadataKeys.Advertiser]  ="Sample Advertiser";
  adMetadata[ADB.Media.AdMetadataKeys.CampaignId] = "Sample Campaign";
  // Custom metadata keys
  adMetadata["affiliate"] = "Sample affiliate";

  tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);

// AdComplete
  tracker.trackEvent(ADB.Media.Event.AdComplete);

// AdSkip
  tracker.trackEvent(ADB.Media.Event.AdSkip);
```

**Rastreamento de capítulos**

```javascript
// ChapterStart
  var chapterObject = ADB.Media.createChapterObject("chapter-name", 1, 60.0, 15.0);

  var chapterMetadata = {};
  chapterMetadata["segmentType"] = "Sample segment type";

  tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterObject, chapterMetadata);

// ChapterComplete
  tracker.trackEvent(ADB.Media.Event.ChapterComplete);

// ChapterSkip
  tracker.trackEvent(ADB.Media.Event.ChapterSkip);
```

**Rastreando estados**

```javascript
// StateStart (ex: Mute is switched on)
  var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
  tracker.trackEvent(ADB.Media.Event.StateStart, stateObject);

// StateEnd (ex: Mute is switched off)
  tracker.trackEvent(ADB.Media.Event.StateEnd, stateObject);
```

**Rastreamento de eventos de reprodução**

```javascript
// BufferStart
  tracker.trackEvent(ADB.Media.Event.BufferStart);

// BufferComplete
  tracker.trackEvent(ADB.Media.Event.BufferComplete);

// SeekStart
  tracker.trackEvent(ADB.Media.Event.SeekStart);

// SeekComplete
  tracker.trackEvent(ADB.Media.Event.SeekComplete);
```

**Rastreamento de alterações da taxa de bits**

```javascript
// If the new bitrate value is available provide it to the tracker.
  var qoeObject = ADB.Media.createQoEObject(1000000, 2.4, 25, 10);
  tracker.updateQoEObject(qoeObject);

// Bitrate change
  tracker.trackEvent(ADB.Media.Event.BitrateChange);
```

+++

+++updatePlayhead

Forneça o indicador de reprodução de mídia atual ao rastreador de mídia. Para obter um rastreamento preciso, chame esse método sempre que o indicador de reprodução for alterado durante a reprodução.

**Sintaxe**

```javascript
ADB.Media.updatePlayhead(time);
```

| Nome da variável | Descrição |
| :--- | :--- |
| `time` | Indicador de reprodução atual em segundos. Para vídeos sob demanda (VOD), o valor é especificado em segundos a partir do início do item de mídia. Para transmissões ao vivo, se o player não fornecer informações sobre a duração do conteúdo, o valor pode ser especificado como o número de segundos desde a meia-noite UTC daquele dia. Observação: ao usar marcadores de progresso, a duração do conteúdo é necessária e o indicador de reprodução precisa ser atualizado para o número de segundos desde o início do item de mídia, começando com 0. |

**Exemplo**

```javascript
tracker.updatePlayhead(13.3);

// For live streams
var UTCTimeInSeconds = Math.floor(Date.now() / 1000)
var timeFromMidnightInSecond = UTCTimeInSeconds % 86400

tracker.updatePlayhead(timeFromMidnightInSecond);
```

+++

+++updateQoEObject

Fornece informações de QoE atuais ao rastreador de mídia. Para obter um rastreamento preciso, chame esse método várias vezes quando o reprodutor de mídia fornecer as informações de QoE atualizadas.

**Sintaxe**

```javascript
ADB.Media.updateQoEObject(qoeObject);
```

| Nome da variável | Descrição |
| :--- | :--- |
| `qoeObject` | Informações de QoE atuais que foram criadas com o método `createQoEObject`. |

**Exemplo**

```javascript
var qoeObject = ADB.Media.createQoEObject(1000000, 2.4, 25, 10);
tracker.updateQoEObject(qoeObject);
```

+++

+++destruir

Destrói a instância do rastreador.

**Sintaxe**

```javascript
ADB.Media.destroy();
```

**Exemplo**

```javascript
tracker.destroy();
```

+++

### Constantes

+++Configuração do rastreador

Define as chaves de configuração que podem ser definidas por instância do rastreador.

```javascript
ADB.Media.TrackerConfig = {
  Channel: "media.channel",
  PlayerName: "media.playerName"
}
```

+++

+++Tipo de mídia

Define o tipo de mídia que está sendo rastreada no momento.

```javascript
ADB.Media.MediaType = {
  Video: "video",
  Audio: "audio"
}
```

+++

+++Tipo de transmissão

Define o tipo de fluxo do conteúdo que está sendo rastreado no momento.

```javascript
ADB.Media.StreamType = {
  VOD: "vod",
  Live: "live",
  Linear: "linear",
  Podcast: "podcast",
  Audiobook: "audiobook",
  AOD: "aod"
}
```

+++

+++Chaves de metadados padrão

`ADB.Media.VideoMetadataKeys`, `ADB.Media.AudioMetadataKeys` e `ADB.Media.AdMetadataKeys` fornecem as cadeias de caracteres de chave de dados de contexto para metadados padrão. Para obter a lista completa de chaves e suas variáveis de relatório correspondentes, consulte a [Referência da variável de metadados padrão](/help/implementation/variables/standard-metadata/show.md).

+++

+++Eventos de mídia

Define o tipo de um evento de rastreamento.

```javascript
ADB.Media.Event = {
  AdBreakStart: "adBreakStart",
  AdBreakComplete: "adBreakComplete",
  AdStart: "adStart",
  AdComplete: "adComplete",
  AdSkip: "adSkip",
  ChapterStart: "chapterStart",
  ChapterComplete: "chapterComplete",
  ChapterSkip: "chapterSkip",
  SeekStart: "seekStart",
  SeekComplete: "seekComplete",
  BufferStart: "bufferStart",
  BufferComplete: "bufferComplete",
  BitrateChange: "bitrateChange",
  StateStart: "stateStart",
  StateEnd: "stateEnd"
}
```

+++

+++Estados do player

Define valores padrão para rastrear o estado do player.

```javascript
ADB.Media.PlayerState = {
  FullScreen: "fullScreen",
  ClosedCaption: "closedCaptioning",
  Mute: "mute",
  PictureInPicture: "pictureInPicture",
  InFocus: "inFocus"
}
```

+++

+++Retomada de mídia

Constante para indicar que a sessão de rastreamento atual está retomando uma sessão fechada anteriormente. Essas informações devem ser fornecidas ao iniciar uma sessão de rastreamento.

**Sintaxe**

```javascript
ADB.Media.MediaObjectKey = {
  MediaResumed: "resumed"
}
```

**Exemplo**

```javascript
var mediaObject = ADB.Media.createMediaObject("media-name", "media-id", 60, ADB.Media.StreamType.VOD, ADB.Media.MediaType.Video);

mediaObject[ADB.Media.MediaObjectKey.MediaResumed] = true;

tracker.trackSessionStart(mediaObject);
```

+++

## ADB.MediaConfig

| Chave | Obrigatório | Descrição |
| :--- | :--- | :--- |
| `trackingServer` | Sim | Digite o nome do servidor de API da coleção de mídia para o qual os dados de rastreamento de mídia baixados devem ser enviados. Entre em contato com o representante de conta da Adobe para receber essas informações. |
| `channel` | Não | Propriedade do nome do canal |
| `playerName` | Não | Nome do reprodutor de mídia em uso |
| `appVersion` | Não | Digite a versão do aplicativo do reprodutor de mídia/SDK |
| `debugLogging` | Não | Habilita ou desabilita logs do Media SDK (Valor padrão: `false`) |
| `ssl` | Não | Envia pings por SSL (Valor padrão: `true`) |
