---
seo-title: Rastreamento da reprodução principal no Chromecast
title: Rastreamento da reprodução principal no Chromecast
uuid: a 9 fc 59 d 8-a 2 f 4-4889-bdec -55 c 42 a 835 d 06
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Rastreamento da reprodução principal no Chromecast{#track-core-playback-on-chromecast}

>[!IMPORTANT]
>
>Esta documentação aborda o rastreamento na versão 2. x do SDK. Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores 1.x aqui: [Baixar SDKs](/help/sdk-implement/download-sdks.md).

1. **Configuração de rastreamento inicial**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   **`MediaObject`Referência da API:**

   [Createmediaobject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

   ```
   mediaObject = ADBMobile.media.createMediaObject(<name>, <id>, <duration>, <streamType>, <mediaType>); 
   ```

   **`StreamType`constantes:**

   [Adbmobile Media](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.StreamType)

   **`MediaType`constantes:**

   [Adbmobile Media](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.MediaType)

1. **Anexar metadados de vídeo**

   Como opção, anexe objetos de metadados de vídeo padrão e/ou personalizados à sessão de monitoramento de vídeo por meio das variáveis de dados de contexto.

   * **Metadados de vídeo padrão**

      [Implementar metadados padrão no Chromecast](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)

      >[!NOTE]
      >
      >A anexação do objeto de metadados de vídeo padrão ao objeto de mídia é opcional.

   * **Metadados personalizados**

      Crie um objeto de variável para as variáveis personalizadas e preencha os dados desse vídeo. Por exemplo:

      ```js
      /* Set custom context data */ 
      var customVideoMetadata = { 
          isUserLoggedIn: "false", 
          tvStation: "Sample TV station", 
          programmer: "Sample programmer" 
      };
      ```

1. **Rastrear a intenção de iniciar a reprodução**

   To begin tracking a media session, call [trackSessionStart](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionStart) on the `media` object.

   ```
   ADBMobile.media.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` rastreia a intenção de reproduzir do usuário e não o início da reprodução. Essa API é utilizada para carregar os dados/metadados de vídeo e estimar a métrica de tempo do início de QoS (duração entre `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >
   >O segundo valor é o nome de objeto de metadados de vídeo personalizado que você criou na etapa 2. If you are not using custom video metadata, simply send an empty object for the `data` argument in `trackSessionStart`, as shown in the commented out line in the iOS example above.

1. **Rastrear o início da reprodução atual**

   Identify the event from the video player for the beginning of the video playback, where the first frame of the video is rendered on the screen, and call [trackPlay:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPlay)

   ```
   ADBMobile.media.trackPlay();
   ```

1. **Rastrear a conclusão da reprodução**

   Identify the event from the video player for the completion of the video playback, where the user has watched the content until the end, and call [trackComplete:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete)

   ```
   ADBMobile.media.trackComplete();
   ```

1. **Rastrear o final da sessão**

   Identify the event from the video player for the unloading/closing of the video playback, where the user closes the video and/or the video is completed and has been unloaded, and call [trackSessionEnd:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionEnd)

   ```
   ADBMobile.media.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` marca o fim de uma sessão de monitoramento de vídeo. Se a sessão tiver sido assistida até o final, onde o usuário assistiu ao conteúdo até o fim, verifique se `trackComplete` () é chamado antes de `trackSessionEnd`. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new video tracking session.

1. **Rastrear todos os cenários de pausa possíveis**

   Identifique o evento no reprodutor de vídeo para vídeos pausados e chame [trackPause:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPause)

   ```
   ADBMobile.media.trackPause();
   ```

   **Pausar cenários**

   Identify any scenario in which the Video Player will pause and make sure that `trackPause` is properly called. Os seguintes cenários exigem que o aplicativo chame `trackPause()`:

   * O usuário clica explicitamente em Pausar no aplicativo.
   * O reprodutor se coloca no estado Pausado.
   * (*Aplicativos móveis*) - O usuário coloca o aplicativo em segundo plano, mas você deseja que o aplicativo mantenha a sessão aberta.
   * (*Aplicativos móveis*) - Qualquer tipo de interrupção de sistema que ocorra e faça com que um aplicativo seja colocado em segundo plano. Por exemplo, o usuário recebe uma chamada ou um pop-up de outro aplicativo ocorre, mas você deseja que o aplicativo mantenha a sessão ativa para que o usuário possa retomar o vídeo do ponto em que foi interrompido.

1. Identifique o evento do reprodutor para reprodução e/ou continuação do vídeo a partir da pausa e chame [trackPlay:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete)

   ```
   ADBMobile.media.trackPlay();
   ```

   >[!TIP]
   >
   >Pode ser a mesma fonte de evento usada na Etapa 4. Verifique se cada chamada `trackPause()` da API está emparelhada a uma chamada `trackPlay()` da API quando a reprodução continuar.

* Cenários de rastreamento: [Reprodução VOD sem anúncios](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Reprodutor de exemplo incluído com o SDK do Chromecast para um exemplo completo de rastreamento.

