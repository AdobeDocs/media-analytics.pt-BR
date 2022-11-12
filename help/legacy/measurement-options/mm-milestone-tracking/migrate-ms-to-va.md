---
title: Saiba como migrar do Marco para o Media Analytics
description: Saiba como alterar variáveis de Marco para Métricas do Media Analytics e métodos do módulo de Marco para sintaxe do Media Analytics.
uuid: fdc96146-af63-48ce-b938-c0ca70729277
exl-id: 655841ed-3a02-4e33-bbc9-46fb14302194
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 9ba64b68efec5dd8b52010ac1a13afd7703448d0
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 100%

---

# Migração do Marco para o Media Analytics {#migrating-from-milestone-to-media-analytics}

## Visão geral  {#overview}

Os conceitos principais de avaliação de vídeo são os mesmos para o Milestone e o Media Analytics, que está pegando eventos do player de vídeo e mapeando-os para métodos de análise, além de capturar metadados e valores de player e mapeá-los para variáveis de análise. A solução do Media Analytics surgiu do Milestone, mas muitos dos métodos e métricas são os mesmos, no entanto, a abordagem de configuração e o código mudaram bastante. Deve ser possível atualizar o código de evento do player para apontar para os novos métodos do Media Analytics. Consulte [Visão geral do SDK](/help/legacy/setup/legacy-setup-overview.md) e [Visão geral do rastreamento](/help/use-cases/track-av-playback/track-core-overview.md) para obter mais detalhes sobre a implementação do Media Analytics.

As tabelas a seguir fornecem as traduções entre as soluções de Marco e do Media Analytics.

## Guia de migração {#migration-guide}

### Referência da variável

| Métrica de marco | Tipo de variável | Métrica do Media Analytics |
| --- | --- | --- |
| Conteúdo | Expiração da eVar <br> padrão: Visita | Conteúdo |
| Tipo de conteúdo | Expiração da eVar <br> padrão: Visualização de página | Tipo de conteúdo |
| Tempo gasto no conteúdo | Tipo de evento:<br> Contador | Tempo gasto no conteúdo |
| Inicialização de vídeo | Tipo de evento:<br> Contador | Inicialização de vídeo |
| Término de vídeo | Tipo de evento:<br> Contador | Conteúdo concluído |


### Variáveis do módulo de mídia

| Milestone | Sintaxe do Milestone | Media Analytics | Sintaxe do Media Analytics |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | N/D | Todos os dados do Media Analytics são enviados somente com os Dados de contexto. |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | N/D | Os dados de contexto do Media Analytics são preenchidos automaticamente em variáveis reservadas. O mapeamento para eVars, as propriedades e os eventos que não são mais necessários no código de implementação. Os clientes podem mapear dados de contexto para variáveis usando regras de processamento. |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | N/D | Não é mais necessário, pois o mapeamento ocorre por meio de variáveis reservadas e regras de processamento. |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | N/D | Não é mais necessário, pois o mapeamento ocorre por meio de variáveis reservadas e regras de processamento. |

### Variáveis opcionais

| Marco | Sintaxe do Milestone | Media Analytics | Sintaxe do Media Analytics |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | N/D | Não fornecemos mais mapeamentos pré-criados de player. |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | N/D | Não fornecemos mais mapeamentos pré-criados de player. |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | N/D | A Conclusão de conteúdo é compatível apenas com um marcador de progresso de 100%. |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | N/D | A Conclusão de conteúdo é compatível apenas com um marcador de progresso de 100%. |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | Chave do SDK: playerName;<br> Chave da API: media.playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | N/D | O Media Analytics está definido para 10 segundos para conteúdo e 1 segundo para anúncios. Nenhuma outra opção está disponível. |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | N/D | O Media Analytics sempre rastreia marcadores de progresso em 10%, 25%, 50%, 75%, 95%. |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | N/D | O Media Analytics sempre rastreia marcadores de progresso em 10%, 25%, 50%, 75%, 95%. |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | N/D | O rastreamento automático não está mais disponível. |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | N/D | O rastreamento automático não está mais disponível. |

