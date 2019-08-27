---
seo-title: Conteúdo principal disponível
title: Conteúdo principal disponível
uuid: e 92 e 99 f 4-c 395-48 aa -8 a 30-cbdd 2 f 5 fc 07 c
translation-type: tm+mt
source-git-commit: 46710c621f00374aeb55a88e51d4b720dcb941a6

---


# Conteúdo principal ao vivo{#live-main-content}

## Cenário {#section_13BD203CBF7546D2A6AD0129B1EEB735}

Neste cenário, há um ativo disponível sem anúncios reproduzido por 40 segundos após a entrada na transmissão ao vivo.

| Acionador | Método do Heartbeat | Chamadas de rede | Notas  |
|---|---|---|---|
| User clicks **[!UICONTROL Play]** | `trackSessionStart` | Início do conteúdo do Analytics, Início do conteúdo do Heartbeat | Pode ser um usuário que clicou na opção **[!UICONTROL Reproduzir], ou um evento de reprodução automática.** |
| O primeiro quadro da mídia é reproduzido. | `trackPlay` | Heartbeat Content Play | Esse método aciona o timer. Os heartbeats são enviados a cada 10 segundos durante toda a reprodução. |
| O conteúdo é reproduzido. |  | Content Heartbeats |  |
| A sessão foi encerrada. | `trackSessionEnd` |  | `SessionEnd` significa o fim de uma sessão de exibição. Essa API deve ser chamada mesmo se o usuário não consumir a mídia para concluir. |

## Parâmetros {#section_D52B325B99DA42108EF560873907E02C}

Diversos valores observados nas Chamadas do Adobe Analytics Content Start estarão presentes nas Chamadas do Heartbeat Content Start. Você também verá muitos outros parâmetros que a Adobe usa para preencher os diversos relatórios de Mídia no Adobe Analytics. Não falaremos de todos aqui; apenas os mais importantes.

### Heartbeat Content Start

| Parâmetro | Valor | Notas |
|---|---|---|
| `s:sc:rsid` | &lt;ID do conjunto de relatórios da Adobe&gt; |  |
| `s:sc:tracking_serve` | &lt;URL do servidor de rastreamento do Analytics&gt; |  |
| `s:user:mid` | `s:user:mid` | Deve corresponder ao valor médio da Chamada de início de conteúdo do Adobe Analytics |
| `s:event:type` | "start" |  |
| `s:asset:type` | "main" |  |
| `s:asset:mediao_id` | &lt; Nome da mídia &gt; |  |
| `s:stream:type` | live |  |
| `s:meta:*` | opcional | Metadados personalizados definidos na mídia |

## Content Heartbeats {#section_7B387303851A43E5993F937AE2B146FE}

Durante a reprodução da mídia, há um temporizador que envia uma ou mais pulsações (ou pings) a cada 10 segundos para o conteúdo principal e a cada segundo para anúncios. Esses heartbeats contêm informações sobre reprodução, anúncios, buffers e outros itens. O conteúdo exato de cada heartbeat está além do escopo deste documento. É importante validar o acionamento das pulsações de modo consistente durante a reprodução.

Em heartbeats de conteúdo, procure por itens específicos:

| Parâmetro | Valor | Notas |
|---|---|---|
| `s:event:type` | "play" |  |
| `l:event:playhead` | &lt;posição do indicador de reprodução&gt;, por exemplo, 50, 60, 70 | Isso deve refletir a posição atual do indicador de reprodução. |

## Heartbeat Content Complete {#section_2CA970213AF2457195901A93FC9D4D0D}

Não haverá uma chamada completa neste cenário porque o streaming ao vivo nunca foi concluído.

## Configurações de valor do indicador de reprodução

Para fluxos ao vivo, é necessário definir o indicador de reprodução para um deslocamento a partir do momento em que a programação começou, para que nos relatórios, os analistas possam determinar em que ponto os usuários estão entrando e saem do stream ao vivo em uma visualização de 24 horas.

### No início

Para a mídia LIVE, quando um usuário começa a reproduzir o fluxo, é necessário definir `l:event:playhead` para o deslocamento atual, em segundos. Isso é oposto ao VOD, onde você define o indicador de reprodução como "0".

Por exemplo, digamos que um evento de streaming ao vivo começa à meia-noite e execute por 24 horas (`a.media.length=86400`;; `l:asset:length=86400`). Em seguida, digamos que um usuário comece a reproduzir esse transmissão ao vivo às 12:00 horas. Nesse cenário, você deve definir `l:event:playhead` como 43200 (12 horas no fluxo).

### Pausar

A mesma lógica de "indicador de reprodução ao vivo" aplicada no início da reprodução deve ser aplicada quando um usuário pausar a reprodução. Quando o usuário retorna para reproduzir o fluxo ao vivo, é necessário definir o `l:event:playhead` valor para a nova posição do indicador de reprodução deslocamento, _não_ para o ponto em que o usuário pausou o stream ao vivo.

## Código de exemplo {#section_vct_j2j_x2b}

![](assets/live-content-playback.png)

### Android

Veja a ordem de chamada da API esperada:

```java
// Set up mediaObject 
MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.LIVE 
); 

HashMap<String, String> mediaMetadata = new HashMap<String, String>(); 
mediaMetadata.put(CUSTOM_VAL_1, CUSTOM_KEY_1); 
mediaMetadata.put(CUSTOM_VAL_2, CUSTOM_KEY_2); 

// 1. Call trackSessionStart() when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback.  
_mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the first  
//    frame of main content is rendered on the screen. 
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackSessionEnd() when user ends the playback session.  
//    Since the user does not watch live media to completion, there  
//    is no need to call trackComplete().  
_mediaHeartbeat.trackSessionEnd(); 
....... 
....... 
```

### iOS

Veja a ordem de chamada da API esperada:

```
// Set up mediaObject 
ADBMediaObject *mediaObject =  
[ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                   length:MEDIA_LENGTH  
                   streamType:ADBMediaHeartbeatStreamTypeLIVE]; 
 
NSMutableDictionary *mediaContextData = [[NSMutableDictionary alloc] init]; 
[mediaContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
[mediaContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
 
// 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback. 
[_mediaHeartbeat trackSessionStart:mediaObject data:mediaContextData]; 
...... 
...... 
 
// 2. Call trackPlay when the playback actually starts, i.e., when the first  
//    frame of the main content is rendered on the screen. 
[_mediaHeartbeat trackPlay]; 
....... 
....... 
 
// 3. Call trackSessionEnd when user ends the playback session. Since the user  
//    does not watch live media to completion, there is no need to call  
//    trackComplete. 
[_mediaHeartbeat trackSessionEnd]; 
........ 
........ 
```

### JavaScript

Veja a ordem de chamada da API esperada:

```js
// Set up mediaObject 
var mediaInfo =  
MediaHeartbeat.createMediaObject(Configuration.MEDIA_NAME,  
                                 Configuration.MEDIA_ID,  
                                 Configuration.MEDIA_LENGTH,  
                                 MediaHeartbeat.StreamType.VOD); 

var mediaMetadata = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 
}; 

// 1. Call trackSessionStart() when Play is clicked or if autoplay  
//    is used, i.e., there's an intent to start playback. 
this._mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the  
//    first frame of media is rendered on the screen. 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackSessionEnd() when user ends the playback session.  
//    Since user does not watch live media to completion, there is  
//    no need to call trackComplete(). 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........ 
```

