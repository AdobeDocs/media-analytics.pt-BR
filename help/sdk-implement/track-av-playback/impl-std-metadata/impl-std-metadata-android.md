---
description: 'null'
seo-description: 'null'
seo-title: Implementar metadados padrão no Android
title: Implementar metadados padrão no Android
uuid: c 48 b 4190-b 062-4 c 4 e -9 c 40-8 dde 4598 a 50 e
translation-type: tm+mt
source-git-commit: 46797deb402fed1c4d4781507c279407f8c13f2e

---


# Implementar metadados padrão no Android{#implement-standard-metadata-on-android}

## Constantes de metadados padrão

| Nome da constante | Descrição  |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardMediaMetadata` | Constante para anexar os metadados padrão no `MediaObject`. |

## Referência da API de chaves de metadados

* Create a `HashMap` of standard metadata key value pairs.
   * [Chaves de metadados do vídeo](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
   * [Teclas de metadados de áudio](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.AudioMetadataKeys.html)
* Defina os metadados padrão `HashMap` no `MediaInfo` usando a constante de Metadados padrão para os metadados.
* Provide this `MediaInfo` object while invoking the `trackSessionStart()` API.

## Exemplo de implementações

### Vídeo

```java
// Sample code to set standard metadata for tracking sessions 
Map <String, String> standardVideoMetadata= new HashMap<String, String>(); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.EPISODE, "Sample Episode"); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SHOW, "Sample Show"); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SEASON, "Sample Season"); 
mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata, standardVideoMetadata);
```

### Áudio

```java
// Sample code to set standard metadata for tracking sessions 
Map <String, String> standardAudiooMetadata= new HashMap<String, String>(); 
standardAudiooMetadata.put(MediaHeartbeat.AudiooMetadataKeys.ARTIST, "Sample Artist"); 
standardAudiooMetadata.put(MediaHeartbeat.AudiooMetadataKeys.ALBUM, "Sample Album"); 
standardAudiooMetadata.put(MediaHeartbeat.AudiooMetadataKeys.LABEL, "Sample Label"); 
mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAudiooMetadata, standardAudiooMetadata);
```