### Variáveis de rastreamento de anúncios

| Marco | Sintaxe do Milestone | Media Analytics | Sintaxe do Media Analytics |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | N/D | O Media Analytics está definido para 10 segundos para conteúdo e 1 segundo para anúncios. Nenhuma outra opção está disponível. |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | N/D | Os marcadores de progresso não são fornecidos por padrão para anúncios. Use as métricas calculadas para criar marcadores de progresso de anúncios. |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | N/D | Media Analytics está definido para 1 segundo para anúncios. Nenhuma outra opção está disponível. |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | N/D | O rastreamento automático não está mais disponível. |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | N/D | O rastreamento automático não está mais disponível. |

### Métodos do módulo de mídia

| Marco | Sintaxe do Milestone | Media Analytics | Sintaxe do Media Analytics |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | trackSessionStart | `trackSessionStart(` <br> `  mediaObject,` <br> `  contextData)` |
| mediaName | `mediaName`: (obrigatório) o nome do vídeo conforme você quer que ele seja exibido nos relatórios de vídeo. | name | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaLength | `mediaLength`: (obrigatório) a duração do vídeo, em segundos. | length | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaPlayerName | `mediaPlayerName`: (obrigatório) o nome do reprodutor de mídia utilizado para exibir o vídeo, conforme você quer que ele seja exibido nos relatórios de vídeo. | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | trackEvent | `mediaHeartbeat.trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdBreakStart, ` <br> `  adBreakObject);` <br> `...` <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdStart, ` <br> `  adObject, ` <br> `  adCustomMetadata);` |
| name | `name`: (obrigatório) o nome ou a ID do anúncio. | name | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| length | `length`: (obrigatório) a duração do anúncio. | length | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| playerName | `playerName`: (obrigatório) o nome do reprodutor de mídia utilizado para exibir o anúncio. | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| parentName | `parentName`: O nome ou a ID do conteúdo principal no qual o anúncio está incorporado. | N/D | Herdado automaticamente. |
| parentPod | `parentPod`: A posição, no conteúdo principal, da reprodução do anúncio. | position | `createAdBreakObject(` <br> `  name, ` <br> `  position, ` <br> `  startTime)` |
| parentPodPosition | `parentPodPosition`: A posição, no pod, da reprodução do anúncio. | position | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| CPM | `CPM`: O CPM ou o CPM criptografado (com prefixo &quot;~&quot;) que se aplica a essa reprodução. | N/D | Por padrão, não disponível no Media Analytics. |
| Media.click | `s.Media.click(name, offset)` | N/D | Usar uma chamada de análise de link personalizado para rastrear os cliques. |
| Media.close | `s.Media.close(mediaName)` | trackSessionEnd | `trackSessionEnd()` |
| Media.complete | `s.Media.complete(name, offset)` | trackComplete | `trackComplete()` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | trackPlay | `trackPlay()` |
| Media.stop | `s.Media.stop(mediaName, mediaOffset)` | trackPause<br> ou <br>trackEvent | `trackPause()` <br> ou `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  SeekStart)` <br> ou <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  BufferStart);` |
| Media.monitor | `s.Media.monitor(s, media)` | Use os metadados personalizados ou padrão para definir variáveis adicionais. | `var customVideoMetadata = ` <br> `{` <br> `  isUserLoggedIn: ` <br> `    "false",` <br> `  tvStation: ` <br> `    "Sample TV station",` <br> `  programmer: ` <br> `    "Sample programmer"` <br> `};` <br> `...` <br> `var standardVideoMetadata ` <br> `  = {};` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   EPISODE] = ` <br> `  "Sample Episode";` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   SHOW] = "Sample Show";` <br> `...` <br> `mediaObject.setValue(` <br> `  MediaHeartbeat.` <br> `  MediaObjectKey.` <br> `  StandardVideoMetadata, ` <br> `  standardVideoMetadata);` |
| Media.track | `s.Media.track(mediaName)` | N/D | A frequência de chamada de rastreamento é definida automaticamente. |
