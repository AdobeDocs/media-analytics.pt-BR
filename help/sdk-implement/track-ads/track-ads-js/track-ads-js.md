---
title: Rastrear anúncios usando o JavaScript 2.x
description: Implementar o rastreamento de anúncios nos aplicativos do navegador (JS) usando o SDK do Media.
uuid: 4d81d29c-c55d-4d48-b505-3260922712ff
translation-type: tm+mt
source-git-commit: 815965d1cd41e73e50666a89f4a7c450af5022da
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 97%

---


# Rastrear anúncios usando o JavaScript 2.x{#track-ads-on-javascript}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação usando os SDKs 2.x. Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores 1.x aqui: [Baixar SDKs.](/help/sdk-implement/download-sdks.md)

## Constantes de rastreamento do anúncio

| Nome da constante | Descrição   |
|---|---|
| `AdBreakStart` | Constante para rastrear o evento AdBreak Start |
| `AdBreakComplete` | Constante para rastrear o evento AdBreak Complete |
| `AdStart` | Constante para rastrear o evento Ad Start |
| `AdComplete` | Constante para rastrear o evento Ad Complete |
| `AdSkip` | Constante para rastrear o evento Ad Skip |

## Etapas da implementação

1. Identifique o início do limite do ad break, incluindo o anúncio precedente, e crie um `AdBreakObject` usando as informações do ad break.

   `AdBreakObject` referência:

   | Nome da variável | Descrição | Obrigatório |
   | --- | --- | :---: |
   | `name` | Nome do ad break, como precedente, intermediário e posterior. | Sim |
   | `position` | A posição do número do ad break, começando com 1. | Sim |
   | `startTime` | Valor do indicador de reprodução no início do ad break. | Sim |

   Criação do objeto Ad break:

   ```js
   var adBreakObject =  
     MediaHeartbeat.createAdBreakObject(<ADBREAK_NAME>,  
                                        <POSITION>,  
                                        <START_TIME>);
   ```

1. Chame `trackEvent()` com `AdBreakStart` na instância `MediaHeartbeat` para começar a rastrear o ad break:

   ```js
   mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);
   ```

1. Identifique o início do anúncio e crie uma instância `AdObject` usando as informações do anúncio.

   `AdObject` referência:

   | Nome da variável | Descrição | Obrigatório |
   | --- | --- | :---: |
   | `name` | Nome amigável do anúncio. | Sim |
   | `adId` | Identificador exclusivo para o anúncio. | Sim |
   | `position` | A posição do número do anúncio no ad break, começando com 1. | Sim |
   | `length` | Duração do anúncio | Sim |

   Criação do objeto de anúncio:

   ```js
   var adObject =  
     MediaHeartbeat.createAdObject(<AD_NAME>,  
                                   <AD_ID>,  
                                   <POSITION>,  
                                   <LENGTH>);
   ```

1. Opcionalmente, anexe metadados padrão e/ou de anúncio à sessão de rastreamento de mídia por meio de variáveis de dados de contexto.

   * [Implementar Metadados de publicidade padrão no JavaScript](/help/sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js.md)
   * **Metadados de anúncio personalizados -** Para metadados personalizados, crie um objeto de variável para as variáveis de dados personalizadas e preencha com os dados do anúncio atual:

      ```js
      /* Set custom context data */
      var adCustomMetadata = {
          affiliate: "Sample affiliate",
          campaign: "Sample ad campaign",
          creative: "Sample creative"
      };
      ```

1. Chame `trackEvent()` com o evento `AdStart` na instância `MediaHeartbeat` para começar a rastrear a reprodução de anúncio.

   Inclua uma referência na variável de metadados personalizada (ou um objeto vazio) como o terceiro parâmetro na chamada de evento:

   ```js
   _onAdStart = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdStart,  
                                       adObject,  
                                       adCustomMetadata);
   };
   ```

1. Quando a reprodução atingir o fim do anúncio, chame `trackEvent()` com o evento`AdComplete`:

   ```js
   _onAdComplete = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdComplete);
   };
   ```

1. Se a reprodução do anúncio não tiver sido concluída porque o usuário optou por ignorar o anúncio, rastreie o evento `AdSkip`

   ```js
   _onAdSkip = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdSkip);
   };
   ```

1. Se houver algum anúncio adicional em um mesmo `AdBreak`, repita novamente as etapas 3 a 7.
1. O ad break está concluído, use o evento `AdBreakComplete` para rastrear:

   ```js
   _onAdBreakComplete = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete);
   };
   ```

Consulte o cenário de rastreamento [Reprodução de VOD com anúncios antes da exibição](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md) para obter mais informações.