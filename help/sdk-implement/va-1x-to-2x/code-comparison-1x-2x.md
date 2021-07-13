---
title: Comparação de código v1.x para v2.x
description: Saiba a diferença entre o código nas versões 1.x e 2.x do SDK do Media.
uuid: 9f0a1660-2100-446d-ab75-afdf966478b3
exl-id: c2324c6a-329f-44e2-bea0-9d43ef9c6ef7
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 93%

---

# Comparação de código: 1.x para 2.x {#code-comparison-x-to-x}

Todos os parâmetros de configuração e APIs de rastreamento foram consolidados nas classes `MediaHeartbeats` e `MediaHeartbeatConfig`.

**Alterações na configuração da API:**

* `AdobeHeartbeatPluginConfig.sdk` - Renomeado para `MediaConfig.appVersion`
* `MediaHeartbeatConfig.playerName` - Agora definido por meio de `MediaHeartbeatConfig` em vez de `VideoPlayerPluginDelegate`
* (Somente para JavaScript): a instância `AppMeasurement` - Agora enviada através do construtor `MediaHeartbeat`.

**Alterações nas configurações das propriedades:**

* `sdk` - Renomeado para `appVersion`
* `publisher` - Removido; a ID da Organização da Experience Cloud é usada em vez de um publicador
* `quiteMode` - Removido

**Links para reprodutores de amostra 1.x e 2.x:**

