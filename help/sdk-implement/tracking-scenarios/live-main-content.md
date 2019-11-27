---
title: Conteúdo principal disponível
description: Um exemplo de como rastrear o conteúdo ao vivo usando o SDK do Media.
uuid: e92e99f4-c395-48aa-8a30-cbdd2f5fc07c
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Conteúdo principal ao vivo {#live-main-content}

## Cenário {#scenario}

Neste cenário, há um ativo disponível sem anúncios reproduzido por 40 segundos após a entrada na transmissão ao vivo.

| Acionador | Método do Heartbeat | Chamadas de rede | Notas   |
|---|---|---|---|
| Cliques do usuário **[!UICONTROL Reproduzir]** | `trackSessionStart` | Início do conteúdo do Analytics, Início do conteúdo do Heartbeat | Pode ser um usuário que clicou na opção **[!UICONTROL Reproduzir]**, ou um evento de reprodução automática. |
| O primeiro quadro da mídia é reproduzido. | `trackPlay` | Heartbeat Content Play | Esse método aciona o timer. Os heartbeats são enviados a cada 10 segundos durante toda a reprodução. |
| O conteúdo é reproduzido. |  | Content Heartbeats |  |
| A sessão foi encerrada. | `trackSessionEnd` |  | `SessionEnd` significa o fim de uma sessão de exibição. Essa API deve ser chamada mesmo se o usuário não consumir a mídia até o fim. |

## Parâmetros {#parameters}

Diversos valores observados nas Chamadas do Adobe Analytics Content Start estarão presentes nas Chamadas do Heartbeat Content Start. Você também pode observar os outros parâmetros que a Adobe utiliza para preencher os diversos relatórios de mídia no Adobe Analytics. Não falaremos de todos aqui; apenas os mais importantes.

### Heartbeat Content Start

| Parâmetro | Valor | Notas |
|---|---|---|
| `s:sc:rsid` | &lt;ID do conjunto de relatórios da Adobe&gt; |  |
| `s:sc:tracking_serve` | &lt;URL do servidor de rastreamento do Analytics&gt; |  |
| `s:user:mid` | `s:user:mid` | Deve corresponder ao valor médio da Chamada de início de conteúdo do Adobe Analytics |
| `s:event:type` | "start" |  |
| `s:asset:type` | "main" |  |
| `s:asset:mediao_id` | &lt;Seu nome de mídia&gt; |  |
| `s:stream:type` | live |  |
| `s:meta:*` | opcional | Metadados personalizados definidos na mídia |

## Content Heartbeats {#content-heartbeats}

Durante a reprodução da mídia, há um temporizador que enviará um ou mais heartbeats (ou pings) a cada 10 segundos para o conteúdo principal e a cada segundo para os anúncios. Esses heartbeats contêm informações sobre reprodução, anúncios, buffers e outros itens. O conteúdo exato de cada heartbeat está além do escopo deste documento. É importante validar o acionamento das pulsações de modo consistente durante a reprodução.

Em heartbeats de conteúdo, procure por itens específicos:

| Parâmetro | Valor | Notas |
|---|---|---|
| `s:event:type` | "play" |  |
| `l:event:playhead` | &lt;posição do indicador de reprodução&gt;, por exemplo, 50, 60, 70 | Isso deve refletir a posição atual do indicador de reprodução. |

## Heartbeat Content Complete {#heartbeat-content-complete}

Não haverá uma chamada completa neste cenário, porque o streaming ao vivo não foi concluído.

## Configurações de valor do indicador de reprodução

Para fluxos AO VIVO, é necessário definir o indicador de reprodução para um deslocamento de quando a programação começou, para que, nos relatórios, os analistas possam determinar em que ponto os usuários estão entrando e deixando o fluxo ao vivo em uma exibição de 24 horas.

### No início

Para mídia AO VIVO, quando um usuário começa a reproduzir o fluxo, é necessário definir `l:event:playhead` para o deslocamento atual, em segundos. Isso é o oposto ao VOD, no qual você define o indicador de reprodução como "0".

Por exemplo, digamos que um evento de transmissão AO VIVO comece à meia-noite e tenha uma duração de 24 horas (`a.media.length=86400`; `l:asset:length=86400`). Então, digamos que um usuário comece a reproduzir esse fluxo AO VIVO às 12h. Nesse cenário, você deve definir `l:event:playhead` para 43200 (12 horas no stream).

### Ao pausar

A mesma lógica de "indicador de reprodução em tempo real" aplicada no início da reprodução deve ser aplicada quando o usuário pausa a reprodução. Quando o usuário retorna para reproduzir o fluxo AO VIVO, é necessário definir o `l:event:playhead` valor para a nova posição do indicador de reprodução de deslocamento, _não_ para o ponto em que o usuário pausou o fluxo ao vivo.

## Código de exemplo {#sample-code}

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

