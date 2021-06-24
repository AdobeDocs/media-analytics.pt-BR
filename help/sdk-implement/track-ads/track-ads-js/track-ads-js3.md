---
title: Saiba como rastrear anúncios usando o JavaScript 3.x
description: Implementar o rastreamento de anúncios nos aplicativos do navegador (JS) usando o SDK do Media.
exl-id: 6b34b2c0-5e50-471a-b52c-b9c760fa3169
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 85%

---

# Rastrear anúncios usando o JavaScript 3.x{#track-ads-on-javascript}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação usando os SDKs 3.x. Se estiver implementando uma versão anterior do SDK, você pode baixar os Guias dos desenvolvedores Anterior aqui: [Baixar SDKs.](/help/sdk-implement/download-sdks.md)

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

   | Nome da variável | Tipo | Descrição |
   | --- | --- | --- |
   | `name` | string | String não vazia que indica o nome do adbreak (antes da exibição, intermediário e posterior). |
   | `position` | número | A posição do número do ad break, começando com 1. |
   | `startTime` | número | Valor do indicador de reprodução no início do ad break. |

   Criação do objeto Ad break:

   ```js
   var adBreakObject =
     ADB.Media.createAdBreakObject(<ADBREAK_NAME>,
                                      <POSITION>,
                                      <START_TIME>);
   ```

1. Chame `trackEvent()` com `AdBreakStart` na instância `MediaHeartbeat` para começar a rastrear o ad break:

   ```js
   tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakObject);
   ```

1. Identifique o início do anúncio e crie uma instância `AdObject` usando as informações do anúncio.

   `AdObject` referência:

   | Nome da variável | Tipo | Descrição |
   | --- | --- | --- |
   | `name` | string | String não vazia que indica o nome da publicidade. |
   | `adId` | string | String não vazia que indica o identificador de anúncio. |
   | `position` | número | A posição do número do anúncio no adbreak, começando com 1. |
   | `length` | número | Número positivo que indica a duração do anúncio. |

   Criação do objeto de anúncio:

   ```js
   var adObject =
     ADB.Media.createAdObject.createAdObject(<AD_NAME>,
                                   <AD_ID>,
                                   <POSITION>,
                                   <LENGTH>);
   ```

1. Opcionalmente, anexe metadados padrão e/ou de anúncio à sessão de rastreamento de mídia por meio de variáveis de dados de contexto.

   * [Implementar Metadados de publicidade padrão no JavaScript](/help/sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
   * **Metadados de anúncio personalizados -** Para metadados personalizados, crie um objeto de variável para as variáveis de dados personalizadas e preencha com os dados do anúncio atual:

      ```js
      /* Set context data */
      // Standard metadata keys provided by adobe.
      adMetadata[ADB.Media.AdMetadataKeys]  ="Sample Advertiser";
      adMetadata[ADB.Media.AdMetadataKeys] = "Sample Campaign";
      
      // Custom metadata keys
      adMetadata["affiliate"] = "Sample affiliate";
      adMetadata["campaign"] = "Sample ad campaign";
      adMetadata["creative"] = "Sample creative";
      ```

1. Chame `trackEvent()` com o evento `AdStart` na instância `MediaHeartbeat` para começar a rastrear a reprodução de anúncio.

   Inclua uma referência na variável de metadados personalizada (ou um objeto vazio) como o terceiro parâmetro na chamada de evento:

   ```js
   _onAdStart = function() {
       tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);
   };
   ```

1. Quando a reprodução atingir o fim do anúncio, chame `trackEvent()` com o evento`AdComplete`:

   ```js
   _onAdComplete = function() {
       tracker.trackEvent(ADB.Media.Event.AdComplete);
   };
   ```

1. Se a reprodução do anúncio não tiver sido concluída porque o usuário optou por ignorar o anúncio, rastreie o evento `AdSkip`

   ```js
   _onAdSkip = function() {
       tracker.trackEvent(ADB.Media.Event.AdSkip);
   };
   ```

1. Se houver algum anúncio adicional em um mesmo `AdBreak`, repita novamente as etapas 3 a 7.
1. O ad break está concluído, use o evento `AdBreakComplete` para rastrear:

   ```js
   _onAdBreakComplete = function() {
       tracker.trackEvent(ADB.Media.Event.AdBreakComplete);
   };
   ```

Consulte o cenário de rastreamento [Reprodução de VOD com anúncios antes da exibição](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md) para obter mais informações.
