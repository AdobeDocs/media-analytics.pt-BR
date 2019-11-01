---
title: Rastreamento da reprodução principal no JavaScript
description: Este tópico descreve como implementar o rastreamento principal usando o SDK de mídia em aplicativos de navegador (JS).
uuid: 3d6e0ab1-899a-43c3-b632-8276e84345ab
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Rastreamento da reprodução principal no JavaScript{#track-core-playback-on-javascript}

>[!IMPORTANT]
>Esta documentação cobre o rastreamento na versão 2.x do SDK. Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores 1.x aqui: [Baixar SDKs](/help/sdk-implement/download-sdks.md).

1. **Configuração de rastreamento inicial**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   [API de createMediaObject API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | Nome da variável | Descrição | Obrigatório |
   | --- | --- | :---: |
   | `name` | Nome da mídia | Sim |
   | `mediaid` | Identificador exclusivo de mídia | Sim |
   | `length` | Comprimento da mídia | Sim |
   | `streamType` | Tipo de fluxo (consulte Constantes _de_ StreamType abaixo) | Sim |
   | `mediaType` | Tipo de mídia (consulte as constantes __ MediaType abaixo) | Sim |

   **`StreamType`constantes:**

   | Nome da constante | Descrição   |
   |---|---|
   | `VOD` | Tipo de fluxo para vídeo sob demanda. |
   | `LIVE` | Tipo de fluxo para conteúdo LIVE. |
   | `LINEAR` | Tipo de fluxo para conteúdos lineares. |
   | `AOD` | Tipo de fluxo para Áudio sob demanda. |
   | `AUDIOBOOK` | Tipo de fluxo para audiobook. |
   | `PODCAST` | Tipo de fluxo para podcast. |

   **`MediaType`constantes:**

   | Nome da constante | Descrição |
   |---|---|
   | `Audio` | Tipo de mídia para fluxos de áudio. |
   | `Video` | Tipo de mídia para fluxos de vídeo. |

   ```
   var mediaObject =  
     MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                     <MEDIA_ID,  
                                     <MEDIA_LENGTH>, 
                                     MediaHeartbeat.StreamType.VOD,
                                     <MEDIA_TYPE>);
   ```

1. **Anexar metadados**

   Como opção, anexe objetos de metadados padrão e/ou personalizados à sessão de rastreamento por meio de variáveis de dados de contexto.

   * **Metadados padrão**

      [Implementar metadados padrão no JavaScript](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-js.md)

      >[!NOTE]
      >
      >Anexar o objeto de metadados padrão ao objeto de mídia é opcional.

      * Referência da API de chaves de metadados de mídia - [Chaves de metadados padrão - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

         See the comprehensive set of available metadata here: [Audio and video parameters](/help/metrics-and-metadata/audio-video-parameters.md)
   * **Metadados personalizados**

      Crie um objeto variável para as variáveis personalizadas e preencha com os dados para essa mídia. Por exemplo:

      ```js
      /* Set custom context data */ 
      var customVideoMetadata = { 
          isUserLoggedIn: "false", 
          tvStation: "Sample TV station", 
          programmer: "Sample programmer" 
      };
      ```


1. **Rastrear a intenção de iniciar a reprodução**

   Para começar a rastrear uma sessão de mídia, chame `trackSessionStart` a instância Media Heartbeat:

   ```js
   mediaHeartbeat.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!TIP]
   >
   >O segundo valor é o nome do objeto de metadados de mídia personalizado que você criou na etapa 2.

   >[!IMPORTANT]
   >
   >`trackSessionStart` rastreia a intenção de reproduzir do usuário e não o início da reprodução. Essa API é utilizada para carregar os dados/metadados e estimar a métrica de tempo do início de QoS (duração entre `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >
   >If you are not using custom metadata, simply send an empty object for the `data` argument in `trackSessionStart`, as shown in the commented out line in the iOS example above.

1. **Rastrear o início real da reprodução**

   Identify the event from the media player for the beginning of the playback, where the first frame of the media is rendered on the screen, and call `trackPlay`:

   ```js
   mediaHeartbeat.trackPlay();
   ```

1. **Acompanhar a conclusão da reprodução**

   Identify the event from the media player for the completion of the playback, where the user has watched the content until the end, and call `trackComplete`:

   ```js
   mediaHeartbeat.trackComplete();
   ```

1. **Acompanhar o final da sessão**

   Identify the event from the media player for the unloading/closing of the playback, where the user closes the media and/or the media is completed and has been unloaded, and call `trackSessionEnd`:

   ```js
   mediaHeartbeat.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` marca o fim de uma sessão de rastreamento. Se a sessão tiver sido assistida até o final, onde o usuário assistiu ao conteúdo até o fim, verifique se `trackComplete` () é chamado antes de `trackSessionEnd`. Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new tracking session.

1. **Rastrear todos os cenários de pausa possíveis**

   Identifique o evento do player de mídia para pausa e chame `trackPause`:

   ```js
   mediaHeartbeat.trackPause();
   ```

   **Pausar cenários**

   Identify any scenario in which the media player will pause and make sure that `trackPause` is properly called. Os seguintes cenários exigem que o aplicativo chame `trackPause()`:

   * O usuário clica explicitamente em Pausar no aplicativo.
   * O reprodutor se coloca no estado Pausado.
   * (*Aplicativos móveis*) - O usuário coloca o aplicativo em segundo plano, mas você deseja que o aplicativo mantenha a sessão aberta.
   * (*Aplicativos móveis*) - Qualquer tipo de interrupção de sistema que ocorra e faça com que um aplicativo seja colocado em segundo plano. Por exemplo, o usuário recebe uma chamada ou um pop-up de outro aplicativo é exibido, mas você deseja que o aplicativo mantenha a sessão ativa para que o usuário possa retomar a mídia do ponto em que foi interrompida.

1. Identifique o evento do reprodutor para reprodução e/ou retomada da pausa e chame `trackPlay`:

   ```js
   mediaHeartbeat.trackPlay();
   ```

   >[!TIP]
   >
   >Essa pode ser a mesma fonte de evento usada na Etapa 4. Ensure that each `trackPause()` API call is paired with a following `trackPlay()` API call when the playback resumes.

* Cenários de rastreamento: [Reprodução VOD sem anúncios](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Reprodutor de exemplo incluído com o SDK do JavaScript para um exemplo completo de rastreamento.

