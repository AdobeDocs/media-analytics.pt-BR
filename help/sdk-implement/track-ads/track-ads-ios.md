---
title: Saiba como rastrear anúncios no iOS
description: Implementar o rastreamento de anúncios em aplicativos iOS usando o SDK do Media.
uuid: e979e679-cde5-4c30-8f34-867feceac13a
exl-id: a352bca9-bcfc-4418-b2a2-c9b1ad226359
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 98%

---

# Rastrear anúncios no iOS{#track-ads-on-ios}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação usando os SDKs 2.x. Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores 1.x aqui: [Baixar SDKs.](/help/sdk-implement/download-sdks.md)

## Constantes de rastreamento do anúncio

| Nome da constante | Descrição   |
|---|---|
| `ADBMediaHeartbeatEventAdBreakStart` | Constante para rastrear o evento AdBreak Start |
| `ADBMediaHeartbeatEventAdBreakComplete` | Constante para rastrear o evento AdBreak Complete |
| `ADBMediaHeartbeatEventAdStart` | Constante para rastrear o evento Ad Start |
| `ADBMediaHeartbeatEventAdComplete` | Constante para rastrear o evento Ad Complete |
| `ADBMediaHeartbeatEventAdSkip` | Constante para rastrear o evento Ad Skip |

## Etapas da implementação

1. Identifique o início do limite do ad break, incluindo o anúncio precedente, e crie um `AdBreakObject` usando as informações do ad break.

   `AdBreakObject` referência:

   | Nome da variável | Descrição | Obrigatório |
   | --- | --- | :---: |
   | `name` | Nome do ad break, como precedente, intermediário e posterior. | Sim |
   | `position` | A posição do número do ad break no conteúdo, começando com 1. | Sim |
   | `startTime` | Valor do indicador de reprodução no início do ad break. | Sim |

   Criação do objeto Ad break:

   ```
   id adBreakObject = [ADBMediaHeartbeat createAdBreakObjectWithName:[ADBREAK_NAME] 
                               position:[POSITION]  
                               startTime:[START_TIME]];
   ```

1. Chame `trackEvent()` com `AdBreakStart` na instância `MediaHeartbeat` para começar a rastrear o ad break:

   ```
   - (void)onAdBreakStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakStart  
                        mediaObject:adBreakObject  
                        data:nil]; 
   }
   ```

1. Identifique o início do anúncio e crie uma instância `AdObject` usando as informações do anúncio.

   `AdObject` referência:

   | Nome da variável | Descrição | Obrigatório |
   | --- | --- | :---: |
   | `name` | Nome amigável do anúncio. | Sim |
   | `adId` | identificador exclusivo para o anúncio. | Sim |
   | `position` | A posição do número do anúncio no ad break, começando com 1. | Sim |
   | `length` | Duração do anúncio | Sim |

   Criação do objeto de anúncio:

   ```
   id adObject = [ADBMediaHeartbeat createAdObjectWithName:[AD_NAME] 
                                    adId:[AD_ID] 
                                    position:[POSITION] 
                                    length:[LENGTH]];
   ```

1. Opcionalmente, anexe metadados padrão e/ou de anúncio à sessão de rastreamento de mídia por meio de variáveis de dados de contexto.

   * [Implementar Metadados de publicidade padrão no iOS](/help/sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
   * **Metadados de anúncio personalizados -** Para metadados personalizados, crie um objeto de variável para as variáveis de dados personalizadas e preencha com os dados do anúncio atual:

      ```
      NSMutableDictionary *adDictionary = [[NSMutableDictionary alloc] init]; 
      [adDictionary setObject:@"Sample affiliate" forKey:@"affiliate"]; 
      [adDictionary setObject:@"Sample campaign" forKey:@"campaign"]; 
      [adDictionary setObject:@"Sample creative" forKey:@"creative"];
      ```

1. Chame `trackEvent()` com o evento `AdStart` na instância `MediaHeartbeat` para começar a rastrear a reprodução de anúncio.

   Inclua uma referência na variável de metadados personalizada (ou um objeto vazio) como o terceiro parâmetro na chamada de evento:

   ```
   - (void)onAdStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdStart  
                        mediaObject:adObject  
                        data:adDictionary]; 
   }
   ```

1. Quando a reprodução atingir o fim do anúncio, chame `trackEvent()` com o evento `AdComplete`.

   ```
   - (void)onAdComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. Se a reprodução do anúncio não tiver sido concluída porque o usuário optou por ignorar o anúncio, rastreie o evento `AdSkip`.

   ```
   - (void)onAdSkip:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdSkip  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. Se houver algum anúncio adicional em um mesmo `AdBreak`, repita novamente as etapas 3 a 7.
1. O ad break está concluído, use o evento `AdBreakComplete` para rastrear:

   ```
   - (void)onAdBreakComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

Consulte o cenário de rastreamento [Reprodução de VOD com anúncios antes da exibição](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md) para obter mais informações.
