---
title: Explicação sobre o rastreamento da reprodução do conteúdo
description: “Saiba mais sobre o rastreamento da reprodução principal, incluindo o rastreamento da carga de mídia, início de mídia, pausa de mídia e conclusão de mídia. ”
uuid: 7b8e2f76-bc4e-4721-8933-3e4453b01788
exl-id: 98ad2783-c9e3-48de-88df-8549f26114a0
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a26e4e283646e5ceb352f357789748f376f5c747
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 100%

---

# Visão geral do rastreamento{#tracking-overview}

Esta documentação abrange o rastreamento na versão 2.x do SDK.

>[!IMPORTANT]
>
>Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores 1.x aqui: [Baixar SDKs.](/help/getting-started/download-sdks.md)

## Eventos do player

O rastreamento da reprodução principal inclui rastreamento da carga de mídia, início da mídia, pausa da mídia e conclusão da mídia. Embora não seja obrigatório, o rastreamento de buffering e busca também são componentes principais usados para rastrear a reprodução do conteúdo. Na API do media player, identifique os eventos do player que correspondem às chamadas de rastreamento do SDK da mídia, codifique os manipuladores de eventos para APIs de rastreamento de chamadas e preencha as variáveis obrigatórias e opcionais.

### No carregamento da mídia

* Criar o objeto de mídia
* Preencha os metadados
* Chame `trackSessionStart`; Por exemplo: `trackSessionStart(mediaObject, contextData)`

### No início da mídia

* Chame `trackPlay`

### Em pausar/retomar

* Chame `trackPause`
* Chame `trackPlay`   _quando a reprodução for retomada_

### Na conclusão da mídia

* Chame `trackComplete`

### Na interrupção da mídia

* Chame `trackSessionEnd`

### Quando a depuração é iniciada

* Chame `trackEvent(SeekStart)`

### Quando a depuração termina

* Chame `trackEvent(SeekComplete)`
Cancelar alterações

### Quando o buffering é iniciado

* Chame `trackEvent(BufferStart);`

### Quando o buffering termina

* Chame `trackEvent(BufferComplete);`

>[!TIP]
>
>A posição do indicador de reprodução é definida como parte do código de instalação e configuração. Para obter mais informações sobre `getCurrentPlayheadTime`, consulte [Visão geral: Diretrizes gerais de implementação.](/help/implementation/media-sdk-overview.md)


## Implementar {#implement}

1. **Configuração do rastreamento inicial -** Identifique quando o usuário aciona a intenção de reproduzir (o usuário clica em Reproduzir e/ou a reprodução automática está ativada) e crie uma instância `MediaObject` com as informações da mídia para nome do conteúdo, ID do conteúdo, duração do conteúdo e tipo de fluxo.

   **`MediaObject`referência:**

   | Nome da variável | Descrição | Obrigatório |
   |---|---|---|
   | `name` | Nome do conteúdo | Sim |
   | `mediaid` | Identificador exclusivo do conteúdo | Sim |
   | `length` | Extensão do conteúdo | Sim |
   | `streamType` | Tipo de transmissão | Sim |
   | `mediaType` | Tipo de mídia (conteúdo de áudio ou vídeo) | Sim |

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

   O formato geral para criar o `MediaObject` é `MediaHeartbeat.createMediaObject(<MEDIA_NAME>, <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);`

1. **Anexar metadados -** Opcionalmente, anexe objetos de metadados padrão e/ou personalizados à sessão de rastreamento por meio de variáveis de dados de contexto.

   * **Metadados padrão -**

     >[!NOTE]
     >
     >Anexar o objeto de metadados padrão ao objeto de mídia é opcional.

     Exemplifique um objeto de metadados padrão, preencha as variáveis desejadas e defina o objeto de metadados no objeto de Heartbeat de mídia.

     Consulte a lista completa de metadados aqui: [Parâmetros de áudio e vídeo.](../../implementation/variables/audio-video-parameters.md)

   * **Metadados personalizados -** Crie um objeto variável para as variáveis personalizadas e preencha com os dados deste conteúdo.

1. **Rastrear a intenção de iniciar a reprodução -** Para iniciar o rastreamento da sessão, chame `trackSessionStart` na instância do Heartbeat de mídia.

   >[!IMPORTANT]
   >
   >`trackSessionStart` rastreia a intenção de reproduzir do usuário e não o início da reprodução. Essa API é utilizada para carregar os dados/metadados e estimar a métrica de tempo do início de QoS (duração entre `trackSessionStart` e `trackPlay`).

   >[!NOTE]
   >
   >Se não estiver utilizando metadados personalizados, basta enviar um objeto vazio para o argumento `data` em `trackSessionStart`.

1. **Rastrear o início real da reprodução -** Identifique o evento do reprodutor de mídia a partir do início da reprodução, onde o primeiro quadro do conteúdo é renderizado na tela, e chame `trackPlay`.

1. **Rastrear a conclusão da reprodução -** Identifique o evento no reprodutor de mídia para a conclusão da reprodução, onde o usuário assistiu ao conteúdo até o fim, e faça a chamada `trackComplete`.

