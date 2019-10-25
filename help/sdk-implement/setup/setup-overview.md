---
seo-title: Visão geral da configuração
title: Visão geral da configuração
uuid: 06fefedb-b0c8-4f7d-90c8-e374cdde1695
translation-type: tm+mt
source-git-commit: ffb97a0162e0bb609ea427afab81e4d8b532f20b

---


# Visão geral da configuração{#setup-overview}

>[!IMPORTANT]
>
>As instruções a seguir se aplicam aos SDKs de mídia 2.x. Se estiver implementando uma versão 1.x do SDK do Media, consulte a [Documentação do SDK do Media 1.x.](/help/sdk-implement/download-sdks.md) Para integradores do Primetime, consulte Documentação _do SDK do_ Primetime Media abaixo.


## Suporte mínimo para versão da plataforma {#minimum-platform-version}

A tabela a seguir descreve as versões mínimas da plataforma compatíveis com cada SDK, a partir de 19 de fevereiro de 2019.

| SO/Navegador | Versão mín necessária |
| --- | --- |
| iOS | iOS 6+ |
| Android | Android 5.0+ - pirulito |
| Chrome | v22+ |
| Mozilla | v27+ |
| Safari | v7+ |
| IE | v11+ |

## Diretrizes de implementação gerais {#general-implementation-guidelines}

Existem três componentes principais do SDK envolvidos no rastreamento de mídia:
* Configuração do Heartbeat de mídia - contém as configurações básicas para a geração de relatórios.
* Delegação do Heartbeat de mídia - o representante controla o tempo de reprodução e o objeto QoS.
* Heartbeat de mídia - a biblioteca principal que contém membros e métodos.

Complete as seguintes etapas de implementação:

1. Create a `MediaHeartbeatConfig` instance and set your config parameter values.

   |  Nome da variável  | Descrição  | Obrigatório |  Valor padrão  |
   |---|---|:---:|---|
   | `trackingServer` | Servidor de rastreamento para o Media Analytics. É diferente do seu servidor de monitoramento do Analytics. | Sim | Sequência de caracteres vazia |
   | `channel` | Nome do canal | Não | Sequência de caracteres vazia |
   | `ovp` | Nome da plataforma de mídia online pela qual o conteúdo é distribuído | Não | Sequência de caracteres vazia |
   | `appVersion` | Versão do aplicativo/SDK do reprodutor de mídia | Não | Sequência de caracteres vazia |
   | `playerName` | Nome do reprodutor de vídeo em uso, por exemplo, "AVPlayer", "HTML5 Player", "My Custom Player" | Não | Sequência de caracteres vazia |
   | `ssl` | Indica se as chamadas devem ser efetuadas por HTTPS | Não | false |
   | `debugLogging` | Indica se o log de depuração está ativado | Não | false |

1. Implementar o `MediaHeartbeatDelegate`.

   |  Nome do método  |  Descrição  | Obrigatório |
   | --- | --- | :---: |
   | `getQoSObject()` | Retorna a instância `MediaObject` que contém as informações de QoS atuais. Esse método será chamado várias vezes durante uma sessão de reprodução. A implementação do reprodutor sempre deve retornar os dados de QoS mais recentes. | Sim |
   | `getCurrentPlaybackTime()` | Retorna a posição atual do indicador de reprodução. Para rastreamento VOD, o valor é especificado em segundos a partir do início do item de mídia. Para rastreamento LINEAR/LIVE, o valor é especificado em segundos a partir do início do programa. | Sim |

   >[!TIP]
   >
   >O objeto Quality of Service (QoS) é opcional. Se os dados de QoS estiverem disponíveis para o seu reprodutor e você desejar rastreá-los, as seguintes variáveis serão necessárias:

   | Nome da variável | Descrição  | Obrigatório |
   | --- | --- | :---: |
   | `bitrate` | A taxa de bits da mídia, em bits por segundo. | Sim |
   | `startupTime` | A hora de inicialização da mídia, em milissegundos. | Sim |
   | `fps` | Os quadros exibidos por segundo. | Sim |
   | `droppedFrames` | O número de quadros ignorados até o momento. | Sim |

