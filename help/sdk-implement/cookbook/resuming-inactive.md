---
seo-title: Resumo de sessões inativas
title: Resumo de sessões inativas
uuid: 3 ff 1205 d -7 bbe -4016-9 bd 7-6 e 34 b 7862 c 4 c
translation-type: tm+mt
source-git-commit: 8c20af925a1043c90b84d7d13021848725e05500

---


# Resumo de sessões inativas{#resuming-inactive-sessions}

## Pausas longas

O SDK de mídia monitora automaticamente por quanto tempo a reprodução da mídia está em um dos estados inativos a seguir:

* Pausado
* Buscando
* Paralisado
* Buffering

Se uma sessão de rastreamento de mídia permanecer em estado inativo por mais de 30 minutos, a sessão será fechada automaticamente. Se o usuário retomar a sessão após o estado inativo (`trackPlay`), o Media Heartbeat cria automaticamente uma nova sessão de vídeo com as informações e os metadados que foram utilizados anteriormente e envia um evento de retomada de heartbeat. Para obter mais informações, consulte [Parâmetros de áudio e vídeo.](../../metrics-and-metadata/audio-video-parameters.md)

## Retomar manualmente uma sessão fechada

O SDK de mídia só retomará automaticamente as sessões se o aplicativo não tiver sido fechado. Se o aplicativo armazenar dados do usuário e tiver a capacidade de retomar uma mídia fechada anteriormente, é possível acionar manualmente um evento de retomada. Assim que iniciar a sessão de rastreamento de vídeo, defina a propriedade opcional Vídeo retomado.

### Android

```java
// Set MediaHeartbeat.MediaObjectKey.mediaResumed to true 
public void onmediaLoad(Observable observable, Object data) { 

  // Replace <MEDIA_NAME> with the media name. 
  // Replace <MEDIA_ID> with a media unique identifier. 
  // Replace <MEDIA_LENGTH> with the media length.  
  MediaObject mediaInfo = MediaHeartbeat.createMediaObject(  
      <MEDIA_NAME>,  
      <MEDIA_ID>,  
      <MEDIA_LENGTH>,  
      MediaHeartbeat.StreamType.VOD 
  ); 
   
  // Set to true if this is a resume playback scenario 
  mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.mediaResumed, true);
   
  _heartbeat.trackSessionStart(mediaInfo, mediaMetadata); 
}
```

### iOS

```
- (void)onMainmediaLoaded:(NSNotification *)notification { 
  //Replace <MEDIA_NAME> with the media name. 
  //Replace <MEDIA_ID> with a media unique identifier. 
  //Replace <MEDIA_LENGTH> with the media length.     
  ADBMediaObject *mediaObject =  
    [ADBMediaHeartbeat createMediaObjectWithName:<MEDIA_NAME> 
                       mediaId:<MEDIA_ID> 
                       length:<MEDIA_LENGTH> 
                       streamType:ADBMediaHeartbeatStreamTypeVOD]; 

  //Set to YES if this user is resuming a previously closed media session 
  [mediaObject setValue:@(YES) forKey:ADBMediaObjectKeymediaResumed];

  [_mediaHeartbeat trackSessionStart:mediaObject data:mediaMetadata]; 
} 
```

### JavaScript

```js
_onmediaLoad = function () { 
  // Replace <MEDIA_NAME> with the media name. 
  // Replace <MEDIA_ID> with a media unique identifier. 
  // Replace <MEDIA_LENGTH> with the media length.  
  var mediaObject =  
    MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                     <MEDIA_ID,  
                                     <MEDIA_LENGTH>,  
                                     MediaHeartbeat.StreamType.VOD);

  // Set to true if this user is resuming a previously closed media session 
  mediaObject.setValue(MediaObjectKey.mediaResumed, true); 
  this._mediaHeartbeat.trackSessionStart(mediaObject, contextData); 
};
```

