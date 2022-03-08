---
title: Implementar SDKs do Media explicados
description: '"Saiba como configurar o SDK do Media para rastreamento de mídia em aplicativos móveis, OTT e do navegador (JS)."'
uuid: 06fefedb-b0c8-4f7d-90c8-e374cdde1695
exl-id: a175332e-0bdc-44aa-82cb-b3f879e7abfc
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 165c7f01a2d2c32df518c89a5c49637107d41086
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 89%

---

# Visão geral da configuração{#setup-overview}

As instruções a seguir se aplicam aos SDKs do Media 2.x. Se estiver implementando uma versão 1.x do SDK do Media, consulte a [Documentação do SDK do Media 1.x.](/help/sdk-implement/download-sdks.md) Para obter os integradores do Primetime, consulte a _Documentação de SDK do Media do Primetime_ abaixo.

>[!IMPORTANT]
>
>Com o fim do suporte para SDKs móveis da versão 4 em 31 de agosto de 2021, a Adobe também encerrará o suporte para o SDKs do Media Analytics para iOS e Android.  Para obter mais informações, consulte [Perguntas frequentes sobre o fim do suporte do SDK do Media Analytics](/help/sdk-implement/end-of-support-faqs.md).


## Suporte mínimo para versão da plataforma {#minimum-platform-version}

A tabela a seguir descreve as versões mínimas da plataforma compatíveis com cada SDK, a partir de 19 de fevereiro de 2019.

| OS/Navegador | Versão mín. necessária |
| --- | --- |
| iOS | iOS 6+ |
| Android | Android 5.0+ - Lollipop |
| Chrome | v22+ |
| Mozilla | v27+ |
| Safari | v7+ |
| IE | v11+ |

## Diretrizes de implementação gerais {#general-implementation-guidelines}

Há três componentes principais do SDK envolvidos no rastreamento de mídia:
* Config Media Heartbeat - A configuração contém as configurações básicas do relatórios.
* Delegar Media Heartbeat - O delegado controla o tempo de reprodução e o objeto QoS.
* Media Heartbeat - A biblioteca principal que contém membros e métodos.

Complete as etapas de implementação a seguir:

1. Crie uma instância `MediaHeartbeatConfig` e defina os valores do parâmetro de configuração.

   |  Nome da variável  | Descrição  | Obrigatório |  Valor padrão  |
   |---|---|:---:|---|
   | `trackingServer` | Servidor de rastreamento para análise de mídia. Isso é diferente do servidor de rastreamento de análise. | Sim | String vazia |
   | `channel` | Nome do canal | Não | String vazia |
   | `ovp` | Nome da plataforma de mídia online pela qual o conteúdo é distribuído. | Não | String vazia |
   | `appVersion` | Versão do aplicativo do reprodutor de vídeo/SDK | Não | String vazia |
   | `playerName` | Nome do media player em uso, ou seja, &quot;AVPlayer&quot;, &quot;HTML5 Player&quot;, &quot;My Custom Player&quot; | Não | String vazia |
   | `ssl` | Indica se as chamadas devem ser feitas em HTTPS | Não | false |
   | `debugLogging` | Indica se o registro de depuração está ativado | Não | false |

1. Implementar o `MediaHeartbeatDelegate`.

   |  Nome do método  |  Descrição  | Obrigatório |
   | --- | --- | :---: |
   | `getQoSObject()` | Retorna a instância `MediaObject` que contém as informações de QoS atuais. Esse método será chamado várias vezes durante uma sessão de reprodução. A implementação do player sempre deve retornar os dados de QoS mais recentes. | Sim |
   | `getCurrentPlaybackTime()` | Retorna a posição atual do indicador de reprodução. <br /> Para rastreamento de VOD, o valor é especificado em segundos a partir do início do item de mídia. <br /> Para transmissão ao vivo, se o reprodutor não fornecer informações sobre a duração do conteúdo, o valor pode ser especificado como o número de segundos desde a meia-noite UTC desse dia. <br /> Observação: Ao usar marcadores de progresso, a duração do conteúdo é necessária e o indicador de reprodução precisa ser atualizado como o número de segundos a partir do início do item de mídia, começando com 0. | Sim |

   >[!TIP]
   >
   >O objeto de Qualidade do serviço (QoS) é opcional. Se os dados de QoS estiverem disponíveis para o player e você desejar rastrear esses dados, as seguintes variáveis serão necessárias:

   | Nome da variável | Descrição   | Obrigatório |
   | --- | --- | :---: |
   | `bitrate` | A taxa de bits da mídia em bits por segundo. | Sim |
   | `startupTime` | A hora de início da mídia em milissegundos. | Sim |
   | `fps` | Os quadros exibidos por segundo. | Sim |
   | `droppedFrames` | O número de quadros soltos até agora. | Sim |

