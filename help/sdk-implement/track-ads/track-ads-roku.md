---
title: Rastrear anúncios no Roku
description: Implemente o rastreamento de anúncios nos aplicativos Roku usando o SDK de mídia.
uuid: b1567265-7043-4efa-a313-aaaa91c4bb01
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Rastrear anúncios no Roku{#track-ads-on-roku}

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

## Etapas de implementação

1. Identifique o início do limite do ad break, incluindo o anúncio precedente, e crie um `AdBreakObject` usando as informações do ad break.

   `AdBreakObject` referência:

   | Nome da variável | Descrição | Obrigatório |
   | --- | --- | :---: |
   | `name` | Nome do ad break, como precedente, intermediário e posterior. | Sim |
   | `position` | A posição do número do ad break, começando com 1. | Sim |
   | `startTime` | Valor do indicador de reprodução no início do ad break. | Sim |

   ```
   ‘ Create an adbreak info object 
   adBreakInfo = adb_media_init_adbreakinfo() 
   adBreakInfo.name = <ADBREAK_NAME> 
   adBreakInfo.startTime = <START_TIME> 
   adBreakInfo.position = <POSITION>
   ```

1. Call `trackEvent()` with `AdBreakStart` in the `MediaHeartbeat` instance to begin tracking the ad break:

   ```
   contextData = {} 
   ADBMobile().mediaTrackEvent(MEDIA_AD_BREAK_START, adBreakInfo, contextData)
   ```

1. Identifique o início do ativo de anúncio e crie uma instância `AdObject` usando as informações do anúncio.

   ```
   adInfo =  
     adb_media_init_adinfo(ad.title,  
                           ad.id,  
                           ad.position,  
                           ad.duration) 
   ```

1. Como opção, anexe metadados padronizados e/ou de anúncio à sessão de rastreamento de mídia por meio de variáveis de dados de contexto.

   * [Implementar Metadados de publicidade padrão no Roku](/help/sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   * **Metadados de anúncio personalizados -** Para metadados personalizados, crie um objeto de variável para as variáveis de dados personalizadas e preencha com os dados do ativo de anúncio atual:

      ```
      contextData = {} 
      contextData["adinfo1"] = "adinfo2" 
      contextData["adinfo2"] = "adinfo2"
      ```

1. Call `trackEvent()` with the `AdStart` event in the `MediaHeartbeat` instance to begin tracking the ad playback:

   ```
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_START, adInfo, contextData)
   ```

1. When the ad asset playback reaches the end of the ad, call `trackEvent()` with the `AdComplete` event.

   ```
   standardAdMetadata = {} 
   contextData = {} 
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_COMPLETE, adInfo, contextData)
   ```

1. Se a reprodução do anúncio não tiver sido concluída porque o usuário optou por ignorar o anúncio, rastreie o evento `AdSkip`

   ```
   contextData = {} 
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_SKIP, adInfo, contextData
   ```

1. Se houver algum anúncio adicional em um mesmo `AdBreak`, repita novamente as etapas 3 a 7.
1. O ad break está concluído, use o evento `AdBreakComplete` para rastrear:

   ```
   contextData = {} 
   ADBMobile().mediaTrackEvent(MEDIA_AD_BREAK_COMPLETE, adBreakInfo, contextData)
   ```

Consulte o cenário de rastreamento [Reprodução de VOD com anúncios antes da exibição](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md) para obter mais informações.