1. **Rastrear o final da sessão -** Identifique o evento no reprodutor de mídia para o descarregamento/fechamento da reprodução, onde o usuário fecha o conteúdo e/ou ele é concluído e descarregado, e faça a chamada `trackSessionEnd`:

   >[!IMPORTANT]
   >
   >`trackSessionEnd` marca o fim de uma sessão de rastreamento. Se a sessão tiver sido assistida até o final, onde o usuário assistiu ao conteúdo até o fim, verifique se `trackComplete` () é chamado antes de `trackSessionEnd`. Qualquer outra chamada de API de `track*` é ignorada depois de `trackSessionEnd`, exceto por `trackSessionStart` para uma nova sessão de rastreamento.

1. **Rastrear todos os cenários de pausa possíveis -** Identifique o evento do reprodutor de mídia para pausar e chame `trackPause`.

   **Cenários de pausa -** Identifique qualquer cenário no qual o Reprodutor será pausado e verifique se `trackPause` foi chamado corretamente. Os seguintes cenários exigem que o aplicativo chame `trackPause()`:

   * O usuário faz uma pausa explicitamente no aplicativo.
   * O player se coloca no estado Pausa.
   * (*Aplicativos móveis*) - O usuário coloca o aplicativo em segundo plano, mas você deseja que ele mantenha a sessão aberta.
   * (*Aplicativos móveis*) - Qualquer tipo de interrupção de sistema que ocorra e faça com que um aplicativo seja colocado em segundo plano. Por exemplo, o usuário recebe uma chamada ou uma pop-up de outro aplicativo ocorre, mas você deseja que o aplicativo mantenha a sessão ativa para dar ao usuário a oportunidade de retomar o conteúdo a partir do ponto de interrupção.

1. Identifique o evento do reprodutor para reprodução e/ou retomada da pausa e chame `trackPlay`.

   >[!TIP]
   >
   >Esta pode ser a mesma fonte de evento utilizada na Etapa 4. Verifique se cada chamada da API `trackPause()` está emparelhada a uma chamada da API `trackPlay()` quando a reprodução for retomada.

1. Analise os eventos de busca de reprodução no reprodutor de mídia. Na notificação de evento de início da busca, rastreie a busca com o evento `SeekStart`.
1. Na notificação de conclusão da busca do reprodutor de mídia, rastreie o término da busca com o evento `SeekComplete`.
1. Analise os eventos de buffering de reprodução no reprodutor de mídia e, na notificação do evento de início de buffering, rastreie o buffering usando o evento `BufferStart`.
1. Na notificação de conclusão de buffer do reprodutor de mídia, rastreie o término do buffer com o evento`BufferComplete`:

Veja exemplos de cada etapa nos seguintes tópicos específicos da plataforma e veja os exemplos de players incluídos em seus SDKs.

Para obter um exemplo simples de rastreamento de reprodução, consulte este uso do SDK do JavaScript 2.x em um player HTML5:

```js
/* Call on media start */
if (e.type == "play") {

    // Check for start of media
    if (!sessionStarted) {
        /* Set media info */     
        /* MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                            <MEDIA_ID>,  
                                            <MEDIA_LENGTH>,
                                            <MEDIA_STREAMTYPE>,
                                            <MEDIA_MEDIATYPE>);*/
        var mediaInfo = MediaHeartbeat.createMediaObject(
          document.getElementsByTagName('video')[0].getAttribute("name"),  
          document.getElementsByTagName('video')[0].getAttribute("id"),  
          video.duration,
          MediaHeartbeat.StreamType.VOD);

        /* Set custom context data */
        var customVideoMetadata = {
            isUserLoggedIn: "false",
            tvStation: "Sample TV station",
            programmer: "Sample programmer"
        };

        /* Set standard video metadata */     
        var standardVideoMetadata = {};
        standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.EPISODE] = "Sample Episode";
        standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.SHOW] = "Sample Show";
        mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata,  
                           standardVideoMetadata);     

        // Start Session
        this.mediaHeartbeat.trackSessionStart(mediaInfo, customVideoMetadata);    

        // Track play
        this.mediaHeartbeat.trackPlay();  
        sessionStarted = true;     

    } else {
        // Track play for resuming playack    
        this.mediaHeartbeat.trackPlay();  
    }
};

/* Call on video complete */
if (e.type == "ended") {
    console.log("video ended");
    this.mediaHeartbeat.trackComplete();
    this.mediaHeartbeat.trackSessionEnd();
    sessionStarted = false;     
};

/* Call on pause */
if (e.type == "pause") {
    this.mediaHeartbeat.trackPause();
};

/* Call on scrub start */
if (e.type == "seeking") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart);
};

/* Call on scrub stop */
if (e.type == "seeked") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete);
};

/* Call on buffer start */
if (e.type == "buffering") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart);
};

/* Call on buffer complete */
if (e.type == "buffered") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete);
};
```

## Validar {#validate}

Para obter informações sobre como validar sua implementação *herdada*, consulte [Validação herdada.](/help/legacy/validation/validation-overview.md)
