---
seo-title: Depuração do SDK
title: Depuração do SDK
uuid: a5972d87-c593-4b4f-a56f-dca6e25268e1
translation-type: tm+mt
source-git-commit: f2b08663a928e27625a9ff63f783c510f41e7a8c

---


# Depuração do SDK{#sdk-debugging}

Você pode ativar e desativar o registro. O SDK de mídia fornece um mecanismo abrangente de rastreamento/registro em toda a pilha de rastreamento de mídia. You can enable or disable logging by setting the `debugLogging` flag on the Config object.

## Exemplo de código para o log de depuração

### Android

```java
// Media Heartbeat initialization 
MediaHeartbeatConfig config = new MediaHeartbeatConfig(); 
config.debugLogging = true; 

// Use this space for setting other config values 
MediaHeartbeat _heartbeat = new MediaHeartbeat(this, config); 
```

### iOS

```
// Media Heartbeat Initialization 
ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init]; 
config.debugLogging = YES; 

// Use this space for setting other config values 
ADBMediaHeartbeat *_mediaHeartbeat =  
[[ADBMediaHeartbeat alloc] initWithDelegate:self config:config]; 
```

### JavaScript

```js
// Media Heartbeat initialization 
var mediaConfig = new MediaHeartbeatConfig(); 
mediaConfig.debugLogging = true; 
this._mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement); 
```

### OTT (Chromecast, Roku)

A biblioteca ADBMobile fornece o log de depuração pelo método `setDebugLogging`. O log de depuração deve ser definido como `false` para todos os aplicativos de produção.

#### Roku

```
ADBMobile().setDebugLogging(true)
```

#### Chromecast

```
ADBMobile.config.setDebugLogging(true)
```

## Usar o Adobe Bloodhound para testar os aplicativos do Chromecast

Durante o desenvolvimento do aplicativo, o Bloodhound permite exibir localmente chamadas de servidor e, como opção, encaminhar os dados para os servidores de coleta da Adobe. Para obter mais informações sobre Bloodhound, consulte os seguintes guias:

* [Bloodhound 3.x para Mac](https://marketing.adobe.com/resources/help/en_US/mobile/bloodhound/)
* [Bloodhound 2.2 para Windows](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=3&cad=rja&uact=8&ved=0ahUKEwjil9aM87jRAhUExlQKHTYZCjoQFggoMAI&url=https%3A%2F%2Fmarketing.adobe.com%2Fresources%2Fhelp%2Fen_US%2Fmobile%2Fbloodhound_win_2x%2F&usg=AFQjCNEW-gZp1IdbifWFDgDNEaQcGlBobg&sig2=K0waTKxdMj_2kfNXdMI2yg)

>[!IMPORTANT]
>
>A partir de 30 de abril de 2017, o Adobe Bloodhound foi lançado. A partir de 1º de maio de 2017, não serão fornecidos aprimoramentos e suporte adicionais pela engenharia ou pelo Adobe Expert Care.

## Mensagens de registro

As mensagens de registro seguem este formato:

```js
Format: [<timestamp>] [<level>] [<tag>] [<message>] 
Example: [16:10:29 GMT­0700 (PDT).245] [DEBUG] [plugin::player] Resolving qos.startupTime: 0
```

* **timestamp:** esta é a hora atual da CPU (no fuso horário GMT)
* **level:** há 4 níveis de mensagens definidos:
   * INFO - Normalmente, é composto pelos dados de entrada do aplicativo (validar o nome do reprodutor, ID do vídeo, etc.)
   * DEBUG - Registros de depuração usados pelos desenvolvedores para depurar problemas mais complexos
   * WARN - Indica possíveis erros de integração/configuração ou bugs no SDK do Heartbeats
   * ERROR - Indica erros de integração importantes ou bugs do SDK do Heartbeats
* **tag:** o nome do subcomponente que emitiu a mensagem do registro (geralmente, o nome da classe)
* **message:** a mensagem de rastreamento atual

Você pode usar a saída de registros pela biblioteca do SDK de mídia para verificar a implementação. Uma boa estratégia é pesquisar nos registros a sequência de caracteres `#track`. This will highlight all the `track*()` calls made by your application.

For instance, this is what the logs filtered for `#track` could look like:

```js
[16:10:29 GMT­0700 (PDT).222] [INFO] [plugin::player] #trackVideoLoad() 
[16:10:29 GMT­0700 (PDT).230] [INFO] [plugin::player] #trackSessionStart() 
[16:10:29 GMT­0700 (PDT).250] [INFO] [plugin::player] #trackPlay() 
[16:10:29 GMT­0700 (PDT).759] [INFO] [plugin::player] #trackChapterStart() 
[16:10:44 GMT­0700 (PDT).769] [INFO] [plugin::player] #trackAdStart() 
[16:10:59 GMT­0700 (PDT).752] [INFO] [plugin::player] #trackAdComplete() 
[16:10:59 GMT­0700 (PDT).770] [INFO] [plugin::player] #trackChapterStart() 
[16:11:29 GMT­0700 (PDT).734] [INFO] [plugin::player] #trackPause() 
[16:11:29 GMT­0700 (PDT).764] [INFO] [plugin::player] #trackComplete() 
[16:11:29 GMT­0700 (PDT).766] [INFO] [plugin::player] #trackVideoUnload()
```

