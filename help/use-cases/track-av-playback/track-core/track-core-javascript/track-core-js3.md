---
title: Saiba como rastrear a reprodução principal usando o JavaScript v3.x
description: Saiba como implementar o rastreamento principal usando o SDK de mídia em um navegador que utiliza aplicativos JavaScript 3.x.
exl-id: f3145450-82ba-4790-91a4-9d2cc97bbaa5
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/bIOfr94Q7wJLH9LfRg9VLIEJuS6JPvcgSWS62YCVguc
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 759
ht-degree: 85%

---

# Rastrear a reprodução principal usando o JavaScript 3.x{#track-core-playback-on-javascript}

Esta documentação abrange o rastreamento na versão 3.x do SDK.

>[!IMPORTANT]
>
>Se estiver implementando uma versão anterior do SDK, você pode baixar os Guias dos desenvolvedores Anterior aqui: [Baixar SDKs](/help/getting-started/download-sdks.md)

1. **Configuração de rastreamento inicial**

   Identifique quando o usuário aciona a intenção de reproduzir (o usuário clica em Reproduzir e/ou a reprodução automática está ativada) e crie uma instância `MediaObject`.

   [API createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | Nome da variável | Tipo | Descrição |
   | --- | --- | --- |
   | `name` | string | String não vazia que indica o nome da mídia. |
   | `id` | string | String não vazia que indica um identificador de mídia exclusivo. |
   | `length` | number | Número positivo que indica a duração da mídia em segundos. Use 0 se o comprimento for desconhecido. |
   | `streamType` | string |   |
   | `mediaType` | | Tipo de mídia (áudio ou vídeo). |

   **`StreamType`Constantes:**

   | Nome da constante | Descrição   |
   |---|---|
   | `VOD` | Tipo de fluxo para vídeo sob demanda. |
   | `AOD` | Tipo de fluxo para áudio sob demanda. |

   **`MediaType`Constantes:**

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

   Opcionalmente, anexe metadados padrão e/ou personalizados à sessão de rastreamento por meio de variáveis de dados de contexto.

   * **Metadados padrão**

     >[!NOTE]
     >
     >Anexar os metadados padrão é opcional.

      * Referência da API de chaves de metadados de mídia - [Chaves de metadados padrão - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

   * **Metadados personalizados**

     Crie um objeto variável para as variáveis personalizadas e preencha com os dados desta mídia. Por exemplo:

     ```js
     /* Set context data */
      var contextData = {};
     
      //Standard metadata
      contextData[ADB.Media.VideoMetadataKeys] = "Sample Episode";
      contextData[ADB.Media.VideoMetadataKeys] = "Sample Show";
     
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
   contextData[ADB.Media.VideoMetadataKeys] = "Sample Episode";
   contextData[ADB.Media.VideoMetadataKeys] = "Sample Show";
   
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
   >Se não estiver usando contextData, basta enviar um objeto vazio para o argumento `data` em `trackSessionStart`.

1. **Rastrear o início real da reprodução**

   Identifique o evento no reprodutor de mídia para o início da reprodução, em que o primeiro quadro da mídia é renderizado na tela, e chame `trackPlay`:

   ```js
   tracker.trackPlay();
   ```

1. **Atualizar valor do indicador de reprodução**

   Quando o indicador de reprodução de mídia for alterado, notifique a SDK chamando a API `mediaUpdatePlayhead`. <br /> Para vídeos sob demanda (VOD), o valor é especificado em segundos a partir do início do item de mídia. <br /> Para transmissões ao vivo, se o player não fornecer informações sobre a duração do conteúdo, o valor pode ser especificado como o número de segundos desde a meia-noite UTC daquele dia.

   ```
   tracker.updatePlayhead(position)
   ```

   >[!NOTE]
   >
   >Considere o seguinte ao chamar a API `tracker.updatePlayhead`:
   >* Ao usar marcadores de progresso, a duração do conteúdo é necessária e o indicador de reprodução precisa ser atualizado para o número de segundos desde o início do item de mídia, começando com 0.
   >* Ao usar SDKs de mídia, você deve chamar a API `tracker.updatePlayhead` pelo menos uma vez por segundo.

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

* Cenários de rastreamento: [Reprodução de VOD sem anúncios](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* Exemplo de player incluído no SDK do JavaScript para obter um exemplo completo de rastreamento.
