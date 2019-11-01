---
title: Implementar metadados padrão no Android
description: Descreve a configuração de metadados de vídeo e anúncio padrão para serem enviados com chamadas de rastreamento no Android.
uuid: c48b4190-b062-4c4e-9c40-8dde4598a50e
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Implementar metadados padrão no Android{#implement-standard-metadata-on-android}

## Constantes de metadados padrão

| Nome da constante | Descrição   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardMediaMetadata` | Constante para anexar os metadados padrão no `MediaObject`. |

## Referência da API para chaves de metadados

* Crie um conjunto `HashMap` de pares de valores principais de metadados padronizados.
   * [Teclas de metadados de vídeo](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
   * [Teclas de metadados de áudio](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.AudioMetadataKeys.html)
* Defina os metadados padrão `HashMap` no `MediaInfo` usando a constante de Metadados padrão para os metadados.
* Provide this `MediaInfo` object while invoking the `trackSessionStart()` API.

## Exemplos de implementações

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