* [Exemplo de reprodutor 1.x ](https://github.com/Adobe-Marketing-Cloud/video-heartbeat/blob/master/sdks/js/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L58)
* [Exemplo de reprodutor 2.x ](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/sdks/js/2.x/samples/BasicPlayerSample/script/app/analytics/video.analytics.provider.js#L47)

As seções a seguir fornecem comparações de código entre o 1.x e o 2.x, abordando a Inicialização, a reprodução principal, a reprodução de anúncio, a reprodução de capítulo e alguns eventos adicionais.

## Comparação de código do VHL: INICIALIZAÇÃO

### Inicialização do objeto

| 1.x API | 2.x API |
| --- | --- |
| `Heartbeat()` | `MediaHeartbeat()` |
| `VideoPlayerPlugin()` | `MediaHeartbeatConfig()` |
| `AdobeAnalyticsPlugin()` |  |
| `HeartbeatPlugin()` |  |

#### Inicialização do plug-in do reprodutor de vídeo (1.x) {#plugin-init-1.x}

```js
this._playerPlugin = new VideoPlayerPlugin( new SampleVideoPlayerPluginDelegate(this._player));
var playerPluginConfig = new VideoPlayerPluginConfig();
playerPluginConfig.debugLogging = true;

// Set up the AppMeasurement plugin 
this._aaPlugin = new AdobeAnalyticsPlugin( appMeasurement, new SampleAdobeAnalyticsPluginDelegate());
var aaPluginConfig = new AdobeAnalyticsPluginConfig();
aaPluginConfig.channel = Configuration.HEARTBEAT.CHANNEL;
aaPluginConfig.debuglogging = true;
this._aaPlugin.configure(aaPluginConfig);

// Set up the AdobeHeartbeat plugin 
var ahPlugin = new AdobeHeartbeatPlugin( new SampleAdobeHeartbeatPluginDelegate());
var ahPluginConfig = new AdobeHeartbeatPluginConfig( configuration.HEARTBEAT.TRACKING_SERVER, configuration.HEARTBEAT.PUBLISHER);
ahPluginConfig.ovp = configuration.HEARTBEAT.OVP;
ahPluginConfig.sdk = configuration.HEARTBEAT.SDK;
ahPluginConfig.debugLogging = true;
ahPlugin.configure(ahPluginConfig);
var plugins = [this._playerPlugin, this._aaPlugin, ahPlugin];

// Set up and configure the heartbeat library this._heartbeat = new Heartbeat(new SampleHeartbeatDelegate(), plugins);
var configData = new HeartbeatConfig();
configData.debugLogging = true;
this._heartbeat.configure(configData);
```

#### Inicialização do Media Heartbeat (2.x) {#mh-init-2.x}

```js
var mediaConfig = new MediaHeartbeatConfig();
mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER;
mediaConfig.playerName = Configuration.PLAYER.NAME;
mediaConfig.debugLogging = true;
mediaConfig.channel = Configuration.HEARTBEAT.CHANNEL;
mediaConfig.ssl = false;
mediaConfig.ovp = Configuration.HEARTBEAT.OVP;
mediaConfig.appVersion = Configuration.HEARTBEAT.SDK;
this._mediaHeartbeat = new MediaHeartbeat( new SampleMediaHeartbeatDelegate(this._player), mediaConfig, appMeasurement);
```

### Representantes

| API 1.x | API 2.x |
| --- | --- |
| `VideoPlayerPluginDelegate()` | `MediaHeartbeatDelegate()` |
| `VideoPlayerPluginDelegate().getVideoInfo` | `MediaHeartbeatDelegate().getCurrentPlaybackTime` |
| `VideoPlayerPluginDelegate().getAdBreakInfo` | `MediaHeartbeatDelegate().getQoSObject` |
| `VideoPlayerPluginDelegate().getAdInfo` |  |
| `VideoPlayerPluginDelegate().getChapterInfo` |  |
| `VideoPlayerPluginDelegate().getQoSInfo` |  |
| `VideoPlayerPluginDelegate().get.onError` |  |
| `AdobeAnalyticsPluginDelegate()` |  |

#### VideoPlayerPluginDelegate (1.x) {#player-plugin-delegate-1.x}

```js
$.extend(SampleVideoPlayerPluginDelegate.prototype, VideoPlayerPluginDelegate.prototype);

function SampleVideoPlayerPluginDelegate(player) { 
    this._player = player;
} 

SampleVideoPlayerPluginDelegate.prototype.getVideoInfo = function() { 
    return this._player.getVideoInfo();
};

SampleVideoPlayerPluginDelegate.prototype.getAdBreakInfo = function() { 
    return this._player.getAdBreakInfo();
};

SampleVideoPlayerPluginDelegate.prototype.getAdInfo = function() { 
    return this._player.getAdInfo();
};

SampleVideoPlayerPluginDelegate.prototype.getChapterInfo = function() { 
    return this._player.getChapterInfo();
};

SampleVideoPlayerPluginDelegate.prototype.getQoSInfo = function() { 
    return this._player.getQoSInfo();
};
```

#### AdobeAnalyticsPluginDelegate (1.x) {#analytics-plugin-delegate-1.x}

```js
$.extend(SampleAdobeAnalyticsPluginDelegate.prototype, AdobeAnalyticsPluginDelegate.prototype);

function SampleAdobeAnalyticsPluginDelegate() {} 

SampleAdobeAnalyticsPluginDelegate.prototype.onError = function(errorInfo) { 
    console.log("AdobeAnalyticsPlugin error: " + errorInfo.getMessage() + " | " + errorInfo.getDetails());
};
```

#### HeartbeatDelegate (1.x) {#hb-delegate-1.x}

```js
$.extend(SampleHeartbeatDelegate.prototype, HeartbeatDelegate.prototype);

function SampleHeartbeatDelegate() {} 

SampleHeartbeatDelegate.prototype.onError = function(errorInfo) { 
    console.log("Heartbeat error: " + errorInfo.getMessage() + " | " + errorInfo.getDetails());
};
```

#### MediaHeartbeatDelegate (2.x) {#mh-delegate-2.x}

```js
ADB.core.extend(SampleMediaHeartbeatDelegate.prototype, MediaHeartbeatDelegate.prototype);

function SampleMediaHeartbeatDelegate(player) { 
    this._player = player;
} 

SampleMediaHeartbeatDelegate.prototype.getCurrentPlaybackTime = function() { 
    return this._player.getCurrentPlaybackTime();
};

SampleMediaHeartbeatDelegate.prototype.getQoSObject = function() { 
    return this._player.getQoSInfo();
};

this._mediaHeartbeat = new MediaHeartbeat(new SampleMediaHeartbeatDelegate(this._player), mediaConfig, appMeasurement);
```

## Comparação de código do VHL: REPRODUÇÃO PRINCIPAL

### Início da sessão

| VHL 1.x | VHL 2.x |
| --- | --- |
| `VideoPlayerPluginDelegate.trackVideoLoad()` | `MediaHeartbeat.createMediaObject()` |
| `VideoPlayerPluginDelegate.getVideoInfo()` | `MediaHeartbeat.trackSessionStart()` |

#### Início da sessão (1.x) {#session-start-1.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() { 
    this._playerPlugin.trackVideoLoad();
};

SampleVideoPlayerPluginDelegate.prototype.getVideoInfo = function() { 
    return this._player.getVideoInfo();
};

VideoPlayer.prototype.getVideoInfo = function() { 
    this._videoInfo.playhead = vTime;
    return this._videoInfo;
};
```

#### Início da sessão (2.x) {#session-start-2.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() { 
    var contextData = {};
    var videoInfo = this._player.getVideoInfo();
    var mediaInfo = MediaHeartbeat.createMediaObject(videoInfo.name, videoInfo.id, videoInfo.length, videoInfo.streamType);
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData);
};
```

### Metadados de vídeo padrão

| API 1.x | API 2.x |
| --- | --- |
| `VideoMetadataKeys()` | `MediaHeartbeat.createMediaObject()` |
| `AdobeAnalyticsPlugin.setVideoMetadata()` | `MediaHeartbeat.trackSessionStart()` |

#### Metadados padrão (1.x) {#std-meta-1.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() {
    console.log('Player event: MEDIA_LOAD');

    var contextData = {};

    // Setting Standard Video Metadata 
    contextData[VideoMetadataKeys.SEASON] = "sample season";
    contextData[VideoMetadataKeys.SHOW] = "sample show";
    contextData[VideoMetadataKeys.EPISODE] = "sample episode";
    contextData[VideoMetadataKeys.ASSET_ID] = "sample asset id";
    contextData[VideoMetadataKeys.GENRE] = "sample genre";
    contextData[VideoMetadataKeys.FIRST_AIR_DATE] = "sample air date";

    // Etc. 
    this._aaPlugin.setVideoMetadata(contextData);
    this._playerPlugin.trackVideoLoad();
};
```

#### Metadados padrão (2.x) {#std-meta-2.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() {
    console.log('Player event: MEDIA_LOAD');
    var contextData = {};
    var mediaInfo = MediaHeartbeat.createMediaObject(videoInfo.name, videoInfo.id, videoInfo.length, videoInfo.streamType);

    // Set standard Video Metadata 
    var standardVideoMetadata = {};
    standardVideoMetadata[VideoMetadataKeys.SEASON] = "sample season";
    standardVideoMetadata[VideoMetadataKeys.SHOW] = "sample show";
    standardVideoMetadata[VideoMetadataKeys.EPISODE] = "sample episode";
    standardVideoMetadata[VideoMetadataKeys.ASSET_ID] = "sample asset id";
    standardVideoMetadata[VideoMetadataKeys.GENRE] = "sample genre";
    standardVideoMetadata[VideoMetadataKeys.FIRST_AIR_DATE] = "sample air date";
    
    // Etc. 
    mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata, standardVideoMetadata);
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData);
};
```

