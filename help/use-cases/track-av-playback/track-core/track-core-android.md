---
title: Saiba como rastrear a reprodução principal no Android
description: Saiba como implementar o rastreamento principal usando o SDK de mídia no Android.
uuid: ab5fab95-76ed-4ae6-aedb-2e66eece7607
exl-id: d5f5a3f0-f1e0-4d68-af7f-88a30faed0db
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 93%

---

# Rastreamento da reprodução principal no Android{#track-core-playback-on-android}

Esta documentação abrange o rastreamento na versão 2.x do SDK.
>[!IMPORTANT]
>
>Se estiver implementando uma versão 1.x do SDK, você pode baixar o Guia dos desenvolvedores 1.x para Android aqui: [Baixar SDKs](/help/getting-started/download-sdks.md).

1. **Configuração de rastreamento inicial**

   Identifique quando o usuário aciona a intenção de reproduzir (o usuário clica em Reproduzir e/ou a reprodução automática está ativada) e crie uma instância `MediaObject`.

   [API de createMediaObject API](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)

   | Nome da variável | Descrição | Obrigatório |
   | --- | --- | :---: |
   | `name` | Nome da mídia | Sim |
   | `mediaId` | Identificador exclusivo de mídia | Sim |
   | `length` | Duração da mídia | Sim |
   | `streamType` | Tipo de fluxo (consulte _Constantes de StreamType_ abaixo) | Sim |
   | `mediaType` | Tipo de mídia (consulte _Constantes de MediaType_ abaixo) | Sim |

   **`StreamType`Constantes:**

   | Nome da constante | Descrição |
   |---|---|
   | `VOD` | Tipo de fluxo para vídeo sob demanda. |
   | `LIVE` | Tipo de fluxo para conteúdo LIVE. |
   | `LINEAR` | Tipo de fluxo para conteúdos lineares. |
   | `AOD` | Tipo de fluxo para áudio sob demanda |
   | `AUDIOBOOK` | Tipo de fluxo para audiobook |
   | `PODCAST` | Tipo de fluxo para podcast |

   **`MediaType`Constantes:**

   | Nome da constante | Descrição |
   |---|---|
   | `Audio` | Tipo de mídia para fluxos de áudio. |
   | `Video` | Tipo de mídia para fluxos de vídeo. |

   ```
   MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
     <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);
   ```

