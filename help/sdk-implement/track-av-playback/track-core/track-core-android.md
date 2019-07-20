---
seo-title: Rastreamento da reprodução principal no Android
title: Rastreamento da reprodução principal no Android
uuid: ab 5 fab 95-76 ed -4 ae 6-aedb -2 e 66 eece 7607
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# Rastreamento da reprodução principal no Android{#track-core-playback-on-android}

>[!IMPORTANT]
>Esta documentação aborda o rastreamento na versão 2. x do SDK. Se estiver implementando uma versão 1.x do SDK, você pode baixar o Guia dos desenvolvedores 1.x para Android aqui: [Baixar SDKs](../../../sdk-implement/download-sdks.md).

1. **Configuração de rastreamento inicial**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   [API de createMediaObject API](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)

   | Nome da variável | Descrição | Obrigatório |
   | --- | --- | :---: |
   | `name` | Nome da mídia | Sim |
   | `mediaId` | Identificador exclusivo de mídia | Sim |
   | `length` | Comprimento da mídia | Sim |
   | `streamType` | Stream type (see _StreamType constants_ below) | Sim |
   | `mediaType` | Media type (see _MediaType constants_ below) | Sim |

   **`StreamType`constantes:**

   | Nome da constante | Descrição |
   |---|---|
   | `VOD` | Tipo de fluxo para vídeo sob demanda. |
   | `LIVE` | Tipo de fluxo para conteúdo LIVE. |
   | `LINEAR` | Tipo de fluxo para conteúdos lineares. |
   | `AOD` | Tipo de fluxo para áudio sob demanda |
   | `AUDIOBOOK` | Tipo de fluxo para audiobook |
   | `PODCAST` | Tipo de fluxo para podcast |

   **`MediaType`constantes:**

   | Nome da constante | Descrição |
   |---|---|
   | `Audio` | Tipo de mídia para fluxos de áudio. |
   | `Video` | Tipo de mídia para fluxos de vídeo. |

   ```
   MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
     <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);
   ```

1. **Anexar metadados**

   Como opção, anexe objetos de metadados padrão e/ou personalizados à sessão de monitoramento por meio das variáveis de dados de contexto.

   * **Metadados padrão**

      [Implementar metadados padrão no Android](../../../sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)

      >[!NOTE]
      >
      >A anexação do objeto de metadados padronizados ao objeto de mídia é opcional.

      * Referência da API de chaves de metadados da mídia - [Chaves de metadados padrão - Android](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
      * Consulte o conjunto completo de metadados aqui: [Parâmetros de áudio e vídeo](../../../metrics-and-metadata/audio-video-parameters.md)
   * **Metadados personalizados**

      Crie um dicionário para as variáveis personalizadas e preencha os dados para esta mídia. Por exemplo:

      ```java
      HashMap<String, String> mediaMetadata =  
        new HashMap<String, String>(); 
      mediaMetadata.put("isUserLoggedIn", "false"); 
      mediaMetadata.put("tvStation", "Sample TV Station"); 
      mediaMetadata.put("programmer", "Sample programmer");
      ```


1. **Rastrear a intenção de iniciar a reprodução**

   To begin tracking a media session, call `trackSessionStart` on the Media Heartbeat instance. Por exemplo:

   ```java
   public void onVideoLoad(Observable observable, Object data) {  
       _heartbeat.trackSessionStart(mediaInfo, mediaMetadata); 
   }
   ```

   >[!TIP]
   >
   >O segundo valor é o nome do objeto de metadados de mídia personalizado que você criou na etapa 2.

   >[!IMPORTANT]
   >
   >`trackSessionStart` rastreia a intenção de reproduzir do usuário e não o início da reprodução. Essa API é utilizada para carregar os dados/metadados de mídia e estimar a métrica de tempo do início de QoS (duração entre `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >
   >If you are not using custom media metadata, simply send an empty object for the second argument in `trackSessionStart`.

1. **Rastrear o início da reprodução atual**

   Identify the event from the media player for the beginning of the media playback, where the first frame of the media is rendered on the screen, and call `trackPlay`:

   ```java
   // Video is rendered on the screen) and call trackPlay.  
   public void onVideoPlay(Observable observable, Object data) { 
       _heartbeat.trackPlay(); 
   }
   ```

1. **Rastrear a conclusão da reprodução**

   Identify the event from the media player for the completion of the media playback, where the user has watched the content until the end, and call `trackComplete`:

   ```java
   public void onVideoComplete(Observable observable, Object data) { 
       _heartbeat.trackComplete(); 
   }
   ```

1. **Rastrear o final da sessão**

   Identify the event from the media player for the unloading/closing of the media playback, where the user closes the media and/or the media is completed and has been unloaded, and call `trackSessionEnd`:

   ```java
   // Closes the media and/or the media completed and unloaded,  
   // and call trackSessionEnd().  
   public void onMainVideoUnload(Observable observable, Object data) {  
       _heartbeat.trackSessionEnd(); 
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` marca o fim de uma sessão de rastreamento de mídia. Se a sessão tiver sido assistida até o final, onde o usuário assistiu ao conteúdo até o fim, verifique se `trackComplete` () é chamado antes de `trackSessionEnd`. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new media tracking session.

1. **Rastrear todos os cenários de pausa possíveis**

   Identify the event from the media player for media pause and call `trackPause`:

   ```java
   public void onVideoPause(Observable observable, Object data) {  
       _heartbeat.trackPause(); 
   }
   ```

   **Pausar cenários**

   Identify any scenario in which the Video Player will pause and make sure that `trackPause` is properly called. Os seguintes cenários exigem que o aplicativo chame `trackPause()`:

   * O usuário clica explicitamente em Pausar no aplicativo.
   * O reprodutor se coloca no estado Pausado.
   * (*Aplicativos móveis*) - O usuário coloca o aplicativo em segundo plano, mas você deseja que o aplicativo mantenha a sessão aberta.
   * (*Aplicativos móveis*) - Qualquer tipo de interrupção de sistema que ocorra e faça com que um aplicativo seja colocado em segundo plano. Por exemplo, o usuário recebe uma chamada ou um pop-up de outro aplicativo é exibido, mas você deseja que o aplicativo mantenha a sessão ativa para que o usuário possa retomar a mídia do ponto em que foi interrompida.

1. Identifique o evento do reprodutor para reprodução e/ou retomada da pausa da mídia e chame `trackPlay`.

   ```java
   // trackPlay() 
   public void onVideoPlay(Observable observable, Object data) {  
       _heartbeat.trackPlay(); 
   }
   ```

   >[!TIP]
   >
   >Pode ser a mesma fonte de evento usada na Etapa 4. Ensure that each `trackPause()` API call is paired with a following `trackPlay()` API call when the media playback resumes.

Consulte as informações adicionais sobre o rastreamento da reprodução principal:

* Cenários de rastreamento: [Reprodução VOD sem anúncios](../../../sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Reprodutor de exemplo incluído com o SDK do Android para um exemplo completo de rastreamento.

