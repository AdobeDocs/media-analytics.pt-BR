---
title: Saiba como rastrear a reprodução principal no iOS
description: Saiba como implementar o rastreamento principal usando o SDK de mídia no iOS.
uuid: bdc0e05c-4fe5-430e-aee2-f331bc59ac6b
exl-id: 5c6b36b3-a421-45a4-a65e-4eb57513ca4a
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 90%

---

# Rastreamento da reprodução principal no iOS{#track-core-playback-on-ios}

Esta documentação abrange o rastreamento na versão 2.x do SDK.

>[!IMPORTANT]
>
>Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores 1.x aqui: [Baixar SDKs](/help/getting-started/download-sdks.md).

1. **Configuração de rastreamento inicial**

   Identifique quando o usuário aciona a intenção de reproduzir (o usuário clica em Reproduzir e/ou a reprodução automática está ativada) e crie uma instância `MediaObject`.

   API de [createMediaObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)

   | Nome da variável | Descrição | Obrigatório |
   |---|---|---|
   | `name` | Nome do vídeo | Sim |
   | `mediaid` | Identificador exclusivo do vídeo | Sim |
   | `length` | Duração do vídeo | Sim |
   | `streamType` | Tipo de fluxo (consulte _Constantes de StreamType_ abaixo) | Sim |
   | `mediaType` | Tipo de mídia (consulte _Constantes de MediaType_ abaixo) | Sim |

   **`StreamType`Constantes:**

   | Nome da constante | Descrição |
   |---|---|
   | `ADBMediaHeartbeatStreamTypeVOD` | Tipo de fluxo para vídeo sob demanda |
   | `ADBMediaHeartbeatStreamTypeLIVE` | Tipo de fluxo para conteúdo LIVE |
   | `ADBMediaHeartbeatStreamTypeLINEAR` | Tipo de fluxo para conteúdos lineares |
   | `ADBMediaHeartbeatStreamTypeAOD` | Tipo de fluxo para áudio sob demanda |
   | `ADBMediaHeartbeatStreamTypeAUDIOBOOK` | Tipo de fluxo para audiobook |
   | `ADBMediaHeartbeatStreamTypePODCAST` | Tipo de fluxo para podcast |

   **`MediaType`Constantes:**

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

   Opcionalmente, anexe objetos de metadados de vídeo padrão e/ou personalizados à sessão de rastreamento de vídeo por meio de variáveis de dados de contexto.

   * **Metadados de vídeo padrão**

      * [Implementar metadados padrão no iOS](/help/use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
      * **Chaves de metadados de vídeo**
        [Chaves de metadados de iOS](/help/use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

      * Consulte a lista completa de metadados de vídeo aqui: [Parâmetros de áudio e vídeo](/help/implementation/variables/audio-video-parameters.md)

     >[!NOTE]
     >
     >Anexar o objeto de metadados de vídeo padrão ao objeto de mídia é opcional.

   * **Metadados personalizados**

     Crie um objeto variável para as variáveis personalizadas e preencha com os dados deste vídeo. Por exemplo:

     ```
     NSMutableDictionary *videoMetadata = [[NSMutableDictionary alloc] init];
     [videoMetadata setObject:@"false" forKey:@"isUserLoggedIn"];
     [videoMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
     ```

1. **Rastrear a intenção de iniciar a reprodução**

   Para começar a rastrear uma sessão de mídia, chame `trackSessionStart` na instância do Heartbeat de mídia.

   >[!TIP]
   >
   >O segundo valor é o nome de objeto dos metadados de vídeo personalizados, criado na etapa 2.

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
   >Se não estiver utilizando metadados de vídeo personalizados, basta enviar um objeto vazio para o argumento `data` em `trackSessionStart`, como mostrado na linha comentada do exemplo de iOS acima.

1. **Rastrear o início real da reprodução**

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
   >`trackSessionEnd` marca o fim de uma sessão de rastreamento de vídeo. Se a sessão tiver sido assistida até o final, onde o usuário assistiu ao conteúdo até o fim, verifique se `trackComplete` () é chamado antes de `trackSessionEnd`. Qualquer outra chamada de API de `track*` é ignorada depois de `trackSessionEnd`, exceto por `trackSessionStart` para uma nova sessão de rastreamento de vídeo.

1. **Rastrear todos os cenários de pausa possíveis**

   Identifique o evento no reprodutor de vídeo para vídeos pausados e chame `trackPause`:

   ```
   - (void)onVideoPause:(NSNotification *)notification {
       [_mediaHeartbeat trackPause];
   }
   ```

   **Pausar cenários**

   Identifique qualquer cenário no qual o reprodutor de vídeo será pausado e verifique se `trackPause` foi chamado corretamente. Os seguintes cenários exigem que o aplicativo chame `trackPause()`:

   * O usuário faz uma pausa explicitamente no aplicativo.
   * O player se coloca no estado Pausa.
   * (*Aplicativos móveis*) - O usuário coloca o aplicativo em segundo plano, mas você deseja que ele mantenha a sessão aberta.
   * (*Aplicativos móveis*) - Qualquer tipo de interrupção de sistema que ocorra e faça com que um aplicativo seja colocado em segundo plano. Por exemplo, o usuário recebe uma chamada ou uma pop-up de outro aplicativo ocorre, mas você deseja que o aplicativo mantenha a sessão ativa para dar ao usuário a oportunidade de retomar o vídeo a partir do ponto de interrupção.

1. Identifique o evento do reprodutor para reprodução e/ou continuação do vídeo a partir da pausa e chame `trackPlay`:

   ```
   - (void)onVideoPlay:(NSNotification *)notification {
       [_mediaHeartbeat trackPlay];
   }
   ```

   >[!TIP]
   >
   >Esta pode ser a mesma fonte de evento utilizada na Etapa 4. Verifique se cada chamada `trackPause()` da API está emparelhada a uma chamada `trackPlay()` da API quando a reprodução continuar.

Consulte o seguinte para obter informações adicionais sobre o rastreamento da reprodução principal:

* Cenários de rastreamento: [Reprodução de VOD sem anúncios](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* Exemplo de reprodutor incluído no SDK do iOS para obter um exemplo completo de rastreamento.