>[!NOTE]
>Em vez de definir os metadados de vídeo padrão por meio da API `AdobeAnalyticsPlugin.setVideoMetadata()`, no VHL 2.0, os metadados de vídeo padrão são definidos pela chave MediaObject `MediaObject.MediaObjectKey.StandardVideoMetadata()`.

### Metadados de vídeo personalizados

| API 1.x | API 2.x |
| --- | --- |
| `VideoMetadataKeys()` | `MediaHeartbeat.createMediaObject()` |
| `AdobeAnalyticsPlugin.setVideoMetadata()` | `MediaHeartbeat.trackSessionStart()` |

#### Metadados personalizados (1.x) {#custom-meta-1.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() { 
    var contextData = { 
        isUserLoggedIn: "false", 
        tvStation: "Sample TV station", 
        programmer: "Sample programmer" 
    };
    this._aaPlugin.setVideoMetadata(contextData);
    this._playerPlugin.trackVideoLoad();
};
```

#### Metadados personalizados (2.x) {#custom-meta-2.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() { 
    var contextData = { 
        isUserLoggedIn: "false", 
        tvStation: "Sample TV station", 
        programmer: "Sample programmer" 
    };
    var videoInfo = this._player.getVideoInfo();
    var mediaInfo = MediaHeartbeat.createMediaObject(videoInfo.name, videoInfo.id, videoInfo.length, videoInfo.streamType);
    mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata, standardVideoMetadata);
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData);
};
```

