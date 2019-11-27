---
title: Implementar metadados padrão no Chromecast
description: Descreve a configuração de vídeos e metadados de anúncio padrão no Chromecast.
uuid: 1560d3e0-29f5-4678-9f01-c672e0ae547b
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Implementar metadados padrão no Chromecast {#implement-standard-metadata-on-chromecast}

Exemplifique um objeto de metadados padrão, preencha as variáveis desejadas e defina o objeto de metadados no objeto de Heartbeat de mídia. Por exemplo:

```js
var standardVideoMetadata = {}; 
standardVideoMetadata[VideoMetadataKeys.SHOW] = "Sample show"; 
standardVideoMetadata[VideoMetadataKeys.SEASON] = "Sample season"; 
 
mediaObject[ADBMobile.media.MediaObjectKey.StandardVideoMetadata] = standardVideoMetadata;
```

```js
var standardAudioMetadata = {}; 
standardAudioMetadata[AudioMetadataKeys.ARTIST] = "Sample artist"; 
standardAudioMetadata[AudioMetadataKeys.ALBUM] = "Sample album"; 
 
mediaObject[ADBMobile.media.MediaObjectKey.StandardAudioMetadata] = standardAudioMetadata;
```

Consulte a lista completa de metadados de áudio e vídeo aqui: [Parâmetros de áudio e vídeo.](/help/metrics-and-metadata/audio-video-parameters.md)