1. Crie a instância `MediaHeartbeat`.

   Use `MediaHertbeatConfig` e `MediaHertbeatDelegate` para criar a instância `MediaHeartbeat`.

   >[!IMPORTANT]
   >
   >Certifique-se de que a instância `MediaHeartbeat` possa ser acessada e não seja desalocada até o final da sessão. Essa instância será usada para todos os eventos de rastreamento de mídia a seguir.

   >[!TIP]
   >
   >`MediaHeartbeat` exige uma instância do `AppMeasurement` para enviar chamadas para o Adobe Analytics.

1. Combine todas as partes.

   O código de exemplo a seguir usa o SDK 2.x do JavaScript para um player de vídeo HTML5:

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

## Validar  {#validate}

As implementações de rastreamento do Media Analytics geram dois tipos de chamadas de rastreamento:

* Chamadas de início de mídia e anúncio são enviadas diretamente para o servidor do Adobe Analytics (AppMeasurement).
* As chamadas de heartbeat são enviadas para o servidor de rastreamento do Media Analytics (heartbeats), processadas e repassadas para o servidor do Adobe Analytics.

* **Servidor do Adobe Analytics (AppMeasurement)** Para obter mais informações sobre as opções do servidor de rastreamento, consulte [Preencher corretamente as variáveis trackingServer e trackingServerSecure.](https://helpx.adobe.com/br/analytics/kb/determining-data-center.html)

   >[!IMPORTANT]
   >
   >Um servidor de rastreamento RDC, ou CNAME que é resolvido para um servidor RDC, é necessário para o serviço de ID do visitante da Experience Cloud.

   O servidor de rastreamento do Analytics deve terminar com “`.sc.omtrdc.net`” ou ser um CNAME.

* ** Servidor do Media Analytics (Heartbeats)**
Este sempre tem o formato &quot;`[your_namespace].hb.omtrdc.net`&quot;. O valor &quot;`[your_namespace]`&quot; especifica sua empresa e é fornecido pela Adobe.

O rastreamento de mídia funciona da mesma forma em todas as plataformas, desktops e dispositivos móveis. O rastreamento de áudio funciona atualmente em plataformas móveis. Para todas as chamadas de rastreamento, há algumas variáveis universais principais que precisam ser validadas:

## Documentação do SDK 1.x {#sdk-1x-documentation}

| SDKs do Video Analytics 1.x  |  Guias do desenvolvedor (somente PDFs) |
| --- | --- |
| Android | [Configurar para Android ](vhl-dev-guide-v15_android.pdf) |
| Apple TV | [Configurar para Apple TV ](vhl-dev-guide-v1x_appletv.pdf) |
| Chromecast | [Configurar para Chromecast ](chromecast_1.x_sdk.pdf) |
| iOS | [Configurar para iOS ](vhl-dev-guide-v15_ios.pdf) |
| JavaScript | [Configurar para JavaScript ](vhl-dev-guide-v15_js.pdf) |
| Primetime | <ul> <li> Android: [Configurar o Media Analytics](https://helpx.adobe.com/br/support/primetime.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> DHLS: [Configurar o Media Analytics](https://helpx.adobe.com/br/support/primetime.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> iOS: [Configurar o Media Analytics](https://helpx.adobe.com/br/support/primetime.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> </ul> |
| TVML | [Configurar para TVML ](vhl_tvml.pdf) |

## Documentação de SDK do Media do Primetime {#primetime-docs}

* [Guias do usuário do Primetime](https://helpx.adobe.com/br/support/primetime.html)
