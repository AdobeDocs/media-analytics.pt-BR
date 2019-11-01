---
title: Rastreamento da reprodução principal no iOS
description: Este tópico descreve como implementar o rastreamento principal usando o SDK de mídia no iOS.
uuid: bdc0e05c-4fe5-430e-aee2-f331bc59ac6b
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Rastreamento da reprodução principal no iOS{#track-core-playback-on-ios}

>[!IMPORTANT]
>Esta documentação cobre o rastreamento na versão 2.x do SDK. Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores 1.x aqui: [Baixar SDKs](/help/sdk-implement/download-sdks.md).

1. **Configuração de rastreamento inicial**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   API de [createMediaObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)

   | Nome da variável | Descrição | Obrigatório |
   |---|---|---|
   | `name` | Nome do vídeo | Sim |
   | `mediaid` | Identificador exclusivo do vídeo | Sim |
   | `length` | Duração do vídeo | Sim |
   | `streamType` | Tipo de fluxo (consulte Constantes _de_ StreamType abaixo) | Sim |
   | `mediaType` | Tipo de mídia (consulte as constantes __ MediaType abaixo) | Sim |

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

   Como opção, anexe objetos de metadados de vídeo padrão e/ou personalizados à sessão de rastreamento de vídeo por meio de variáveis de dados de contexto.

   * **Metadados de vídeo padrão**

      * [Implementar metadados padrão no iOS](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
      * **Chaves de metadados de vídeo**
         [Chaves de metadados de iOS](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

      * Consulte a lista completa de metadados de vídeo aqui: [Parâmetros de áudio e vídeo](/help/metrics-and-metadata/audio-video-parameters.md)
      >[!NOTE]
      >
      >Anexar o objeto de metadados de vídeo padrão ao objeto de mídia é opcional.

   * **Metadados personalizados**

      Crie um objeto variável para as variáveis personalizadas e preencha com os dados para este vídeo. Por exemplo:

      ```
      NSMutableDictionary *videoMetadata = [[NSMutableDictionary alloc] init]; 
      [videoMetadata setObject:@"false" forKey:@"isUserLoggedIn"]; 
      [videoMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
      ```


1. **Rastrear a intenção de iniciar a reprodução**

   Para começar a rastrear uma sessão de mídia, chame `trackSessionStart` a instância Media Heartbeat.

   >[!TIP]
   >
   >O segundo valor é o nome do objeto de metadados de vídeo personalizado que você criou na etapa 2.

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

1. **Rastrear o início real da reprodução**

   Identifique o evento no reprodutor de vídeo a partir do início da reprodução, onde o primeiro quadro do vídeo é renderizado na tela, e chame `trackPlay`.

   ```
   - (void)onVideoPlay:(NSNotification *)notification { 
       [_mediaHeartbeat trackPlay]; 
   }
   ```

1. **Acompanhar a conclusão da reprodução**

   Identifique o evento no reprodutor de vídeo para a conclusão da reprodução, onde o usuário assistiu ao conteúdo até o fim, e chame `trackComplete`.

   ```
   - (void)onVideoComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackComplete]; 
   }
   ```

1. **Acompanhar o final da sessão**

   Identifique o evento no reprodutor de vídeo para o descarregamento/encerramento da reprodução, onde o usuário fecha o vídeo, e/ou ele é concluído e descarregado, e chame `trackSessionEnd`.

   ```
   - void)onMainVideoUnloaded:(NSNotification *)notification { 
       [_mediaHeartbeat trackSessionEnd]; 
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` marca o fim de uma sessão de rastreamento de vídeo. Se a sessão tiver sido assistida até o final, onde o usuário assistiu ao conteúdo até o fim, verifique se `trackComplete` () é chamado antes de `trackSessionEnd`. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new video tracking session.

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
   >Essa pode ser a mesma fonte de evento usada na Etapa 4. Verifique se cada chamada `trackPause()` da API está emparelhada a uma chamada `trackPlay()` da API quando a reprodução continuar.

Consulte as informações adicionais sobre o rastreamento da reprodução principal:

* Cenários de rastreamento: [Reprodução VOD sem anúncios](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Reprodutor de exemplo incluído com o SDK do iOS para um exemplo completo de rastreamento.

