---
seo-title: Rastrear anúncios no Chromecast
title: Rastrear anúncios no Chromecast
uuid: 7 b 1 f 584 a -3472-416 c -944 c -5 f 5 ea 0 ee 5ee 5ee
translation-type: tm+mt
source-git-commit: 2bf7cfd1e50309ce1ab8de0325d666ed209fbf5b

---


# Rastrear anúncios no Chromecast{#track-ads-on-chromecast}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação usando os sdks 2. x. Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores 1.x aqui: [Baixar SDKs.](../../sdk-implement/download-sdks.md)

## Constantes de rastreamento do anúncio

| Nome da constante | Descrição  |
|---|---|
| `AdBreakStart` | Constante para rastrear o evento AdBreak Start |
| `AdBreakComplete` | Constante para rastrear o evento AdBreak Complete |
| `AdStart` | Constante para rastrear o evento Ad Start |
| `AdComplete` | Constante para rastrear o evento Ad Complete |
| `AdSkip` | Constante para rastrear o evento Ad Skip |

## Etapas de implementação

1. Identifique o início do limite do ad break, incluindo o anúncio precedente, e crie um `AdBreakObject` usando as informações do ad break.

   Criação do objeto Ad break:[ createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createAdBreakObject)

   ```
   adBreakInfo = ADBMobile.media.createAdBreakObject("First Ad-Break", 1, AD_BREAK_START_TIME, playerName); 
   ```

1. Call `trackEvent()` with `AdBreakStart` in the `MediaHeartbeat` instance to begin tracking the ad break: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakStart, getAdBreakInfo());
   ```

1. Identifique o início do ativo de anúncio e crie uma instância `AdObject` usando as informações do anúncio.

   Criação do objeto de anúncio:[ createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createAdObject)

   ```
   adInfo = ADBMobile.media.createAdObject("Sample ad", "001", 1, AD_LENGTH); 
   ```

1. Como opção, anexe metadados padrão e/ou de anúncio à sessão de rastreamento de mídia por meio das variáveis de dados de contexto.

   * **Metadados de publicidade padrão -** Para metadados de anúncios padrão, crie um dicionário de pares de valores-chave de Metadados de publicidade padrão usando as chaves da sua plataforma:
   * **Metadados de anúncio personalizados -** Para metadados personalizados, crie um objeto de variável para as variáveis de dados personalizadas e preencha com os dados do ativo de anúncio atual:

1. Call `trackEvent()` with the `AdStart` event to begin tracking the ad playback.

   Inclua uma referência na variável de metadados personalizada (ou um objeto vazio) como o terceiro parâmetro na chamada de evento: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, getAdInfo(), adContextData);
   ```

1. When the ad asset playback reaches the end of the ad, call `trackEvent()` with the `AdComplete` event: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdComplete); 
   ```

1. Se houver algum anúncio adicional em um mesmo `AdBreak`, repita novamente as etapas 3 a 6.
1. O ad break está concluído, use o evento `AdBreakComplete` para rastrear: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakComplete, getAdBreakInfo());
   ```

Consulte o cenário de rastreamento [Reprodução de VOD com anúncios antes da exibição](../../sdk-implement/tracking-scenarios/vod-preroll-ads.md) para obter mais informações.
