---
title: Explicação sobre os anúncios de rastreamento
description: Visão geral da implementação do rastreamento de anúncios com o SDK de mídia.
uuid: 1607798b-c6ef-4d60-8e40-e958c345b09c
exl-id: c714d31f-3d08-4ded-a413-2762d53bec75
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 100%

---

# Visão geral{#overview}

As instruções a seguir fornecem orientação para a implementação usando os SDKs 2.x.

>[!IMPORTANT]
>
>Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores 1.x aqui: [Baixar SDKs.](/help/getting-started/download-sdks.md)

A reprodução do anúncio inclui o rastreamento de ad breaks, anúncios iniciados, anúncios concluídos e anúncios ignorados. Use a API do reprodutor de mídia para identificar eventos importantes do reprodutor e preencher as variáveis de anúncio obrigatórias e opcionais. Consulte a lista abrangente de metadados aqui: [Parâmetros de anúncios.](../../implementation/variables/ad-parameters.md)

## Eventos do player {#player-events}


### No início de pausa de anúncio

>[!NOTE]
>Incluindo precedente

* Crie uma instância de objeto `adBreak` para o ad break. Por exemplo, `adBreakObject`.

* Chame `trackEvent` para iniciar o ad break com `adBreakObject`.

### Em cada início de ativo de anúncio

* Crie a instância do objeto de anúncio para o ativo de anúncio. Por exemplo, `adObject`.
* Preencha os metadados do anúncio, `adCustomMetadata`.
* Chame `trackEvent` para iniciar o anúncio.

### Em cada conclusão de anúncio

* Chame `trackEvent` para concluir o anúncio.

### Ao ignorar o anúncio

* Chame `trackEvent` para o anúncio ignorado.

### Na conclusão do ad break

* Chame `trackEvent` para concluir o ad break.

## Implementar o rastreamento de anúncios {#implement-ad-tracking}

### Constantes de rastreamento do anúncio

| Nome da constante | Descrição   |
|---|---|
| `AdBreakStart` | Constante para rastrear o evento AdBreak Start |
| `AdBreakComplete` | Constante para rastrear o evento AdBreak Complete |
| `AdStart` | Constante para rastrear o evento Ad Start |
| `AdComplete` | Constante para rastrear o evento Ad Complete |
| `AdSkip` | Constante para rastrear o evento Ad Skip |

### Etapas da implementação

1. Identifique o início do limite do ad break, incluindo o anúncio precedente, e crie um `AdBreakObject` usando as informações do ad break.

   `AdBreakObject` referência:

   | Nome da variável | Descrição | Obrigatório |
   | --- | --- | :---: |
   | `name` | Nome do ad break, como precedente, intermediário e posterior. | Sim |
   | `position` | A posição do número do ad break no conteúdo, começando com 1. | Sim |
   | `startTime` | Valor do indicador de reprodução no início do ad break. | Sim |

1. Chame `trackEvent()` com `AdBreakStart` na instância `MediaHeartbeat` para começar a rastrear o ad break.

1. Identifique o início do anúncio e crie uma instância `AdObject` usando as informações do anúncio.

   `AdObject` referência:

   | Nome da variável | Descrição | Obrigatório |
   | --- | --- | :---: |
   | `name` | Nome amigável do anúncio. | Sim |
   | `adId` | identificador exclusivo para o anúncio. | Sim |
   | `position` | A posição do número do anúncio no ad break, começando com 1. | Sim |
   | `length` | Duração do anúncio | Sim |

1. Opcionalmente, anexe metadados padrão e/ou de anúncio à sessão de rastreamento por meio de variáveis de dados de contexto.

   * **Metadados de publicidade padrão -** Para metadados de anúncios padrão, crie um dicionário de pares de valores-chave de Metadados de publicidade padrão usando as chaves da sua plataforma.
   * **Metadados de anúncio personalizados -** Para metadados personalizados, crie um objeto de variável para as variáveis de dados personalizadas e preencha com os dados do anúncio atual.

1. Chame `trackEvent()` com o evento `AdStart` na instância `MediaHeartbeat` para começar a rastrear a reprodução de anúncio.

   Inclua uma referência na variável de metadados personalizada (ou um objeto vazio) como o terceiro parâmetro na chamada de evento.

1. Quando a reprodução atingir o fim do anúncio, chame `trackEvent()` com o evento `AdComplete`.

1. Se a reprodução do anúncio não tiver sido concluída porque o usuário optou por ignorar o anúncio, rastreie o evento `AdSkip`.
1. Se houver algum anúncio adicional em um mesmo `AdBreak`, repita novamente as etapas 3 a 7.
1. O ad break está concluído, use o evento `AdBreakComplete` para rastreá-lo.

>[!IMPORTANT]
>
>Certifique-se de NÃO incrementar o indicador de reprodução do reprodutor de conteúdo (`l:event:playhead`) durante a reprodução do anúncio (`s:asset:type=ad`). Se você fizer isso, as métricas de Tempo gasto do conteúdo serão afetadas negativamente.

O código de exemplo a seguir usa o SDK 2.x do JavaScript para um reprodutor de mídia HTML5.

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
