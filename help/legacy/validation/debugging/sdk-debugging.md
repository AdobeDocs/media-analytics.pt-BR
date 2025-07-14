---
title: Depuração do SDK
description: Saiba mais sobre o rastreamento/registro disponível no SDK de mídia.
uuid: a5972d87-c593-4b4f-a56f-dca6e25268e1
exl-id: c2de6454-8538-4d07-a099-e278b153d894
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Depuração do SDK {#sdk-debugging}

Você pode ativar e desativar o registro. O SDK do Media fornece um mecanismo abrangente de rastreamento/registro em toda a pilha de rastreamento de mídia. Você pode ativar ou desativar o registro, definindo o sinalizador `debugLogging` no objeto de configuração.

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

## Mensagens de registro

As mensagens de registro seguem este formato:

```js
Format: [<timestamp>] [<level>] [<tag>] [<message>]
Example: [16:10:29 GMT­0700 (PDT).245] [DEBUG] [plugin::player] Resolving qos.startupTime: 0
```

* **carimbo de data e hora:** este é o horário atual da CPU (fuso horário GMT)
* **nível:** há 4 níveis de mensagem definidos:
   * INFO - Normalmente, os dados de entrada do aplicativo (validar o nome do player, ID do vídeo etc.)
   * DEPURAR - Logs de depuração, usados pelos desenvolvedores para depurar problemas mais complexos
   * AVISO - Indica possíveis erros de integração/configuração ou bugs do SDK do Heartbeats
   * ERRO - Indica erros importantes de integração ou bugs do SDK do Heartbeats
* **tag:** O nome do subcomponente que emitiu a mensagem de registro (geralmente o nome da classe)
* **mensagem:** a mensagem de rastreamento real

Você pode usar a saída dos registros pela biblioteca do SDK do Media para verificar a implantação. Uma boa estratégia é pesquisar nos registros a sequência de caracteres `#track`. Isso destacará todas as chamadas `track*()` feitas pelo seu aplicativo.

Por exemplo, registros filtrados por `#track` podem ter a seguinte aparência:

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