>[!NOTE]
>Em vez de definir os metadados de vídeo personalizado por meio da API `AdobeAnalyticsPlugin.setVideoMetadata()`, no VHL 2.0, os metadados de vídeo padrão são definidos pela API `MediaHeartbeat.trackSessionStart()`.


### Reprodução

| API 1.x | API 2.x |
| --- | --- |
| `VideoPlayerPlugin.trackPlay()` | `MediaHeartbeat.trackPlay()` |

#### Reprodução (1.x) {#playback-1.x}

```js
VideoAnalyticsProvider.prototype._onSeekStart = function() { 
    console.log('Player event: SEEK_START');
    this._playerPlugin.trackSeekStart();
};
```

#### Reprodução (2.x) {#playback-2.x}

```js
VideoAnalyticsProvider.prototype._onSeekStart = function() { 
    console.log('Player event: SEEK_START');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart);
};
```

### Pausar

| API 1.x | API 2.x |
| --- | --- |
| `VideoPlayerPlugin.trackPause()` | `MediaHeartbeat.trackPausel()` |

#### Pausar (1.x) {#pause-1.x}

```js
VideoAnalyticsProvider.prototype._onPause = function() { 
    console.log('Player event:X PAUSE');
    this._playerPlugin.trackPause();
};
```

#### Pausar (2.x) {#pause-2.x}

```js
VideoAnalyticsProvider.prototype._onBufferComplete = function() { 
    console.log('Player event: BUFFER_COMPLETE');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete);
};
```

### Busca concluída

| API 1.x | API 2.x |
| --- | --- |
| `VideoPlayerPlugin.trackSeekComplete()` | `MediaHeartbeat.`<br/>  `trackEvent(MediaHeartbeat.Event.SeekComplete)` |

#### Busca (1.x) {#seek-1.x}

```js
VideoAnalyticsProvider.prototype._onSeekComplete = function() { 
    console.log('Player event: SEEK_COMPLETE');
    this._playerPlugin.trackSeekComplete();
};
```

#### Busca (2.x) {#seek-2.x}

```js
VideoAnalyticsProvider.prototype._onSeekComplete = function() { 
    console.log('Player event: SEEK_COMPLETE');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete);
};
```

### Início do buffer

| API 1.x | API 2.x |
| --- | --- |
| `VideoPlayerPlugin.trackBufferStart()` | `MediaHeartbeat.trackEvent(`<br/>  `MediaHeartbeat.Event.BufferStart)` |

#### Início do buffer (1.x) {#buffer-start-1.x}

```js
VideoAnalyticsProvider.prototype._onBufferStart = function() { 
    console.log('Player event: BUFFER_START');
    this._playerPlugin.trackBufferStart();
};
```

#### Início do buffer (2.x) {#buffer-start-2.x}

```js
VideoAnalyticsProvider.prototype._onBufferStart = function() { 
    console.log('Player event: BUFFER_START');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart);
};
```

### Buffer concluído

| API 1.x | API 2.x |
| --- | --- |
| `VideoPlayerPlugin.trackBufferComplete()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.BufferComplete)` |

#### Buffer concluído (1.x) {#buffer-complete-1.x}

