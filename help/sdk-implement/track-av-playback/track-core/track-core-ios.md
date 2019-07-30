---
seo-title: Rastreamento da reprodução principal no iOS
title: Rastreamento da reprodução principal no iOS
uuid: bdc 0 e 05 c -4 fe 5-430 e-aee 2-f 331 bc 59 ac 6 b
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Rastreamento da reprodução principal no iOS{#track-core-playback-on-ios}

>[!IMPORTANT]
>Esta documentação aborda o rastreamento na versão 2. x do SDK. Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores 1.x aqui: [Baixar SDKs](/help/sdk-implement/download-sdks.md).

1. **Configuração de rastreamento inicial**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   API de [createMediaObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)

   | Nome da variável | Descrição | Obrigatório |
   |---|---|---|
   | `name` | Nome do vídeo | Sim |
   | `mediaid` | Identificador exclusivo do vídeo | Sim |
   | `length` | Duração do vídeo | Sim |
   | `streamType` | Stream type (see _StreamType constants_ below) | Sim |
   | `mediaType` | Media type (see _MediaType constants_ below) | Sim |

   **`StreamType`constantes:**

   | Nome da constante | Descrição |
   |---|---|
   | `ADBMediaHeartbeatStreamTypeVOD` | Tipo de fluxo para vídeo sob demanda |
   | `ADBMediaHeartbeatStreamTypeLIVE` | Tipo de fluxo para conteúdo LIVE |
   | `ADBMediaHeartbeatStreamTypeLINEAR` | Tipo de fluxo para conteúdos lineares |
   | `ADBMediaHeartbeatStreamTypeAOD` | Tipo de fluxo para áudio sob demanda |
   | `ADBMediaHeartbeatStreamTypeAUDIOBOOK` | Tipo de fluxo para audiobook |
   | `ADBMediaHeartbeatStreamTypePODCAST` | Tipo de fluxo para podcast |

   **`MediaType`constantes:**

   | Nome da constante | Descrição |
   |---|---|
   | `ADBMediaTypeAudio` | Tipo de mídia para fluxos de áudio. |
   | `ADBMediaTypeVideo` | Tipo de mídia para fluxos de vídeo. |

   O formato geral para criar o `MediaObject`:

   ```
   ADBMediaObject *mediaObject =  
     [ADBMediaHeartbeat createMediaObjectWithName:<MEDIA_NAME> 
                                          mediaId:<MEDIA_ID> 
                                           length:<MEDIA_LENGTH>                       
                                       streamType:<STREAM_TYPE> 
                                        mediaType: <MEDIA_TYPE>];
   ```

1. **Anexar metadados de vídeo**

   Como opção, anexe objetos de metadados de vídeo padrão e/ou personalizados à sessão de monitoramento de vídeo por meio das variáveis de dados de contexto.

   * **Metadados de vídeo padrão**

      * [Implementar metadados padrão no iOS](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
      * **Chaves de metadados de vídeo**
         [Chaves de metadados de iOS](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

      * Consulte a lista completa de metadados de vídeo aqui: [Parâmetros de áudio e vídeo](/help/metrics-and-metadata/audio-video-parameters.md)
      >[!NOTE]
      >
      >A anexação do objeto de metadados de vídeo padrão ao objeto de mídia é opcional.

   * **Metadados personalizados**

      Crie um objeto de variável para as variáveis personalizadas e preencha os dados desse vídeo. Por exemplo:

      ```
      NSMutableDictionary *videoMetadata = [[NSMutableDictionary alloc] init]; 
      [videoMetadata setObject:@"false" forKey:@"isUserLoggedIn"]; 
      [videoMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
      ```


1. **Rastrear a intenção de iniciar a reprodução**

   To begin tracking a media session, call `trackSessionStart` on the Media Heartbeat instance.

   >[!TIP]
   >
   >O segundo valor é o nome de objeto de metadados de vídeo personalizado que você criou na etapa 2.

   ```
   - (void)onMainVideoLoaded:(NSNotification *)notification { 
   //    [_mediaHeartbeat trackSessionStart:mediaObject data:nil]; 
       [_mediaHeartbeat trackSessionStart:mediaObject data:videoMetadata]; 
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` rastreia a intenção de reproduzir do usuário e não o início da reprodução. Essa API é utilizada para carregar os dados/metadados de vídeo e estimar a métrica de tempo do início de QoS (duração entre `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >
   >If you are not using custom video metadata, simply send an empty object for the `data` argument in `trackSessionStart`, as shown in the commented out line in the iOS example above.

1. **Rastrear o início da reprodução atual**

   Identifique o evento no reprodutor de vídeo a partir do início da reprodução, onde o primeiro quadro do vídeo é renderizado na tela, e chame `trackPlay`.

   ```
   - (void)onVideoPlay:(NSNotification *)notification { 
       [_mediaHeartbeat trackPlay]; 
   }
   ```

1. **Rastrear a conclusão da reprodução**

   Identifique o evento no reprodutor de vídeo para a conclusão da reprodução, onde o usuário assistiu ao conteúdo até o fim, e chame `trackComplete`.

   ```
   - (void)onVideoComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackComplete]; 
   }
   ```

1. **Rastrear o final da sessão**

   Identifique o evento no reprodutor de vídeo para o descarregamento/encerramento da reprodução, onde o usuário fecha o vídeo, e/ou ele é concluído e descarregado, e chame `trackSessionEnd`.

   ```
   - void)onMainVideoUnloaded:(NSNotification *)notification { 
       [_mediaHeartbeat trackSessionEnd]; 
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` marca o fim de uma sessão de monitoramento de vídeo. Se a sessão tiver sido assistida até o final, onde o usuário assistiu ao conteúdo até o fim, verifique se `trackComplete` () é chamado antes de `trackSessionEnd`. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new video tracking session.

1. **Rastrear todos os cenários de pausa possíveis**

   Identifique o evento no reprodutor de vídeo para vídeos pausados e chame `trackPause`:

   ```
   - (void)onVideoPause:(NSNotification *)notification { 
       [_mediaHeartbeat trackPause]; 
   }
   ```

   **Pausar cenários**

   Identify any scenario in which the Video Player will pause and make sure that `trackPause` is properly called. Os seguintes cenários exigem que o aplicativo chame `trackPause()`:

   * O usuário clica explicitamente em Pausar no aplicativo.
   * O reprodutor se coloca no estado Pausado.
   * (*Aplicativos móveis*) - O usuário coloca o aplicativo em segundo plano, mas você deseja que o aplicativo mantenha a sessão aberta.
   * (*Aplicativos móveis*) - Qualquer tipo de interrupção de sistema que ocorra e faça com que um aplicativo seja colocado em segundo plano. Por exemplo, o usuário recebe uma chamada ou um pop-up de outro aplicativo ocorre, mas você deseja que o aplicativo mantenha a sessão ativa para que o usuário possa retomar o vídeo do ponto em que foi interrompido.

1. Identifique o evento do reprodutor para reprodução e/ou continuação do vídeo a partir da pausa e chame `trackPlay`:

   ```
   - (void)onVideoPlay:(NSNotification *)notification { 
       [_mediaHeartbeat trackPlay]; 
   }
   ```

   >[!TIP]
   >
   >Pode ser a mesma fonte de evento usada na Etapa 4. Verifique se cada chamada `trackPause()` da API está emparelhada a uma chamada `trackPlay()` da API quando a reprodução continuar.

Consulte as informações adicionais sobre o rastreamento da reprodução principal:

* Cenários de rastreamento: [Reprodução VOD sem anúncios](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Reprodutor de exemplo incluído com o SDK do iOS para um exemplo completo de rastreamento.