1. **Anexar metadados**

   Opcionalmente, anexe objetos de metadados padrão e/ou personalizados à sessão de rastreamento por meio de variáveis de dados de contexto.

   * **Metadados padrão**

     [Implementar metadados padrão no Android](/help/use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)

     >[!NOTE]
     >
     >Anexar o objeto de metadados padrão ao objeto de mídia é opcional.

      * Referência da API de chaves de metadados de mídia - [Chaves de metadados padrão - Android](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
      * Consulte o conjunto completo de metadados de vídeo aqui: [Parâmetros de áudio e vídeo](/help/implementation/variables/audio-video-parameters.md)

   * **Metadados personalizados**

     Crie um dicionário para as variáveis personalizadas e preencha com os dados desta mídia. Por exemplo:

     ```java
     HashMap<String, String> mediaMetadata =  
       new HashMap<String, String>();
     mediaMetadata.put("isUserLoggedIn", "false");
     mediaMetadata.put("tvStation", "Sample TV Station");
     mediaMetadata.put("programmer", "Sample programmer");
     ```

1. **Rastrear a intenção de iniciar a reprodução**

   Para começar a rastrear uma sessão de mídia, chame `trackSessionStart` na instância do Heartbeat de mídia. Por exemplo:

   ```java
   public void onVideoLoad(Observable observable, Object data) {  
       _heartbeat.trackSessionStart(mediaInfo, mediaMetadata);
   }
   ```

   >[!TIP]
   >
   >O segundo valor é o nome de objeto dos metadados de mídia personalizados, criado na etapa 2.

   >[!IMPORTANT]
   >
   >`trackSessionStart` rastreia a intenção de reproduzir do usuário e não o início da reprodução. Essa API é utilizada para carregar os dados/metadados de mídia e estimar a métrica de tempo do início de QoS (duração entre `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >
   >Se não estiver utilizando metadados de mídia personalizados, basta enviar um objeto vazio para o argumento em `trackSessionStart`.

1. **Rastrear o início real da reprodução**

   Identifique o evento do reprodutor de mídia para o início da reprodução, em que o primeiro quadro da mídia é renderizado na tela, e chame `trackPlay`:

   ```java
   // Video is rendered on the screen) and call trackPlay.  
   public void onVideoPlay(Observable observable, Object data) {
       _heartbeat.trackPlay();
   }
   ```

1. **Rastrear a conclusão da reprodução**

   Identifique o evento do reprodutor de mídia para a conclusão da reprodução, em que o usuário assistiu ao conteúdo até o fim, e chame `trackComplete`:

   ```java
   public void onVideoComplete(Observable observable, Object data) {
       _heartbeat.trackComplete();
   }
   ```

1. **Rastrear o final da sessão**

   Identifique o evento do reprodutor de mídia para o descarregamento/encerramento da reprodução, em que o usuário fecha a mídia, e/ou a mídia é concluída e descarregada, e chame `trackSessionEnd`:

   ```java
   // Closes the media and/or the media completed and unloaded,  
   // and call trackSessionEnd().  
   public void onMainVideoUnload(Observable observable, Object data) {  
       _heartbeat.trackSessionEnd();
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` marca o fim de uma sessão de rastreamento de mídia. Se a sessão tiver sido assistida até o final, onde o usuário assistiu ao conteúdo até o fim, verifique se `trackComplete` () é chamado antes de `trackSessionEnd`. Qualquer outra chamada de API de `track*` é ignorada depois de `trackSessionEnd`, exceto por `trackSessionStart` para uma nova sessão de rastreamento de mídia.

1. **Rastrear todos os cenários de pausa possíveis**

   Identifique o evento no reprodutor de mídia para pausa de mídia e chame `trackPause`:

   ```java
   public void onVideoPause(Observable observable, Object data) {  
       _heartbeat.trackPause();
   }
   ```

   **Pausar cenários**

   Identifique qualquer cenário no qual o reprodutor de vídeo será pausado e verifique se `trackPause` foi chamado corretamente. Os seguintes cenários exigem que o aplicativo chame `trackPause()`:

   * O usuário faz uma pausa explicitamente no aplicativo.
   * O player se coloca no estado Pausa.
   * (*Aplicativos móveis*) - O usuário coloca o aplicativo em segundo plano, mas você deseja que ele mantenha a sessão aberta.
   * (*Aplicativos móveis*) - Qualquer tipo de interrupção de sistema que ocorra e faça com que um aplicativo seja colocado em segundo plano. Por exemplo, o usuário recebe uma chamada ou uma pop-up de outro aplicativo ocorre, mas você deseja que o aplicativo mantenha a sessão ativa para dar ao usuário a oportunidade de retomar a mídia a partir do ponto de interrupção.

1. Identifique o evento do reprodutor para reprodução e/ou retomada da pausa da mídia e chame `trackPlay`.

   ```java
   // trackPlay()
   public void onVideoPlay(Observable observable, Object data) {  
       _heartbeat.trackPlay();
   }
   ```

   >[!TIP]
   >
   >Esta pode ser a mesma fonte de evento utilizada na Etapa 4. Verifique se cada chamada da API de `trackPause()` está emparelhada a uma chamada da API de `trackPlay()` quando a reprodução de mídia for retomada.

Consulte o seguinte para obter informações adicionais sobre o rastreamento da reprodução principal:

* Cenários de rastreamento: [Reprodução de VOD sem anúncios](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* Exemplo de reprodutor incluído no SDK do Android para obter um exemplo completo de rastreamento.