```js
VideoAnalyticsProvider.prototype._onBufferComplete = function() { 
    console.log('Player event: BUFFER_COMPLETE');
    this._playerPlugin.trackBufferComplete();
};
```

#### Buffer concluído (2.x) {#buffer-complete-2.x}

```js
VideoAnalyticsProvider.prototype._onBufferComplete = function() { 
    console.log('Player event: BUFFER_COMPLETE');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete);
};
```

### Reprodução concluída

| API 1.x | API 2.x |
| --- | --- |
| `VideoPlayerPlugin.trackComplete()` | `MediaHeartbeat.trackComplete()` |

#### Reprodução concluída (1.x) {#playback-complete-1.x}

```js
VideoAnalyticsProvider.prototype._onComplete = function() { 
    console.log('Player event: COMPLETE');
    this._playerPlugin.trackComplete(function() { 
        console.log( "The completion of the content has been tracked.");
    });
};
```

#### Reprodução concluída (2.x) {#playback-complete-2.x}

```js
VideoAnalyticsProvider.prototype._onComplete = function() { 
    console.log('Player event: COMPLETE');
    this._mediaHeartbeat.trackComplete();
};
```

## Comparação de código do VHL: REPRODUÇÃO DO ANÚNCIO

### Início do anúncio

| VHL 1.x | VHL 2.x |
| --- | --- |
| `VideoPlayerPlugin.trackAdStart()` | `MediaHeartbeat.createAdBreakObject()` |
| `VideoPlayerPluginDelegate.getAdBreakInfo()` | `MediaHeartbeat.createAdObject()` |
| `VideoPlayerPluginDelegate.getAdInfo()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.AdBreakStart)` |
|  | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.AdStart)` |

#### Início do anúncio (1.x) {#ad-start-1.x}

```js
VideoAnalyticsProvider.prototype._onAdStart = function() { 
    console.log('Player event: AD_START');
    this._playerPlugin.trackAdStart();
};
```

```js
SampleVideoPlayerPluginDelegate.prototype.getAdInfo = function() { 
    return this._player.getAdInfo(); 
};
```

#### Início do anúncio (2.x) {#ad-start-2.x}

```js
VideoAnalyticsProvider.prototype._onAdStart = function() { 
    console.log('Player event: AD_START');
    var adContextData = {};

    // AdBreak Info - getting the adBreakInfo from player and creating AdBreakInfo Object from MediaHeartbeat 
    var _adBreakInfo = this._player.getAdBreakInfo();
    var adBreakInfo = MediaHeartbeat.createAdBreakObject(_adBreakInfo.name, _adBreakInfo.position, _adBreakInfo.startTime);

    // Ad Info - getting the adInfo from player and creating AdInfo Object from MediaHeartbeat 
    var _adInfo = this._player.getAdInfo();
    var adInfo = MediaHeartbeat.createAdObject(_adInfo.name, _adInfo.id, _adInfo.position, _adInfo.length);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adContextData);
};
```

### Metadados de publicidade padrão

| API 1.x | API 2.x |
| --- | --- |
| `AdMetadataKeys()` | `MediaHeartbeat.createAdObject()` |
| `AdobeAnalyticsPlugin.setAdMetadata()` | `MediaHeartbeat.trackAdStart()` |

#### Metadados de anúncio padrão (1.x) {#ad-meta-1.x}

```js
VideoAnalyticsProvider.prototype._onAdStart = function() {
    console.log('Player event: AD_START');
    var contextData = {};

    // setting Standard Ad Metadata 
    contextData[AdMetadataKeys.ADVERTISER] = "sample advertiser";
    contextData[AdMetadataKeys.CAMPAIGN_ID] = "sample campaign";
    contextData[AdMetadataKeys.CREATIVE_ID] = "sample creative";
    contextData[AdMetadataKeys.CREATIVE_URL] = "sample url";
    contextData[AdMetadataKeys.SITE_ID] = "sample site";
    contextData[AdMetadataKeys.PLACEMENT_ID] = "sample placement";
    this._aaPlugin.setAdMetadata(contextData);
    this._playerPlugin.trackAdStart();
};
```

#### Metadados de anúncio padrão (2.x) {#ad-meta-2.x}

```js
VideoAnalyticsProvider.prototype._onAdStart = function() { 
    console.log('Player event: AD_START');
    var adContextData = { };

    // AdBreak Info - getting the adBreakInfo from player and creating AdBreakInfo Object from MediaHeartbeat 
    var _adBreakInfo = this._player.getAdBreakInfo();
    var adBreakInfo = MediaHeartbeat.createAdBreakObject(_adBreakInfo.name, _adBreakInfo.position, _adBreakInfo.startTime);

    // Ad Info - getting the adInfo from player and creating AdInfo Object from MediaHeartbeat 
    var _adInfo = this._player.getAdInfo();
    var adInfo = MediaHeartbeat.createAdObject(_adInfo.name, _adInfo.id, _adInfo.position, _adInfo.length);

    // Set standard Ad Metadata 
    var standardAdMetadata = {};
    standardAdMetadata[MediaHeartbeat.AdMetadataKeys.ADVERTISER] = "Sample Advertiser";
    standardAdMetadata[MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID] = "Sample Campaign";
    adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adContextData);
};
```

>[!NOTE]
>Em vez de definir os metadados de anúncio padrão por meio da API `AdobeAnalyticsPlugin.setVideoMetadata()`, no VHL 2.0, os metadados de anúncio padrão são definidos pela chave `AdMetadata` `MediaObject.MediaObjectKey.StandardVideoMetadata`

### Metadados de anúncio personalizados

| API 1.x | API 2.x |
| --- | --- |
| `AdobeAnalyticsPlugin.setAdMetadata()` | `MediaHeartbeat.createAdObject()` |
|  | `MediaHeartbeat.trackAdStart()` |

#### Metadados de anúncio personalizados (1.x) {#custom-ad-meta-1.x}

```js
VideoAnalyticsProvider.prototype._onAdStart = function() { 
    console.log('Player event: AD_START');
    var contextData = {};

    // Setting Standard Ad Metadata 
    contextData[AdMetadataKeys.ADVERTISER] = "sample advertiser";
    contextData[AdMetadataKeys.CAMPAIGN_ID] = "sample campaign";
    contextData[AdMetadataKeys.CREATIVE_ID] = "sample creative";
    contextData[AdMetadataKeys.CREATIVE_URL] = "sample url";
    contextData[AdMetadataKeys.SITE_ID] = "sample site";
    contextData[AdMetadataKeys.PLACEMENT_ID] = "sample placement";
    this._aaPlugin.setAdMetadata(contextData);
    this._playerPlugin.trackAdStart();
};
```

#### Metadados de anúncio personalizados (2.x) {#custom-ad-meta-2.x}

```js
VideoAnalyticsProvider.prototype._onAdStart = function() { 
    console.log('Player event: AD_START');
    var adContextData = { 
        affiliate: "Sample affiliate", 
        campaign: "Sample ad campaign" 
    };

    // AdBreak Info - getting the adBreakInfo from player and creating AdBreakInfo Object from MediaHeartbeat 
    var _adBreakInfo = this._player.getAdBreakInfo();
    var adBreakInfo = MediaHeartbeat.createAdBreakObject(_adBreakInfo.name, _adBreakInfo.position, _adBreakInfo.startTime);

    // Ad Info - getting the adInfo from player and creating AdInfo Object from MediaHeartbeat 
    var _adInfo = this._player.getAdInfo();
    var adInfo = MediaHeartbeat.createAdObject(_adInfo.name, _adInfo.id, _adInfo.position, _adInfo.length);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakInfo);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adInfo, adContextData);
};
```

>[!NOTE]
>Em vez de definir os metadados de anúncio personalizados por meio da API `AdobeAnalyticsPlugin.setVideoMetadata`, no VHL 2.0, os metadados de anúncios padrão são definidos pela API `MediaHeartbeat.trackAdStart()`.

### Anúncio ignorado

| API 1.x | API 2.x |
| --- | --- |
| `AdobeAnalyticsPlugin.setAdMetadata()` | `MediaHeartbeat.createAdObject()` |
|  | `MediaHeartbeat.trackAdStart()` |

#### Ignorar anúncio (1.x) {#ad-skip-1.x}

```js
SampleVideoPlayerPluginDelegate.prototype.getAdInfo = function() { 
    return this._player.getAdInfo();
};
```

#### Ignorar anúncio (2.x) {#ad-skip-2.x}

```js
VideoAnalyticsProvider.prototype._onAdSkip = function() { 
    console.log('Player event: AD_SKIP');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip);
};
```

>[!NOTE]
>Nas APIs do VHL 1.5.X; `getAdinfo()` e `getAdBreakInfo()` devem retornar nulo se o reprodutor estiver fora dos limites do Ad break.

### Anúncio concluído

| API 1.x | API 2.x |
| --- | --- |
| `VideoPlayerPlugin.trackAdComplete()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.AdComplete)` |
|  | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.AdBreakComplete)` |

