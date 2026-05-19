---
title: Explicação sobre a implementação de SDKs de mídia
description: Saiba como configurar o Media SDK para rastreamento de mídia em seus aplicativos móveis, OTT e do navegador (JS).
uuid: 06fefedb-b0c8-4f7d-90c8-e374cdde1695
exl-id: a175332e-0bdc-44aa-82cb-b3f879e7abfc
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/DsVDPsePWd123v5D8OdC2zUn52IWAOwh6QxcpvB1FIs
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: c8add8f2-4250-4fd9-9cde-9707036c567d
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 626
ht-degree: 81%

---

# Herdados - Visão geral da configuração do SDK de mídia {#setup-overview}

Após baixar o SDK de mídia para seu aplicativo de vídeo ou player, siga as informações desta seção para configurar e implementar o SDK de mídia.


## Diretrizes gerais de implementação {#general-implementation-guidelines}

Há três componentes principais do SDK usados no rastreamento com os serviços de mídia de transmissão:
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
   | `debugLogging` | Indica se o registro de depuração está habilitado | Não | false |

1. Implementar o `MediaHeartbeatDelegate`.

   |  Nome do método  |  Descrição  | Obrigatório |
   | --- | --- | :---: |
   | `getQoSObject()` | Retorna a instância `MediaObject` que contém as informações de QoS atuais. Esse método será chamado várias vezes durante uma sessão de reprodução. A implementação do player sempre deve retornar os dados de QoS mais recentes. | Sim |
   | `getCurrentPlaybackTime()` | Retorna a posição atual do indicador de reprodução. <br /> Para rastreamento VOD, o valor é especificado em segundos a partir do início do item de mídia. <br /> Para transmissões ao vivo, se o player não fornecer informações sobre a duração do conteúdo, o valor pode ser especificado como o número de segundos desde a meia-noite UTC daquele dia. <br /> Observação: ao usar marcadores de progresso, a duração do conteúdo é necessária e o indicador de reprodução precisa ser atualizado para o número de segundos desde o início do item de mídia, começando com 0. | Sim |

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

## Validar {#validate}

As implementações de rastreamento do Media Analytics geram dois tipos de chamadas de rastreamento:

* Chamadas de início de mídia e anúncio são enviadas diretamente para o servidor do Adobe Analytics (AppMeasurement).
* As chamadas de heartbeat são enviadas para o servidor de rastreamento do Media Analytics (heartbeats), processadas e repassadas para o servidor do Adobe Analytics.

* **Servidor do Adobe Analytics (AppMeasurement)**
Para obter mais informações sobre as opções do servidor de rastreamento, consulte [Preencher corretamente as variáveis trackingServer e trackingServerSecure.](https://helpx.adobe.com/br/analytics/kb/determining-data-center.html)

  >[!IMPORTANT]
  >
  >Um servidor de rastreamento RDC, ou CNAME que é resolvido para um servidor RDC, é necessário para o serviço de ID do visitante da Experience Cloud.

  O servidor de rastreamento do Analytics deve terminar com “`.sc.omtrdc.net`” ou ser um CNAME.

* **&#x200B; Servidor do Media Analytics (Heartbeats)**
Este sempre tem o formato &quot;`[your_namespace].hb.omtrdc.net`&quot;. O valor &quot;`[your_namespace]`&quot; especifica sua empresa e é fornecido pela Adobe.

O rastreamento de mídia funciona da mesma forma em todas as plataformas, desktops e dispositivos móveis. O rastreamento de áudio funciona atualmente em plataformas móveis. Para todas as chamadas de rastreamento, há algumas variáveis universais principais que precisam ser validadas:
