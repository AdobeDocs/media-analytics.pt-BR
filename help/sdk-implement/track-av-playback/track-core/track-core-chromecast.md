---
title: Saiba como rastrear a reprodução principal no Chromecast
description: Saiba como implementar o rastreamento principal usando o SDK do Media no Chromecast.
uuid: a9fc59d8-a2f4-4889-bdec-55c42a835d06
exl-id: 9812d06d-9efd-460c-a626-6a15f61a4c35
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 165c7f01a2d2c32df518c89a5c49637107d41086
workflow-type: tm+mt
source-wordcount: '750'
ht-degree: 85%

---

# Rastreamento da reprodução principal no Chromecast{#track-core-playback-on-chromecast}

Esta documentação abrange o rastreamento na versão 2.x do SDK.

>[!IMPORTANT]
>
>Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores 1.x aqui: [Baixar SDKs](/help/sdk-implement/download-sdks.md).

1. **Configuração de rastreamento inicial**

   Identifique quando o usuário aciona a intenção de reproduzir (o usuário clica em Reproduzir e/ou a reprodução automática está ativada) e crie uma instância `MediaObject`.

   **`MediaObject`Referência da API:**

   [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

   ```
   mediaObject = ADBMobile.media.createMediaObject(<name>, <id>, <duration>, <streamType>, <mediaType>);
   ```

   **`StreamType`Constantes de:**

   [ADBMobile Media](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.StreamType)

   **`MediaType`Constantes de:**

   [ADBMobile Media](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.MediaType)

1. **Anexar metadados de vídeo**

   Opcionalmente, anexe objetos de metadados de vídeo padrão e/ou personalizados à sessão de rastreamento de vídeo por meio de variáveis de dados de contexto.

   * **Metadados de vídeo padrão**

      [Implementar metadados padrão no Chromecast](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)

      >[!NOTE]
      >
      >Anexar o objeto de metadados de vídeo padrão ao objeto de mídia é opcional.

   * **Metadados personalizados**

      Crie um objeto variável para as variáveis personalizadas e preencha com os dados deste vídeo. Por exemplo:

      ```js
      /* Set custom context data */
      var customVideoMetadata = {
          isUserLoggedIn: "false",
          tvStation: "Sample TV station",
          programmer: "Sample programmer"
      };
      ```

1. **Rastrear a intenção de iniciar a reprodução**

   Para começar a rastrear uma sessão de mídia, chame [trackSessionStart](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionStart) no objeto `media`.

   ```
   ADBMobile.media.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` rastreia a intenção de reproduzir do usuário e não o início da reprodução. Essa API é utilizada para carregar os dados/metadados de vídeo e estimar a métrica de tempo do início de QoS (duração entre `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >
   >O segundo valor é o nome de objeto dos metadados de vídeo personalizados, criado na etapa 2. Se não estiver utilizando metadados de vídeo personalizados, basta enviar um objeto vazio para o argumento `data` em `trackSessionStart`, como mostrado na linha comentada do exemplo de iOS acima.

1. **Rastrear o início real da reprodução**

   Identifique o evento no reprodutor de vídeo a partir do início da reprodução, em que o primeiro quadro do vídeo é renderizado na tela, e chame [trackPlay:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPlay)

   ```
   ADBMobile.media.trackPlay();
   ```

1. **Atualizar valor do indicador de reprodução**

   Atualizar `mediaUpdatePlayhead`&quot; posiciona várias vezes quando o indicador de reprodução muda. <br /> Para vídeo sob demanda (VOD), o valor é especificado em segundos a partir do início do item de mídia. <br /> Para transmissão ao vivo, se o reprodutor não fornecer informações sobre a duração do conteúdo, o valor pode ser especificado como o número de segundos desde a meia-noite UTC desse dia. <br />  Observação: Ao usar marcadores de progresso, a duração do conteúdo é necessária e o indicador de reprodução precisa ser atualizado como o número de segundos a partir do início do item de mídia, começando com 0.

   ```
   ADBMobile().mediaUpdatePlayhead(position)
   ```

1. **Rastrear a conclusão da reprodução**

   Identifique o evento no reprodutor de vídeo para a conclusão da reprodução, onde o usuário assistiu ao conteúdo até o fim, e chame [trackComplete:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete)

   ```
   ADBMobile.media.trackComplete();
   ```

1. **Rastrear o final da sessão**

   Identifique o evento no reprodutor de vídeo para o descarregamento/encerramento da reprodução, onde o usuário fecha o vídeo, e/ou ele é concluído e descarregado, e chame [trackSessionEnd:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionEnd)

   ```
   ADBMobile.media.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` marca o fim de uma sessão de rastreamento de vídeo. Se a sessão tiver sido assistida até o final, onde o usuário assistiu ao conteúdo até o fim, verifique se `trackComplete` () é chamado antes de `trackSessionEnd`. Qualquer outra chamada de API de `track*` é ignorada depois de `trackSessionEnd`, exceto por `trackSessionStart` para uma nova sessão de rastreamento de vídeo.

1. **Rastrear todos os cenários de pausa possíveis**

   Identifique o evento no reprodutor de vídeo para vídeos pausados e chame [trackPause:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPause)

   ```
   ADBMobile.media.trackPause();
   ```

   **Pausar cenários**

   Identifique qualquer cenário no qual o reprodutor de vídeo será pausado e verifique se `trackPause` foi chamado corretamente. Os seguintes cenários exigem que o aplicativo chame `trackPause()`:

   * O usuário faz uma pausa explicitamente no aplicativo.
   * O player se coloca no estado Pausa.
   * (*Aplicativos móveis*) - O usuário coloca o aplicativo em segundo plano, mas você deseja que ele mantenha a sessão aberta.
   * (*Aplicativos móveis*) - Qualquer tipo de interrupção de sistema que ocorra e faça com que um aplicativo seja colocado em segundo plano. Por exemplo, o usuário recebe uma chamada ou um pop-up de outro aplicativo ocorre, mas você deseja que o aplicativo mantenha a sessão ativa para que o usuário possa retomar o vídeo do ponto em que foi interrompido.

1. Identifique o evento do reprodutor para reprodução e/ou continuação do vídeo a partir da pausa e chame [trackPlay:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete)

   ```
   ADBMobile.media.trackPlay();
   ```

   >[!TIP]
   >
   >Esta pode ser a mesma fonte de evento utilizada na Etapa 4. Verifique se cada chamada `trackPause()` da API está emparelhada a uma chamada `trackPlay()` da API quando a reprodução continuar.

* Cenários de rastreamento: [Reprodução de VOD sem anúncios](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Reprodutor de exemplo incluído com o SDK do Chromecast para um exemplo completo de rastreamento.
