---
seo-title: Rastrear anúncios no Android
title: Rastrear anúncios no Android
uuid: 4 a 4249 fb-dc 39-4947-a 14 d-a 51 d 972 f 32 d 4
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Rastrear anúncios no Android{#track-ads-on-android}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação usando os sdks 2. x. Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores 1.x aqui: [Baixar SDKs.](../../sdk-implement/download-sdks.md)

## Constantes de rastreamento do anúncio

| Nome da constante | Descrição |
| --- | --- |
| `MediaHeartbeat.Event.AdBreakStart` | Constante para rastrear o evento AdBreak Start |
| `MediaHeartbeat.Event.AdBreakComplete` | Constante para rastrear o evento AdBreak Complete |
| `MediaHeartbeat.Event.AdStart` | Constante para rastrear o evento Ad Start |
| `MediaHeartbeat.Event.AdComplete` | Constante para rastrear o evento Ad Complete |
| `MediaHeartbeat.Event.AdSkip` | Constante para rastrear o evento Ad Skip |

## Etapas de implementação

1. Identifique o início do limite do ad break, incluindo o anúncio precedente, e crie um `AdBreakObject` usando as informações do ad break.

   `AdBreakObject` referência:

   | Nome da variável | Descrição | Obrigatório |
   | --- | --- | :---: |
   | `name` | Nome do ad break, como precedente, intermediário e posterior. | Sim |
   | `position` | A posição do número do ad break no conteúdo, começando com 1. | Sim |
   | `startTime` | Valor do indicador de reprodução no início do ad break. | Sim |

   Criação do objeto Ad break:

   ```java
   MediaObject adBreakInfo =  
     MediaHeartbeat.createAdBreakObject(<ADBREAK_NAME>,  
                                        <POSITION>,  
                                        <START_TIME>);
   ```

1. Call `trackEvent()` with `AdBreakStart` in the `MediaHeartbeat` instance to begin tracking the ad break:

   ```java
   public void onAdBreakStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart,  
                             adBreakInfo,  
                             null); 
   }
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

   ```java
   MediaObject adInfo =  
     MediaHeartbeat.createAdObject(<AD_NAME> 
                                   <AD_ID>,  
                                   <POSITION>,  
                                   <LENGTH>);
   ```

1. Como opção, anexe metadados padrão e/ou de anúncio à sessão de rastreamento de mídia por meio das variáveis de dados de contexto.

   * [Implementar Metadados de publicidade padrão no Android](../../sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
   * **Metadados de anúncio personalizados -** Para metadados personalizados, crie um objeto de variável para as variáveis de dados personalizadas e preencha com os dados do anúncio atual:

      ```java
      // Setting Ad Metadata 
      HashMap<String, String> adMetadata = new HashMap<String, String>(); 
      adMetadata.put("affiliate", "Sample affiliate"); 
      adMetadata.put("campaign", "Sample ad campaign");
      ```

1. Call `trackEvent()` with the `AdStart` event in the `MediaHeartbeat` instance to begin tracking the ad playback.

   Inclua uma referência na variável de metadados personalizada (ou um objeto vazio) como o terceiro parâmetro na chamada de evento:

   ```java
   public void onAdStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdStart,  
                             adInfo,  
                             adMetadata); 
   }
   ```

1. When the ad playback reaches the end of the ad, call `trackEvent()` with the `AdComplete` event:

   ```java
   public void onAdComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdComplete, null, null); 
   }
   ```

1. Se a reprodução do anúncio não tiver sido concluída porque o usuário optou por ignorar o anúncio, rastreie o evento `AdSkip`

   ```java
   public void onAdSkip(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdSkip, null, null); 
   }
   ```

1. Se houver algum anúncio adicional em um mesmo `AdBreak`, repita novamente as etapas 3 a 7.
1. O ad break está concluído, use o evento `AdBreakComplete` para rastrear:

   ```java
   public void onAdBreakComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete, null, null); 
   }
   ```

Consulte o cenário de rastreamento [Reprodução de VOD com anúncios antes da exibição](../../sdk-implement/tracking-scenarios/vod-preroll-ads.md) para obter mais informações.