#### Anúncio concluído (1.x) {#ad-complete-1.x}

```js
VideoAnalyticsProvider.prototype._onAdComplete = function() { 
    console.log('Player event: AD_COMPLETE');
    this._playerPlugin.trackAdComplete();
};
```

#### Anúncio concluído (2.x) {#ad-complete-2.x}

```js
VideoAnalyticsProvider.prototype._onAdComplete = function() { 
    console.log('Player event: AD_COMPLETE');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete);
};
```

## Comparação de código do VHL: REPRODUÇÃO DO CAPÍTULO

### Início do capítulo

| VHL 1.x | VHL 2.x |
| --- | --- |
| `VideoPlayerPluginDelegate.getChapterInfo()` | `MediaHeartbeat.createChapterObject` |
| `VideoPlayerPlugin.trackChapterStart()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.ChapterStart)` |

#### Início do capítulo (1.x) {#chap-start-1.x}

```js
VideoAnalyticsProvider.prototype._onChapterStart = function() { 
    console.log('Player event: CHAPTER_START');
    this._playerPlugin.trackChapterStart();
};
```

```js
SampleVideoPlayerPluginDelegate.prototype.getChapterInfo = function() { 
    return this._player.getChapterInfo();
};
```

#### Início do capítulo (2.x) {#chap-start-2.x}

