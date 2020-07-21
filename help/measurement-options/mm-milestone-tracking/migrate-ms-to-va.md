---
title: Migração do Marco para o Media Analytics
description: null
uuid: fdc96146-af63-48ce-b938-c0ca70729277
translation-type: tm+mt
source-git-commit: aa2a230daa96b823f9963345ac4578799e59d3f5
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 77%

---


# Migração do Marco para o Media Analytics {#migrating-from-milestone-to-media-analytics}

## Visão geral {#overview}

Os conceitos principais de avaliação de vídeo são os mesmos para o Milestone e o Media Analytics, que está pegando eventos do player de vídeo e mapeando-os para métodos de análise, além de capturar metadados e valores de player e mapeá-los para variáveis de análise. A solução do Media Analytics surgiu do Milestone, mas muitos dos métodos e métricas são os mesmos, no entanto, a abordagem de configuração e o código mudaram bastante. Deve ser possível atualizar o código de evento do player para apontar para os novos métodos do Media Analytics. Consulte [Visão geral do SDK](/help/sdk-implement/setup/setup-overview.md) e [Visão geral do rastreamento](/help/sdk-implement/track-av-playback/track-core-overview.md) para obter mais detalhes sobre a implementação do Media Analytics.

As tabelas a seguir fornecem as traduções entre as soluções de Marco e do Media Analytics.

## Guia de migração {#migration-guide}

### Referência da variável

| Métrica de marco | Tipo de variável | Métrica do Media Analytics |
| --- | --- | --- |
| Conteúdo | Expiração <br>padrão do eVar: Visita | Conteúdo |
| Tipo de conteúdo | Expiração <br>padrão do eVar: Visualização de página | Tipo de conteúdo |
| Tempo gasto no conteúdo | Tipo <br>de evento: Contador | Tempo gasto no conteúdo |
| Inicialização de vídeo | Tipo <br>de evento: Contador | Inicialização de vídeo |
| Término de vídeo | Tipo <br>de evento: Contador | Conteúdo concluído |

### Variáveis do módulo de mídia

| Milestone | Sintaxe do Milestone | Media Analytics | Sintaxe do Media Analytics |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | N/D | Todos os dados do Media Analytics são enviados somente com os Dados de contexto. |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | N/D | Os dados de contexto do Media Analytics são preenchidos automaticamente em variáveis reservadas. O mapeamento para eVars, as propriedades e os eventos que não são mais necessários no código de implementação. Os clientes podem mapear dados de contexto para variáveis usando regras de processamento. |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | N/D | Não é mais necessário, pois o mapeamento ocorre por meio de variáveis reservadas e regras de processamento. |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | N/D | Não é mais necessário, pois o mapeamento ocorre por meio de variáveis reservadas e regras de processamento. |

### Variáveis opcionais

| Milestone | Sintaxe do Milestone | Media Analytics | Sintaxe do Media Analytics |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | N/D | Não fornecemos mais mapeamentos pré-criados de player. |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | N/D | Não fornecemos mais mapeamentos pré-criados de player. |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | N/D | A Conclusão de conteúdo é compatível apenas com um marcador de progresso de 100%. |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | N/D | A Conclusão de conteúdo é compatível apenas com um marcador de progresso de 100%. |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | SDK Key: playerName;<br> API Key: media.playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | N/D | O Media Analytics está definido para 10 segundos para conteúdo e 1 segundo para anúncios. Nenhuma outra opção está disponível. |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | N/D | Media Analytics sempre rastreia marcadores de progresso em 10%, 25%, 50%, 75%, 95% |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | N/D | Media Analytics sempre rastreia marcadores de progresso em 10%, 25%, 50%, 75%, 95% |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | N/D | O rastreamento automático não está mais disponível. |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | N/D | O rastreamento automático não está mais disponível. |

### Variáveis de rastreamento de anúncios

| Milestone | Sintaxe do Milestone | Media Analytics | Sintaxe do Media Analytics |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | N/D | O Media Analytics está definido para 10 segundos para conteúdo e 1 segundo para anúncios. Nenhuma outra opção está disponível. |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | N/D | Os marcadores de progresso não são fornecidos por padrão para anúncios. Use as métricas calculadas para criar marcadores de progresso de anúncios. |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | N/D | Media Analytics está definido para 1 segundo para anúncios. Nenhuma outra opção está disponível. |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | N/D | O rastreamento automático não está mais disponível. |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | N/D | O rastreamento automático não está mais disponível. |

### Métodos do módulo de mídia

| Milestone | Sintaxe do Milestone | Media Analytics | Sintaxe do Media Analytics |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | trackSessionStart | `trackSessionStart(` <br> `  mediaObject,` <br> `  contextData)` |
| mediaName - (Required) <br> The name of the video as you want it to appear in video reports. | `mediaName` | name | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaLength - (Required) <br> The length of the video in seconds. | `mediaLength` | length | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaPlayerName - (Required) <br> The name of the media player used to view the video, as you want it to appear in video reports. | `mediaPlayerName` | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | trackEvent | `mediaHeartbeat.trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdBreakStart, ` <br> `  adBreakObject);` <br> `...` <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdStart, ` <br> `  adObject, ` <br> `  adCustomMetadata);` |
| name - (Required) <br> The name or ID of the ad. | `name` | name | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| length - (Required) <br> The length of the ad. | `length` | length | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| playerName - (Required) <br> The name of the media player used to view the ad. | `playerName` | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| parentName <br> The name or ID of the primary content where the ad is embedded. | `parentName` | N/D | Herdado automaticamente |
| parentPod <br> The position in the primary content the ad was played. | `parentPod` | position | `createAdBreakObject(` <br> `  name, ` <br> `  position, ` <br> `  startTime)` |
| parentPodPosition <br> The position within the pod where the ad is played. | `parentPodPosition` | position | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| CPM <br> The CPM or encrypted CPM (prefixed with a &quot;~&quot;) that applies to this playback. | `CPM` | N/D | Por padrão, não disponível no Media Analytics. |
| Media.click | `s.Media.click(` <br> `  name,` <br> `  offset)` | N/D | Use uma chamada personalizada de análise de link para rastrear cliques. |
| Media.close | `s.Media.close(` <br> `  mediaName)` | trackSessionEnd | `trackSessionEnd()` |
| Media.complete | `s.Media.complete(` <br> `  name,` <br> `  offset)` | trackComplete | `trackComplete()` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | trackPlay | `trackPlay()` |
| Media.stop | `s.Media.stop(` <br> `  mediaName,` <br> `  mediaOffset)` | trackPause<br> ou <br>trackEvent | `trackPause()` <br> ou `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  SeekStart)` <br> ou <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  BufferStart);` |
| Media.monitor | `s.Media.monitor(s, media)` | Use metadados personalizados ou padrão para definir variáveis adicionais. | `var customVideoMetadata = ` <br> `{` <br> `  isUserLoggedIn: ` <br> `    "false",` <br> `  tvStation: ` <br> `    "Sample TV station",` <br> `  programmer: ` <br> `    "Sample programmer"` <br> `};` <br> `...` <br> `var standardVideoMetadata ` <br> `  = {};` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   EPISODE] = ` <br> `  "Sample Episode";` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   SHOW] = "Sample Show";` <br> `...` <br> `mediaObject.setValue(` <br> `  MediaHeartbeat.` <br> `  MediaObjectKey.` <br> `  StandardVideoMetadata, ` <br> `  standardVideoMetadata);` |
| Media.track | `s.Media.track(` <br> `  mediaName)` | N/D | A frequência de chamada de rastreamento é definida automaticamente. |

