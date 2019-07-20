---
seo-title: Visão geral da configuração
title: Visão geral da configuração
uuid: 06 fefedb-b 0 c 8-4 f 7 d -90 c 8-e 374 cdde 1695
translation-type: tm+mt
source-git-commit: 63fb6332694675cd03843995f8f86ae45973d399

---


# Setup Overview{#setup-overview}

>[!IMPORTANT]
>
>As instruções a seguir se aplicam aos 2. x Media sdks. Se estiver implementando uma versão 1.x do SDK do Media, consulte a [Documentação do SDK do Media 1.x.](../download-sdks.md) Para integradores do Primetime, consulte _a Documentação_ do Primetime Media SDK abaixo.


## Minimum Platform Version Support {#minimum-platform-version}

A tabela a seguir descreve as versões mínimas de plataforma compatíveis com cada SDK, a partir de 19 de fevereiro de 29 19.

| Sistema operacional/Navegador | Versão mínima exigida |
| --- | --- |
| iOS | iOS 6+ |
| Android | Android 5.0 + - Lollipop |
| Chrome | v 22 + |
| Mozilla | v 27 + |
| Safari | v 7 + |
| IE | v 11 + |

## Diretrizes de implementação gerais {#section_965A3B699A8248DDB9B2B3EA3CC20E41}

Existem três componentes principais do SDK envolvidos no rastreamento de mídia:
* Configuração do Heartbeat de mídia - contém as configurações básicas para a geração de relatórios.
* Delegação do Heartbeat de mídia - o representante controla o tempo de reprodução e o objeto QoS.
* Heartbeat de mídia - a biblioteca principal que contém membros e métodos.

Conclua as seguintes etapas de implementação:

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

1. Implement the `MediaHeartbeatDelegate`.

   |  Nome do método  |  Descrição  | Obrigatório |
   | --- | --- | :---: |
   | `getQoSObject()` | Retorna a instância `MediaObject` que contém as informações de QoS atuais. Esse método será chamado várias vezes durante uma sessão de reprodução. A implementação do reprodutor sempre deve retornar os dados de QoS mais recentes. | Sim |
   | `getCurrentPlaybackTime()` | Retorna a posição atual do indicador de reprodução. Para rastreamento VOD, o valor é especificado em segundos a partir do início do item de mídia. Para rastreamento LINEAR/LIVE, o valor é especificado em segundos a partir do início do programa. | Sim |

   >[!TIP]
   >
   >O objeto de Qualidade do serviço (qos) é opcional. Se os dados de QoS estiverem disponíveis para o seu reprodutor e você desejar rastreá-los, as seguintes variáveis serão necessárias:

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
   >`MediaHeartbeat` requer uma instância de `AppMeasurement` envio de chamadas para o Adobe Analytics.

1. Combine todas as partes.

   O código de exemplo a seguir usa o SDK do JavaScript 2.x para um reprodutor de vídeo HTML5:

   ```javascript
   // Create local references to the heartbeat classes 
   var MediaHeartbeat = ADB.va.MediaHeartbeat; 
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig; 
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate; 
   
   //Media Heartbeat Config 
   var mediaConfig = new MediaHeartbeatConfig(); 
   mediaConfig.trackingServer = "namespace.hb.omtrdc.net"; 
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

## Validar {#section_D4D46F537A4E442B8AB0BB979DDAA4CC}

As implementações de mídia são compostas por dois tipos de chamadas de rastreamento:

* Chamadas de Início de mídia e anúncio são enviadas diretamente para o servidor AppMeasurement.
* As chamadas do Heartbeat são enviadas para o servidor de rastreamento do Heartbeat no início, a cada dez segundos para o conteúdo e a cada segundo para os anúncios.

O rastreamento de mídia funciona da mesma forma em todas as plataformas, desktops e dispositivos móveis. O rastreamento automático funciona atualmente em plataformas móveis. Para todas as chamadas de rastreamento, há algumas variáveis universais principais que precisam ser validadas:

* **AppMeasurement (Analytics)**
Para obter mais informações sobre como rastrear as opções do servidor, consulte [Preencher corretamente as variáveis trackingServer e trackingServerSecure.](https://marketing.adobe.com/resources/help/kb/en_US/analytics/kb/determining-data-center.html)

   >[!IMPORTANT]
   >
   >É necessário um servidor de rastreamento RDC ou CNAME resolver a um servidor RDC para o serviço de ID de visitante da Experience Cloud.

   The analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

* **Heartbeats (Media Analytics)**
Sempre tem o formato "`[namespace].hb.omtrdc.net`, onde"`[namespace]`é definido pela empresa de logon e é fornecido pela Adobe.

## SDK 1.x Documentation {#section_acj_tkk_t2b}

| Video Analytics 1. x sdks  | Guias do desenvolvedor (somente pdfs) |
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
