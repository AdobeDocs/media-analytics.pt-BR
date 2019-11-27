---
title: Rastreamento da reprodução principal no Roku
description: Este tópico descreve como implementar o rastreamento principal usando o SDK do Media no Roku.
uuid: a8aa7b3c-2d39-44d7-8ebc-b101d130101f
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Rastreamento da reprodução principal no Roku {#track-core-playback-on-roku}

>[!IMPORTANT]
>Esta documentação abrange o rastreamento na versão 2.x do SDK. Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores 1.x aqui: [Baixar SDKs](/help/sdk-implement/download-sdks.md).

1. **Configuração de rastreamento inicial**

   Identifique quando o usuário aciona a intenção de reproduzir (o usuário clica em Reproduzir e/ou a reprodução automática está ativada) e crie uma instância `MediaObject`.

   **`MediaObject`referência:**

   | Nome da variável | Descrição | Obrigatório |
   | --- | --- | :---: |
   | `name` | Nome do vídeo | Sim |
   | `mediaid` | Identificador exclusivo do vídeo | Sim |
   | `length` | Duração do vídeo | Sim |
   | `streamType` | Tipo de fluxo (consulte _Constantes de StreamType_ abaixo) | Sim |
   | `mediaType` | Tipo de mídia (consulte _Constantes de MediaType_ abaixo) | Sim |

   Constantes de **`StreamType`:**

   | Nome da constante | Descrição   |
   |---|---|
   | `MEDIA_STREAM_TYPE_VOD` | Tipo de fluxo para vídeo sob demanda. |
   | `MEDIA_STREAM_TYPE_LIVE` | Tipo de fluxo para conteúdo LIVE. |
   | `MEDIA_STREAM_TYPE_LINEAR` | Tipo de fluxo para conteúdos lineares. |
   | `MEDIA_STREAM_TYPE_AOD` | Tipo de fluxo para áudio sob demanda |
   | `MEDIA_STREAM_TYPE_AUDIOBOOK` | Tipo de fluxo para audiobook |
   | `MEDIA_STREAM_TYPE_PODCAST` | Tipo de fluxo para podcast |

   Constantes de **`MediaType`:**

   | Nome da constante | Descrição |
   |---|---|
   | `MEDIA_STREAM_TYPE_AUDIO` | Tipo de mídia para fluxos de áudio. |
   | `MEDIA_STREAM_TYPE_VIDEO` | Tipo de mídia para fluxos de vídeo. |

   **Crie um objeto de informações de mídia para vídeo com conteúdo de VOD:**

   ```
    mediaInfo = adb_media_init_mediainfo(
     "<MEDIA_NAME>",
     "<MEDIA_ID>",
     600,
     ADBMobile().MEDIA_STREAM_TYPE_VOD,
     ADBMobile().MEDIA_TYPE_VIDEO
   )
   ```

   ou

   ```
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.name = "<MEDIA_NAME>"
   mediaInfo.id = "<MEDIA_ID>"
   mediaInfo.length = 600
   mediaInfo.streamType = ADBMobile().MEDIA_STREAM_TYPE_VOD
   mediaInfo.mediaType = ADBMobile().MEDIA_TYPE_VIDEO
   ```

   **Crie um objeto de informações de mídia para vídeo com conteúdo AOD:**

   ```
   mediaInfo = adb_media_init_mediainfo(
    "<MEDIA_NAME>", 
    "<MEDIA_ID>", 
    600, 
    ADBMobile().MEDIA_STREAM_TYPE_AOD, 
    ADBMobile().MEDIA_TYPE_AUDIO
   )
   ```

   ou

   ```
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.name = "<MEDIA_NAME>"
   mediaInfo.id = "<MEDIA_ID>"
   mediaInfo.length = 600
   mediaInfo.streamType = ADBMobile().MEDIA_STREAM_TYPE_AOD
   mediaInfo.mediaType = ADBMobile().MEDIA_TYPE_AUDIO
   ```

1. **Anexar metadados**

   Opcionalmente, anexe objetos de metadados padrão e/ou personalizados à sessão de rastreamento por meio de variáveis de dados de contexto.

   * **Metadados padrão**

      [Implementar metadados padrão no JavaScript](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-js.md)

      >[!NOTE]
      >
      >Anexar o objeto de metadados padrão ao objeto de mídia é opcional.

      * Referência da API de chaves de metadados de mídia - [Chaves de metadados padrão - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

         Consulte o conjunto completo de metadados aqui: [Parâmetros de áudio e vídeo](/help/metrics-and-metadata/audio-video-parameters.md)
   * **Metadados personalizados**

      Crie um objeto variável para as variáveis personalizadas e preencha com os dados desta mídia. Por exemplo:

      ```js
      /* Set custom context data */ 
      var customVideoMetadata = { 
          isUserLoggedIn: "false", 
          tvStation: "Sample TV station", 
          programmer: "Sample programmer" 
      };
      ```


1. **Rastrear a intenção de iniciar a reprodução**

   Para começar a rastrear uma sessão de mídia, chame `trackSessionStart` na instância do Media Heartbeat:

   ```js
   mediaHeartbeat.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!TIP]
   >
   >O segundo valor é o nome de objeto dos metadados de mídia personalizados, criado na etapa 2.

   >[!IMPORTANT]
   >
   >`trackSessionStart` rastreia a intenção de reproduzir do usuário e não o início da reprodução. Essa API é utilizada para carregar os dados/metadados e estimar a métrica de tempo do início de QoS (duração entre `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >
   >Se não estiver utilizando metadados personalizados, basta enviar um objeto vazio para o argumento `data` em `trackSessionStart`, como mostrado na linha comentada do exemplo de iOS acima.

1. **Rastrear o início real da reprodução**

   Identifique o evento no reprodutor de mídia para o início da reprodução, em que o primeiro quadro da mídia é renderizado na tela, e chame `trackPlay`:

   ```js
   mediaHeartbeat.trackPlay();
   ```

1. **Rastrear a conclusão da reprodução**

   Identifique o evento no reprodutor de mídia para a conclusão da reprodução, em que o usuário assistiu ao conteúdo até o fim, e chame `trackComplete`:

   ```js
   mediaHeartbeat.trackComplete();
   ```

1. **Rastrear o final da sessão**

   Identifique o evento no reprodutor de mídia para o descarregamento/encerramento da reprodução, em que o usuário fecha a mídia, e/ou a mídia é concluída e descarregada, e chame `trackSessionEnd`:

   ```js
   mediaHeartbeat.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >Um `trackSessionEnd` marca o fim de uma sessão de rastreamento. Se a sessão tiver sido assistida até o final, onde o usuário assistiu ao conteúdo até o fim, verifique se `trackComplete` () é chamado antes de `trackSessionEnd`. Qualquer outra chamada de API de `track*` é ignorada depois de `trackSessionEnd`, exceto por `trackSessionStart` para uma nova sessão de rastreamento.  Método de rastreamento da reprodução de mídia para rastrear o carregamento da mídia e definir a sessão atual como ativa:

   ```
   ‘ Create a media info object
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.id = <MEDIA_ID>
   mediaInfo.playhead = "0"
   mediaInfo.length = "600"
   ```

1. **Anexar metadados de vídeo**

   Opcionalmente, anexe objetos de metadados de vídeo padrão e/ou personalizados à sessão de rastreamento de vídeo por meio de variáveis de dados de contexto.

   * **Metadados de vídeo padrão**

      [Implementar metadados padrão no Roku](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)

      >[!NOTE]
      >Anexar o objeto de metadados de vídeo padrão ao objeto de mídia é opcional.

   * **Metadados personalizados**

      Crie um objeto variável para as variáveis personalizadas e preencha com os dados deste vídeo. Por exemplo:

      ```
      mediaContextData = {}
      mediaContextData["cmk1"] = "cmv1"
      mediaContextData["cmk2"] = "cmv2"
      ```

1. **Rastrear a intenção de iniciar a reprodução**

   Para começar a rastrear uma sessão de mídia, chame `trackSessionStart` na instância do Media Heartbeat:

   ```
   ADBMobile().mediaTrackSessionStart(mediaInfo,mediaContextData)
   ```

   >[!TIP]
   >O segundo valor é o nome de objeto dos metadados de vídeo personalizados, criado na etapa 2.

   >[!IMPORTANT]
   >`trackSessionStart` rastreia a intenção de reproduzir do usuário e não o início da reprodução. Essa API é utilizada para carregar os dados/metadados de vídeo e estimar a métrica de tempo do início de QoS (duração entre `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >Se não estiver utilizando metadados de vídeo personalizados, basta enviar um objeto vazio para o argumento `data` em `trackSessionStart`, como mostrado na linha comentada do exemplo de iOS acima.

1. **Rastrear o início real da reprodução**

   Identifique o evento no reprodutor de vídeo a partir do início da reprodução, onde o primeiro quadro do vídeo é renderizado na tela, e chame `trackPlay`.

   ```
   ADBMobile().mediaTrackPlay()
   ```

1. **Rastrear a conclusão da reprodução**

   Identifique o evento no reprodutor de vídeo para a conclusão da reprodução, onde o usuário assistiu ao conteúdo até o fim, e chame `trackComplete`.

   ```
   ADBMobile().mediaTrackComplete()
   ```

1. **Rastrear o final da sessão**

   Identifique o evento no reprodutor de vídeo para o descarregamento/encerramento da reprodução, onde o usuário fecha o vídeo, e/ou ele é concluído e descarregado, e chame `trackSessionEnd`.

   ```
   ADBMobile().mediaTrackSessionEnd()
   ```

   >[!IMPORTANT]
   >`trackSessionEnd` marca o fim de uma sessão de rastreamento de vídeo. Se a sessão tiver sido assistida até o final, onde o usuário assistiu ao conteúdo até o fim, verifique se `trackComplete` () é chamado antes de `trackSessionEnd`. Qualquer outra chamada de API de `track*` é ignorada depois de `trackSessionEnd`, exceto por `trackSessionStart` para uma nova sessão de rastreamento de vídeo.

1. **Rastrear todos os cenários de pausa possíveis**

   Identifique o evento no reprodutor de vídeo para vídeos pausados e chame `trackPause`:

   ```
   ADBMobile().mediaTrackPause()
   ```

   **Pausar cenários**

   Identifique qualquer cenário no qual o reprodutor de vídeo será pausado e verifique se `trackPause` foi chamado corretamente. Os seguintes cenários exigem que o aplicativo chame `trackPause()`:

   * O usuário clica explicitamente em Pausar no aplicativo.
   * O reprodutor se coloca no estado Pausado.
   * (*Aplicativos móveis*) - O usuário coloca o aplicativo em segundo plano, mas você deseja que o aplicativo mantenha a sessão aberta.
   * (*Aplicativos móveis*) - Qualquer tipo de interrupção de sistema que ocorra e faça com que um aplicativo seja colocado em segundo plano. Por exemplo, o usuário recebe uma chamada ou um pop-up de outro aplicativo ocorre, mas você deseja que o aplicativo mantenha a sessão ativa para que o usuário possa retomar o vídeo do ponto em que foi interrompido.

1. Identifique o evento do reprodutor para reprodução e/ou continuação do vídeo a partir da pausa e chame `trackPlay`:

   ```
   ADBMobile().mediaTrackPlay()
   ```

   >[!TIP]
   >Esta pode ser a mesma fonte de evento utilizada na Etapa 4. Verifique se cada chamada `trackPause()` da API está emparelhada a uma chamada `trackPlay()` da API quando a reprodução continuar.

* Cenários de rastreamento: [Reprodução de VOD sem anúncios](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Reprodutor de exemplo incluído com o SDK do Roku para um exemplo completo de rastreamento.