```js
VideoAnalyticsProvider.prototype._onChapterStart = function() { 
    console.log('Player event: CHAPTER_START');
    var chapterContextData = { };

    // Chapter Info - getting the chapterInfo from player and creating ChapterInfo Object from MediaHeartbeat 
    var _chapterInfo = this._player.getChapterInfo();
    var chapterInfo = MediaHeartbeat.createChapterObject(_chapterInfo.name, _chapterInfo.position, _chapterInfo.length, _chapterInfo.startTime);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart, chapterInfo, chapterContextData);
};
```

### Capítulo ignorado

| API 1.x | API 2.x |
| --- | --- |
| `VideoPlayerPluginDelegate.getChapterInfo()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.ChapterSkip)` |

#### Capítulo Ignorar (1.x) {#chap-skip-1.x}

```js
SampleVideoPlayerPluginDelegate.prototype.getChapterInfo = function() { 
    return this._player.getChapterInfo();
};
```

>[!NOTE]
>Nas APIs do VHL 1.5.X, `getChapterinfo()` deve retornar nulo se o reprodutor estiver fora dos limites do Capítulo.

#### Capítulo Ignorar (2.x) {#chap-skip-2.x}

```js
VideoAnalyticsProvider.prototype._onChapterSkip = function() { 
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip);
};
```

### Metadados de capítulo personalizados

| API 1.x | API 2.x |
| --- | --- |
| `VideoPlayerPlugin.trackChapterStart()` | `MediaHeartbeat.createChapterObject()` |
| `AdobeAnalyticsPlugin.setChapterMetadata()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.ChapterStart)` |

