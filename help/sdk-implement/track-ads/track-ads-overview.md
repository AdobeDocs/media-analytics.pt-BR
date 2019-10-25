---
seo-title: Visão geral
title: Visão geral
uuid: 1607798b-c6ef-4d60-8e40-e958c345b09c
translation-type: tm+mt
source-git-commit: 8938e324d570b7e3e2c3c3e971c00ade7e6be8b6

---


# Visão geral{#overview}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação usando os SDKs 2.x. Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores 1.x aqui: [Baixar SDKs.](/help/sdk-implement/download-sdks.md)

A reprodução do anúncio inclui o rastreamento de ad breaks, anúncios iniciados, anúncios concluídos e anúncios ignorados. Use a API do player de mídia para identificar eventos do player principal e preencher as variáveis de anúncio necessárias e opcionais. Consulte a lista abrangente de metadados aqui: Parâmetros de [anúncio.](/help/metrics-and-metadata/ad-parameters.md)

## Eventos do player {#player-events}


### Início de pausa de anúncio

>[!NOTE]
>Incluindo pre-roll

* Crie uma instância de objeto `adBreak` para o ad break. Por exemplo, `adBreakObject`.

* Call `trackEvent` for the ad break start with your `adBreakObject`.

### Em cada início de ativo de anúncio

* Crie a instância do objeto de anúncio para o ativo de anúncio. Por exemplo, `adObject`.
* Populate the ad metadata, `adCustomMetadata`.
* Chame `trackEvent` para iniciar o anúncio. 

### Em cada conclusão de anúncio

* Chame `trackEvent` para concluir o anúncio. 

### Ao ignorar o anúncio

* Chame `trackEvent` para o anúncio ignorado.

### Na conclusão do ad break

* Chame `trackEvent` para concluir o ad break.

## Implementação do rastreamento de anúncios {#implement-ad-tracking}

### Constantes de rastreamento do anúncio

| Nome da constante | Descrição  |
|---|---|
| `AdBreakStart` | Constante para rastrear o evento AdBreak Start |
| `AdBreakComplete` | Constante para rastrear o evento AdBreak Complete |
| `AdStart` | Constante para rastrear o evento Ad Start |
| `AdComplete` | Constante para rastrear o evento Ad Complete |
| `AdSkip` | Constante para rastrear o evento Ad Skip |

### Etapas de implementação

1. Identifique o início do limite do ad break, incluindo o anúncio precedente, e crie um `AdBreakObject` usando as informações do ad break.

   `AdBreakObject` referência:

   | Nome da variável | Descrição | Obrigatório |
   | --- | --- | :---: |
   | `name` | Nome do ad break, como precedente, intermediário e posterior. | Sim |
   | `position` | A posição do número do ad break no conteúdo, começando com 1. | Sim |
   | `startTime` | Valor do indicador de reprodução no início do ad break. | Sim |

1. Call `trackEvent()` with `AdBreakStart` in the `MediaHeartbeat` instance to begin tracking the ad break.

1. Identifique o início do anúncio e crie uma instância `AdObject` usando as informações do anúncio.

   `AdObject` referência:

   | Nome da variável | Descrição | Obrigatório |
   | --- | --- | :---: |
   | `name` | Nome amigável do anúncio. | Sim |
   | `adId` | Identificador exclusivo para o anúncio. | Sim |
   | `position` | A posição do número do anúncio no ad break, começando com 1. | Sim |
   | `length` | Duração do anúncio | Sim |

1. Opcionalmente, anexe metadados padrão e/ou de anúncio à sessão de rastreamento por meio de variáveis de dados de contexto.

   * **Metadados de publicidade padrão -** Para metadados de anúncios padrão, crie um dicionário de pares de valores-chave de Metadados de publicidade padrão usando as chaves da sua plataforma.
   * **Metadados de anúncio personalizados -** Para metadados personalizados, crie um objeto de variável para as variáveis de dados personalizadas e preencha com os dados do anúncio atual.

1. Call `trackEvent()` with the `AdStart` event in the `MediaHeartbeat` instance to begin tracking the ad playback.

   Inclua uma referência na variável de metadados personalizada (ou um objeto vazio) como o terceiro parâmetro na chamada de evento.

1. When the ad playback reaches the end of the ad, call `trackEvent()` with the `AdComplete` event.

1. Se a reprodução do anúncio não tiver sido concluída porque o usuário optou por ignorar o anúncio, rastreie o evento `AdSkip`.
1. Se houver algum anúncio adicional em um mesmo `AdBreak`, repita novamente as etapas 3 a 7.
1. O ad break está concluído, use o evento `AdBreakComplete` para rastreá-lo.

>[!IMPORTANT]
>
>Certifique-se de NÃO incrementar o indicador de reprodução (`l:event:playhead`) do player de conteúdo durante a reprodução do anúncio (`s:asset:type=ad`). Se você fizer isso, as métricas de Tempo gasto do conteúdo serão afetadas negativamente.

O código de amostra a seguir utiliza o JavaScript 2.x SDK para um player de mídia HTML5.

```js
/* Call on ad break start */ 
 
if (e.type == "ad break start") { 
    var adBreakObject = MediaHeartbeat.createAdBreakObject("mid-roll", 2, 500); 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject); 
}; 
 
/* Call on ad start */ 
if (e.type == "ad start") { 
    var adObject = MediaHeartbeat.createAdObject("PepsiOne", "123456ab", 1, 30); 
    /* Set custom context data */ 
    var adCustomMetadata = { 
        affiliate:"Sample affiliate", 
        campaign:"Sample ad campaign", 
        creative:"Sample creative" 
    } 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata); 
}; 
 
/* Call on ad complete */ 
if (e.type == "ad complete") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete); 
}; 
 
/* Call on ad skip */ 
if (e.type == "ad skip") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip); 
}; 
     
/* Call on ad break complete */ 
if (e.type == "ad break complete") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete); 
}; 
```

