---
title: Implementar metadados padrão no JavaScript
description: Descreve a configuração de metadados de vídeo e anúncios padrão a serem enviados com chamadas de rastreamento em aplicativos do navegador (JS).
uuid: 523d29e3-0a62-40d7-ac74-da645024cdcb
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Implementar metadados padrão no JavaScript {#implement-standard-metadata-on-javascript}

## Constante de metadados

| Nome da constante | Descrição   |
| --- | --- |
| `StandardMediaMetadata` | Constante para anexar os metadados padrão no `MediaObject` |

## Implementação

Exemplifique um objeto de metadados padrão, preencha as variáveis desejadas e defina o objeto de metadados no objeto de Heartbeat de mídia. Por exemplo:

```js
_onVideoLoad = function () { 
    //Create the Media Object   
    var mediaInfo =  
      MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                       <MEDIA_ID,  
                                       <MEDIA_LENGTH>, 
                                       <STREAM_TYPE>,
                                       <MEDIA_TYPE>); 
 
    //Set standard Video Metadata 
    var standardMediaMetadata = {};     
    standardMediaMetadata[MediaHeartbeat.VideoMetadataKeys.SHOW] = "Sample Show"; 
    standardMediaMetadata[MediaHeartbeat.VideoMetadataKeys.SEASON] = "Sample Season"; 
    standardMediaMetadata[MediaHeartbeat.VideoMetadataKeys.EPISODE] = "Sample Episode"; 
 
    //Set standard Audio Metadata 
    var standardMediaMetadata = {};     
    standardMediaMetadata[MediaHeartbeat.AudioMetadataKeys.ARTIST] = "Sample Artist"; 
    standardMediaMetadata[MediaHeartbeat.AudioMetadataKeys.ALBUM] = "Sample Album"; 
    standardMediaMetadata[MediaHeartbeat.AudioMetadataKeys.LABEL] = "Sample Label"; 
 
    mediaInfo.setValue(MediaObjectKey.StandardMediaMetadata, standardMediaMetadata); 
    this._mediaHeartbeat.trackSessionStart(mediaInfo, contextData); 
}; 
```