#### Metadados personalizados do capítulo (1.x) {#chap-cust-meta-1.x}

```js
VideoAnalyticsProvider.prototype._onChapterStart = function() { 
    console.log('Player event: CHAPTER_START');
    this._aaPlugin.setChapterMetadata({ 
        segmentType: "Sample segment type" 
    });
    this._playerPlugin.trackChapterStart();
};
```

#### Metadados personalizados do capítulo (2.x) {#chap-cust-meta-2.x}

```js
VideoAnalyticsProvider.prototype._onChapterStart = function() { 
    console.log('Player event: CHAPTER_START');
    var chapterContextData = { 
        segmentType: "Sample segment type" 
    };

    // Chapter Info - getting the chapterInfo from player and creating ChapterInfo Object from MediaHeartbeat 
    var _chapterInfo = this._player.getChapterInfo();
    var chapterInfo = MediaHeartbeat.createChapterObject(_chapterInfo.name, _chapterInfo.position, _chapterInfo.length, _chapterInfo.startTime);
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart, chapterInfo, chapterContextData);
};
```

### Capítulo concluído

| API 1.x | API 2.x |
| --- | --- |
| `trackChapterComplete()` | `trackEvent(MediaHeartbeat.Event.ChapterComplete)` |

#### Capítulo concluído (1.x) {#chap-complete-1.x}

```js
VideoAnalyticsProvider.prototype._onChapterComplete = function() { 
    console.log('Player event: CHAPTER_COMPLETE');
    this._playerPlugin.trackChapterComplete();
};
```

#### Capítulo concluído (2.x) {#chap-complete-2.x}

```js
VideoAnalyticsProvider.prototype._onChapterComplete = function() { 
    console.log('Player event: CHAPTER_COMPLETE');
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete);
};
```

## Comparação de código do VHL: OUTROS EVENTOS

### Alteração na taxa de bits

| VHL 1.x | VHL 2.x |
| --- | --- |
| `VideoPlayerPlugin.trackBitrateChange()` | `MediaHeartbeat.trackEvent(`<br/><br/>  `MediaHeartbeat.Event.BitrateChange)` |

#### Alteração da taxa de bits (1.x) {#bitrate-chg-1.x}

```js
VideoAnalyticsProvider.prototype._onBitrateChange = function() { 
    console.log('Player event: BITRATE_CHANGE');

    // Update getQosInfo to return the updated bitrate 
    this._playerPlugin.trackBitrateChange();
};
```

#### Alteração da taxa de bits (2.x) {#bitrate-chg-2.x}

```js
VideoAnalyticsProvider.prototype._onBitrateChange = function() { 
    console.log('Player event: BITRATE_CHANGE');

    // Update getQosObject to return the updated bitrate 
    this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange);
};
```

### Retomar vídeo

| API 1.x | API 2.x |
| --- | --- |
| `VideoInfo.resumed()` | `MediaObject()` |
| `VideoPlayerPluginDelegate.getVideoInfo()` | `MediaHeartbeat.trackSessionStart()` |
| `VideoPlayerPlugin.trackVideoLoad()` |  |

#### Retomada de vídeo (1.x) {#video-resume-1.x}

```js
this._videoInfo.resumed=true;
```

```js
VideoPlayer.prototype.getVideoInfo = function() { 
    this._videoInfo.playhead = vTime;
    return this._videoInfo;
};
```

#### Retomada de vídeo (2.x) {#video-resume-2.x}

```js
VideoAnalyticsProvider.prototype._onLoad = function() { 
    console.log('Player event: MEDIA_LOAD');
    var contextData = {};
    var videoInfo = this._player.getVideoInfo();
    var mediaInfo = MediaHeartbeat.createMediaObject(videoInfo.playerName, videoInfo.id, videoInfo.length, videoInfo.streamType);
    mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.VideoResumed, true);
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData);
};
```

Para obter mais informações sobre o rastreamento de vídeo com 2.x, consulte [Rastrear reprodução de vídeo principal.](/help/sdk-implement/track-av-playback/track-core-overview.md)
