---
title: Reprodução de VOD com buffering
description: Veja um exemplo de como rastrear o conteúdo de VOD usando o SDK do Media.
uuid: 958f7692-7193-40fb-a8e7-2ff4fa805330
exl-id: 3a8f913f-cb51-45ae-ac1d-862ea1e7c994
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 92%

---

# Reprodução de VOD com buffering{#vod-playback-with-buffering}

## Cenário {#scenario}

Nesse cenário, ocorre buffering quando o conteúdo de VOD é reproduzido.

A menos que seja especificado, as chamadas de rede desse cenário correspondem às chamadas presentes no cenário de [reprodução de VOD sem anúncios](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md).

| Acionador   | Método do Heartbeat   | Chamadas de rede   | Notas   |
|---|---|---|---|
| Cliques do usuário **[!UICONTROL Reproduzir]** | `trackSessionStart` | Início do conteúdo do Analytics, Início do conteúdo do Heartbeat | Pode ser um usuário que clicou na opção **[!UICONTROL Reproduzir]**, ou um evento de reprodução automática. |
| O primeiro quadro do vídeo é reproduzido. | `trackPlay` | Heartbeat Content Play | Esse método aciona o temporizador. Os heartbeats são enviados a cada 10 segundos enquanto a reprodução continuar. |
| O conteúdo é reproduzido. |  | Content Heartbeats |  |
| Os buffering inicia. | `trackEvent:BufferStart` | Buffer do Heartbeat |  |
| O conteúdo está em buffer. |  | Content Heartbeats |  |
| O buffering é concluído. | `trackEvent:BufferComplete` | Heartbeat Buffer, Heartbeat Play |  |
| O conteúdo é reproduzido. |  | Content Heartbeats |  |
| A reprodução do conteúdo é concluída. | `trackComplete` | Heartbeat Content Complete | O fim do indicador de reprodução foi atingido. |
| A sessão foi encerrada. | `trackSessionEnd` |  | `SessionEnd` significa o fim de uma sessão de exibição. Essa API deve ser chamada mesmo se o usuário não assistir o vídeo até o fim. |

## Parâmetros {#parameters}

### Buffer do Heartbeat

| Parâmetro | Valor | Notas |
|---|---|---|
| `s:event:type` | `"buffer"` |  |

## Código de exemplo {#sample-code}

Nesse cenário, ocorre buffering quando o conteúdo de VOD é reproduzido.

![](assets/buffer-regular-content.png)

### Android

Para exibir esse cenário no Android, configure o seguinte código:

```java
// Set up mediaObject 

MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.VOD 

); 

HashMap<String, String> videoMetadata = new HashMap<String, String>(); 
videoMetadata.put(CUSTOM_KEY_1, CUSTOM_VAL_1); 
videoMetadata.put(CUSTOM_KEY_2, CUSTOM_VAL_2); 

// 1. Call trackSessionStart() when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback. 
_mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the first  
//    frame of the main content is rendered on the screen. 
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Track the MediaHeartbeat.Event.BufferStart event when the video player  
//    goes into the buffering state and begins to buffer content. 
_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart, null, null); 

....... 
....... 

// 4. Track the MediaHeartbeat.Event.BufferComplete event when the video player  
//    goes into the buffering state and begins to buffer content. 
_mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete, null, null); 

....... 
....... 

// 5. Call trackComplete() when the playback reaches the end, i.e., when the 
//    video completes and finishes playing. 
_mediaHeartbeat.trackComplete(); 

........ 
........ 

// 6. Call trackSessionEnd() when the playback session is over. This method must  
//    be called even if the user does not watch the video to completion. 
_mediaHeartbeat.trackSessionEnd(); 

........ 
```

### iOS

Para exibir esse cenário no iOS, configure o seguinte código:

```
// Set up mediaObject 
ADBMediaObject *mediaObject =  
[ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                   length:MEDIA_LENGTH  
                   streamType:ADBMediaHeartbeatStreamTypeVOD]; 
 
NSMutableDictionary *videoContextData = [[NSMutableDictionary alloc] init]; 
[videoContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
[videoContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 

// 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback. 
[_mediaHeartbeat trackSessionStart:mediaObject data:videoContextData]; 
....... 
....... 

// 2. Call trackPlay when the playback actually starts, i.e., when the first  
//    frame of the main content is rendered on the screen. 
[_mediaHeartbeat trackPlay];  
....... 
....... 

// 3. Track the trackEvent:ADBMediaHeartbeatEventBufferStart event when the  
//    video player goes in buffering state and begins to buffer content. 
[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferStart  
               mediaObject:nil  
               data:nil]; 
....... 
....... 

// 4. Track the trackEvent:ADBMediaHeartbeatEventBufferComplete event when  
//    the video player goes in buffering state and begins to buffer content. 
[_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferComplete  
               mediaObject:nil  
               data:nil]; 
....... 
....... 

// 5. Call trackComplete when the playback reaches the end, i.e., when the 
//    video completes and finishes playing. 
[_mediaHeartbeat trackComplete]; 
....... 
....... 

// 6. Call trackSessionEnd when the playback session is over. This method must  
//    be called even if the user does not watch the video to completion. 
[_mediaHeartbeat trackSessionEnd]; 
....... 
....... 
```

### JavaScript

Para exibir este cenário, insira o seguinte texto:

```js
// Set up mediaObject 

var mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.VOD 

); 

var videoMetadata = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 
}; 

// 1. Call trackSessionStart() when Play is clicked or if autoplay is used,  
//    i.e., there's an intent to start playback. 
this._mediaHeartbeat.trackSessionStart(mediaInfo, videoMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the  
//    first frame of the ad video is rendered on the screen. 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Track event MediaHeartbeat.Event.BufferStart when the video player  
//    goes into the buffering state and begins to buffer content. 
this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart); 

....... 
....... 

// 4. Track the MediaHeartbeat.Event.BufferComplete event when the  
//    video player goes into the buffering state and begins to buffer content. 
this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete); 

....... 
....... 

// 5. Call trackComplete() when the playback reaches the end, i.e.,  
//    when playback completes and finishes playing. 
this._mediaHeartbeat.trackComplete(); 

........ 
........ 

// 6. Call trackSessionEnd() when the playback session is over. This method must  
//    be called even if the user does not watch the video to completion. 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........ 
```