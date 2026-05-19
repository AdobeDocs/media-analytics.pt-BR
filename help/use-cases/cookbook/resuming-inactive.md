---
title: Resumo de sessões inativas
description: Como lidar com a retomada de uma sessão inativa.
uuid: 3ff1205d-7bbe-4016-9bd7-6e34b7862c4c
exl-id: ee4cf7f5-5788-4d35-a04d-4ed714ccd663
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/KT7NfrYlagrMwAjsrbSNR8YUbj5d-ihU8AfJ6wcbgOA
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: 398
ht-degree: 37%

---

# Resumo de sessões inativas{#resuming-inactive-sessions}

## Pausas longas

O SDK do Media rastreia automaticamente por quanto tempo a reprodução de mídia permanece em um dos seguintes estados inativos:

* Pausado
* Busca
* Parado
* Buffering

Se uma sessão de rastreamento de mídia se mantiver no estado inativo por mais de 30 minutos, ela será encerrada automaticamente. Se o usuário retomar a sessão após o estado inativo (`trackPlay`), o Media Heartbeat cria automaticamente uma nova sessão de vídeo com as informações e os metadados que foram utilizados anteriormente e envia um evento de retomada de heartbeat.

## Transferência entre dispositivos usando o sinalizador de retomada

O mesmo mecanismo de continuação que lida com a continuação da sessão de aplicativo único também se aplica quando um visualizador transfere a reprodução entre dispositivos — por exemplo, transmitindo um vídeo de um telefone celular para uma TV ou receptor Chromecast. Como cada dispositivo executa sua própria instância do Media SDK, a entrega cria várias sessões por padrão. Use o sinalizador de retomada para uni-los em uma continuação lógica, de modo que o Analytics reporte a visualização combinada como uma única parte do engajamento, em vez de inicializações de mídia separadas.

**Como implementar:**

1. No **dispositivo de origem** (por exemplo, o telefone), chame `trackSessionEnd` quando o visualizador iniciar a conversão. Não chamar `trackComplete` — o conteúdo não foi concluído, está sendo movido para outro dispositivo.
2. No **dispositivo de destino** (por exemplo, o Chromecast), chame `trackSessionStart` com o sinalizador de retomada definido como `true` e os mesmos metadados de conteúdo (nome, ID, comprimento) usados no dispositivo de origem. Passe a posição do indicador de reprodução para onde o visualizador parou no dispositivo de origem.
3. Se o visualizador retornar posteriormente a reprodução para o dispositivo de origem, repita o mesmo padrão: `trackSessionEnd` no destino e `trackSessionStart` com o sinalizador de retomada na origem.

Definir o sinalizador de retomada faz com que o Adobe Analytics incremente [retomas de conteúdo](/help/reporting/metrics/content-resumes.md) em vez de [inícios da mídia](/help/reporting/metrics/media-starts.md) para o segundo e seguintes trechos da entrega. Como não há nenhum mecanismo incorporado para compartilhar a ID da sessão entre instâncias do SDK, o sinalizador de retomada é uma declaração do lado do cliente. Você o transmite com base na lógica do aplicativo quando sabe que o visualizador continua uma sessão anterior.

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
