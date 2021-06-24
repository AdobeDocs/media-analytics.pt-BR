---
title: Resumo de sessões inativas
description: Saiba como lidar com a retomada de uma sessão inativa.
uuid: 3ff1205d-7bbe-4016-9bd7-6e34b7862c4c
exl-id: ee4cf7f5-5788-4d35-a04d-4ed714ccd663
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 95%

---

# Resumo de sessões inativas{#resuming-inactive-sessions}

## Pausas longas

O SDK do Media rastreia automaticamente por quanto tempo a reprodução de mídia permanece em um dos seguintes estados inativos:

* Pausado
* Buscando
* Paralisado
* Buffering

Se uma sessão de rastreamento de mídia se mantiver no estado inativo por mais de 30 minutos, ela será encerrada automaticamente. Se o usuário retomar a sessão após o estado inativo (`trackPlay`), o Media Heartbeat cria automaticamente uma nova sessão de vídeo com as informações e os metadados que foram utilizados anteriormente e envia um evento de retomada de heartbeat. Para obter mais informações, consulte [Parâmetros de áudio e vídeo.](/help/metrics-and-metadata/audio-video-parameters.md)

## Retomar manualmente uma sessão fechada

O SDK do Media só retomará automaticamente as sessões se o aplicativo não tiver sido fechado. Se o aplicativo armazenar dados do usuário e tiver a capacidade de retomar uma mídia fechada anteriormente, será possível acionar manualmente um evento de retomada. Assim que iniciar a sessão de rastreamento de vídeo, defina a propriedade opcional Vídeo retomado.

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
