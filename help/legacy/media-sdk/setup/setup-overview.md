---
title: Explicação sobre a implementação de SDKs de mídia
description: Saiba como configurar o SDK de mídia para rastreamento de mídia em seus aplicativos para dispositivos móveis, OTT e do navegador (JS).
uuid: 06fefedb-b0c8-4f7d-90c8-e374cdde1695
exl-id: a175332e-0bdc-44aa-82cb-b3f879e7abfc
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 94%

---

# Herdados - Visão geral da configuração do SDK de mídia {#setup-overview}

Após baixar o SDK de mídia para seu aplicativo de vídeo ou player, siga as informações desta seção para configurar e implementar o SDK de mídia.


## Diretrizes gerais de implementação {#general-implementation-guidelines}

Há três componentes principais do SDK usados no rastreamento com o complemento Coleção de mídia de transmissão:
* Configuração do Heartbeat de mídia - O `MediaHeartbeatConfig` contém as configurações básicas para relatórios.
* Delegar Heartbeat de mídia - O `MediaHeartbeatDelegate` controla o tempo de reprodução e o objeto QoS.
* Heartbeat de mídia - O `MediaHeartbeat` é a biblioteca principal que contém membros e métodos.

## Implementar o SDK de mídia de streaming

Para configurar e usar o SDK de mídia de streaming, conclua as seguintes etapas de implementação:

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
   | `getCurrentPlaybackTime()` | Retorna a posição atual do indicador de reprodução. <br /> Para rastreamento de VOD, o valor é especificado em segundos a partir do início do item de mídia. <br /> Para transmissões ao vivo, se o player não fornecer informações sobre a duração do conteúdo, o valor pode ser especificado como o número de segundos desde a meia-noite UTC daquele dia. <br /> Observação: ao usar marcadores de progresso, a duração do conteúdo é necessária e o indicador de reprodução precisa ser atualizado para o número de segundos desde o início do item de mídia, começando com 0. | Sim |

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
