---
seo-title: Conversão da API de 1.x para 2.x
title: Conversão da API de 1.x para 2.x
uuid: 6 e 619288-c 082-4 cb 4-8685-e 90823 dadf 4 a
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# API 1.x to 2.x conversion {#one-x-to-two-x-conv}

## Referências de API do Media SDK 2. x

* [Referência da API do Android](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/index.html)
* [Referência da API do iOS](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/index.html)
* [Referência da API do JS](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/index.html)
* [Referência da API do Chromecast](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/index.html)

## Track Track * apis:

| VHL 1. x  | VHL 2. x |
|---|---|
| `videoPlayerPlugin.trackVideoLoad()` | N/A |
| `videoPlayerPlugin.trackSessionStart()` | [mediaHeartbeat.trackSessionStart(mediaObject, mediaCustomMetadata)](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackSessionStart) |
| `videoPlayerPlugin.trackPlay()` | [mediaHeartbeat.trackPlay()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackPlay) |
| `videoPlayerPlugin.trackPause()` | [mediaHeartbeat.trackPause()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackPause) |
| `videoPlayerPlugin.trackComplete()` | [mediaHeartbeat.trackComplete()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackComplete) |
| `videoPlayerPlugin.trackVideoUnload()` | [mediaHeartbeat.trackSessionEnd()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackSessionEnd) |
| `videoPlayerPlugin.trackApplicationError()` | N/A |
| `videoPlayerPlugin.trackVideoPlayerError()` | [mediaHeartbeat.trackError()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackError) |

Todas as APIs de rastreamento opcionais, como anúncios, capítulos, alteração na taxa de bits, busca e buffering, agora fazem parte de uma única API `trackEvent`. A API [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackEvent) recebe um parâmetro de constante que representa o tipo de evento que ela deve rastrear:

## APIs trackEvent opcionais:

| VHL 1.x | VHL 2.x |
|---|---|
| Return a valid `AdBreakInfo` in `VideoPlayerPlugin.getAdBreakInfo()` | `trackEvent(Event.AdBreakStart)` |
| Return null in `VideoPlayerPlugin.getAdBreakInfo()` | `trackEvent(Event.AdBreakComplete)` |
| `playerPlugin.trackAdStart()` | `trackEvent(Event.AdStart, adObject, adCustomMetadata)` |
| `playerPlugin.trackAdComplete()` | `trackEvent(Event.AdComplete)` |
| Return null in `VideoPlayerPlugin.getAdInfo()` | `trackEvent(Event.AdSkip)` |
| `playerPlugin.trackChapterStart()` | `trackEvent(Event.ChapterStart, chapterObject, chapterCustomMetadata)` |
| `playerPlugin.trackChapterComplete()` | `trackEvent(Event.ChapterComplete)` |
| Return null in `VideoPlayerPlugin.getChapterInfo()` | `trackEvent(Event.ChapterSkip)` |
| `playerPlugin.trackSeekStart()` | `trackEvent(Event.SeekStart)` |
| `playerPlugin.trackSeekComplete()` | `trackEvent(Event.SeekComplete)` |
| `playerPlugin.trackBufferStart()` | `trackEvent(Event.BufferStart)` |
| `playerPlugin.trackBufferComplete()` | `trackEvent(Event.BufferComplete)` |
| `playerPlugin.trackBitrateChange()` | `trackEvent(Event.BitrateChange)` |
| `playerPlugin.trackTimedMetadata()` | `trackEvent(Event.TimedMetadataUpdate)` |