1. Create the `MediaHeartbeat` instance.

   Use the `MediaHertbeatConfig` and `MediaHertbeatDelegate` to create the `MediaHeartbeat` instance.

   >[!IMPORTANT]
   >
   >Make sure that your `MediaHeartbeat` instance is accessible and does not get deallocated until the end of the session. Essa instância será usada para todos os eventos de rastreamento de mídia a seguir.

   >[!TIP]
   >
   >`MediaHeartbeat` requer uma instância de `AppMeasurement` para enviar chamadas ao Adobe Analytics.

1. Combine todas as partes.

   O código de exemplo a seguir usa o SDK do JavaScript 2.x para um reprodutor de vídeo HTML5:

   ```javascript
   // Create local references to the heartbeat classes 
   var MediaHeartbeat = ADB.va.MediaHeartbeat; 
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig; 
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate; 
   
   //Media Heartbeat Config 
   var mediaConfig = new MediaHeartbeatConfig(); 
   mediaConfig.trackingServer = "[your_namespace].hb.omtrdc.net"; 
   mediaConfig.playerName = "HTML5 Basic"; 
   mediaConfig.channel = "Video Channel"; 
   mediaConfig.debugLogging = true; 
   mediaConfig.appVersion = "2.0"; 
   mediaConfig.ssl = false; 
   mediaConfig.ovp = ""; 
   
   // Media Heartbeat Delegate 
   var mediaDelegate = new MediaHeartbeatDelegate(); 
   
   // Set mediaDelegate CurrentPlaybackTime 
   mediaDelegate.getCurrentPlaybackTime = function() { 
       return video.currentTime; 
   }; 
   
   // Set mediaDelegate QoSObject - OPTIONAL 
   mediaDelegate.getQoSObject = function() { 
       return MediaHeartbeat.createQoSObject(video.bitrate,  
                                             video.startuptime,  
                                             video.fps,  
                                             video.droppedframes); 
   } 
   // Create mediaHeartbeat instance      
   this.mediaHeartbeat =  
     new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurementInstance);  
   ```

## Validar {#validate}

As implementações de rastreamento do Media Analytics geram dois tipos de chamadas de rastreamento:

* As chamadas de Media e ad Start são enviadas diretamente para o servidor Adobe Analytics (AppMeasurement).
* As chamadas de pulsação são enviadas para o servidor de rastreamento do Media Analytics (pulsações), processadas e repassadas para o servidor do Adobe Analytics.

* **Servidor** do Adobe Analytics (AppMeasurement) Para obter mais informações sobre as opções do servidor de rastreamento, consulte Preencher [corretamente as variáveis trackingServer e trackingServerSecure.](https://helpx.adobe.com/analytics/kb/determining-data-center.html)

   >[!IMPORTANT]
   >
   >É necessário um servidor de rastreamento RDC ou uma resolução CNAME para um servidor RDC para o serviço de ID de visitante da Experience Cloud.

   The analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

* ** Servidor do Media Analytics (Heartbeats)**Este sempre tem o formato "`[your_namespace].hb.omtrdc.net`". O valor "`[your_namespace]`" especifica sua empresa e é fornecido pela Adobe.

O rastreamento de mídia funciona da mesma forma em todas as plataformas, desktops e dispositivos móveis. O rastreamento de áudio funciona atualmente em plataformas móveis. Para todas as chamadas de rastreamento, há algumas variáveis universais principais que precisam ser validadas:

## Documentação do SDK 1.x {#sdk-1x-documentation}

| SDKs 1.x do Video Analytics |  Guias do desenvolvedor (somente PDFs) |
| --- | --- |
| Android | [Configurar para Android ](vhl-dev-guide-v15_android.pdf) |
| Apple TV | [Configurar para Apple TV ](vhl-dev-guide-v1x_appletv.pdf) |
| Chromecast | [Configurar para Chromecast ](chromecast_1.x_sdk.pdf) |
| iOS | [Configurar para iOS ](vhl-dev-guide-v15_ios.pdf) |
| JavaScript | [Configurar para JavaScript ](vhl-dev-guide-v15_js.pdf) |
| Primetime | <ul> <li> Android:   [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/android/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> DHLS:   [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/dhls/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> iOS:   [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> </ul> |
| TVML | [Configurar para TVML ](vhl_tvml.pdf) |

## Documentação de SDK do Media do Primetime {#primetime-docs}

* [Guias do usuário do Primetime](https://helpx.adobe.com/primetime/user-guide.html)
