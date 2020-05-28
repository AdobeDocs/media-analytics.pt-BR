---
title: Rastrear a reprodução principal usando o JavaScript v3.x
description: Este tópico descreve como implementar o rastreamento principal usando o SDK de mídia em um navegador usando aplicativos JavaScript 3.x.
translation-type: tm+mt
source-git-commit: 6c672bdf71a817f18cc2ca7ac76a17f8c4c93d4b
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 79%

---


# Rastrear a reprodução principal usando o JavaScript 3.x{#track-core-playback-on-javascript}

>[!IMPORTANT]
>Esta documentação abrange o rastreamento na versão 3.x do SDK. If you are implementing any previous versions of the SDK, you can download the Developers Guides here: [Download SDKs](/help/sdk-implement/download-sdks.md)

1. **Configuração de rastreamento inicial**

   Identifique quando o usuário aciona a intenção de reproduzir (o usuário clica em Reproduzir e/ou a reprodução automática está ativada) e crie uma instância `MediaObject`.

   [API de createMediaObject API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | Nome da variável | Tipo | Descrição |
   | --- | --- | --- |
   | `name` | string | String não vazia que denota o nome da mídia. |
   | `id` | string | Sequência de caracteres não vazia que denota um identificador de mídia exclusivo. |
   | `length` | número | Número positivo que indica a duração da mídia em segundos. Use 0 se o comprimento for desconhecido. |
   | `streamType` | string | [Tipo]de fluxo (link para constantes streamType) ou cadeia de caracteres não vazia para indicar o tipo de fluxo de mídia. |
   | `mediaType` | [MediaType](link para constantes MediaType) | Tipo de mídia (áudio ou vídeo). |

   **`StreamType`Constantes de:**

   | Nome da constante | Descrição   |
   |---|---|
   | `VOD` | Tipo de fluxo para vídeo sob demanda. |
   | `LIVE` | Tipo de fluxo para conteúdo LIVE. |
   | `LINEAR` | Tipo de fluxo para conteúdos lineares. |
   | `AOD` | Tipo de fluxo para áudio sob demanda. |
   | `AUDIOBOOK` | Tipo de fluxo para audiobook. |
   | `PODCAST` | Tipo de fluxo para podcast. |

   **`MediaType`Constantes de:**

   | Nome da constante | Descrição |
   |---|---|
   | `Audio` | Tipo de mídia para fluxos de áudio. |
   | `Video` | Tipo de mídia para fluxos de vídeo. |

   ```
   var mediaObject = ADB.Media.createMediaObject(<MEDIA_NAME>,
                                     <MEDIA_ID,
                                     <MEDIA_LENGTH>,
                                     <STREAM_TYPE>,
                                     <MEDIA_TYPE>);
   ```

1. **Anexar metadados**

   Como opção, anexe metadados padrão e/ou personalizados à sessão de rastreamento por meio de variáveis de dados de contexto.

   * **Metadados padrão**

      >[!NOTE]
      >
      >Anexar os metadados padrão é opcional.

      * Referência da API de chaves de metadados de mídia - [Chaves de metadados padrão - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

         Consulte o conjunto completo de metadados aqui: [Parâmetros de áudio e vídeo](/help/metrics-and-metadata/audio-video-parameters.md)
   * **Metadados personalizados**

      Crie um objeto variável para as variáveis personalizadas e preencha com os dados desta mídia. Por exemplo:

      ```js
      /* Set context data */
       var contextData = {};
      
       //Standard metadata
       contextData[ADB.Media.VideoMetadataKeys.EPISODE] = "Sample Episode";
       contextData[ADB.Media.VideoMetadataKeys.SHOW] = "Sample Show";
      
       //Custom metadata
       contextData["isUserLoggedIn"] = "false";
       contextData["tvStation"] = "Sample TV Station";
      ```


1. **Rastrear a intenção de iniciar a reprodução**

   Para começar a rastrear uma sessão de mídia, chame `trackSessionStart` na instância do Media Heartbeat:

   ```js
   var mediaObject = ADB.Media.createMediaObject("video-name",
                                                 "video-id",
                                                 60.0,
                                                 ADB.Media.StreamType.VOD,
                                                 ADB.Media.MediaType.Video);
   
   var contextData = {};
   
   //Standard metadata
   contextData[ADB.Media.VideoMetadataKeys.EPISODE] = "Sample Episode";
   contextData[ADB.Media.VideoMetadataKeys.SHOW] = "Sample Show";
   
   //Custom metadata
   contextData["isUserLoggedIn"] = "false";
   contextData["tvStation"] = "Sample TV Station";
   
   tracker.trackSessionStart(mediaObject, contextData);
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` rastreia a intenção de reproduzir do usuário e não o início da reprodução. Essa API é utilizada para carregar os dados/metadados e estimar a métrica de tempo do início de QoS (duração entre `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >
   >If you are not using contextData, simply send an empty object for the `data` argument in `trackSessionStart`.

1. **Rastrear o início real da reprodução**

   Identifique o evento no reprodutor de mídia para o início da reprodução, em que o primeiro quadro da mídia é renderizado na tela, e chame `trackPlay`:

   ```js
   tracker.trackPlay();
   ```

1. **Rastrear a conclusão da reprodução**

   Identifique o evento no reprodutor de mídia para a conclusão da reprodução, em que o usuário assistiu ao conteúdo até o fim, e chame `trackComplete`:

   ```js
   tracker.trackComplete();
   ```

1. **Rastrear o final da sessão**

   Identifique o evento no reprodutor de mídia para o descarregamento/encerramento da reprodução, em que o usuário fecha a mídia, e/ou a mídia é concluída e descarregada, e chame `trackSessionEnd`:

   ```js
   tracker.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` marca o fim de uma sessão de rastreamento. Se a sessão tiver sido assistida até o final, onde o usuário assistiu ao conteúdo até o fim, verifique se `trackComplete` () é chamado antes de `trackSessionEnd`. Qualquer outra chamada de API de `track*` é ignorada depois de `trackSessionEnd`, exceto por `trackSessionStart` para uma nova sessão de rastreamento.

1. **Rastrear todos os cenários de pausa possíveis**

   Identifique o evento do reprodutor de mídia para pausa e chame `trackPause`:

   ```js
   tracker.trackPause();
   ```

   **Pausar cenários**

   Identifique qualquer cenário no qual o reprodutor de mídia será pausado e verifique se `trackPause` foi chamado corretamente. Os seguintes cenários exigem que o aplicativo chame `trackPause()`:

   * O usuário faz uma pausa explicitamente no aplicativo.
   * O player se coloca no estado Pausa.
   * (*Aplicativos móveis*) - O usuário coloca o aplicativo em segundo plano, mas você deseja que ele mantenha a sessão aberta.
   * (*Aplicativos móveis*) - Qualquer tipo de interrupção de sistema que ocorra e faça com que um aplicativo seja colocado em segundo plano. Por exemplo, o usuário recebe uma chamada ou uma pop-up de outro aplicativo ocorre, mas você deseja que o aplicativo mantenha a sessão ativa para dar ao usuário a oportunidade de retomar a mídia a partir do ponto de interrupção.

1. Identifique o evento do reprodutor para reprodução e/ou retomada da pausa e chame `trackPlay`:

   ```js
   tracker.trackPlay();
   ```

   >[!TIP]
   >
   >Esta pode ser a mesma fonte de evento utilizada na Etapa 4. Verifique se cada chamada da API `trackPause()` está emparelhada a uma chamada da API `trackPlay()` quando a reprodução for retomada.

* Cenários de rastreamento: [Reprodução de VOD sem anúncios](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Exemplo de player incluído no SDK do JavaScript para obter um exemplo completo de rastreamento.
