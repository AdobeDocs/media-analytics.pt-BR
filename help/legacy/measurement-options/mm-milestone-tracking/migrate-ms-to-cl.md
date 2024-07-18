---
title: Saiba mais sobre a migração do Marco para Link personalizado
description: Saiba como alterar as variáveis de Marco para os métodos de Link personalizado e de módulo de Marco para a sintaxe de Link personalizado.
uuid: 1c8edde5-0ef1-4bc0-a62d-1747f4907f09
exl-id: 732079f4-3eb8-4b9a-892b-25a1c9332be4
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 9ba64b68efec5dd8b52010ac1a13afd7703448d0
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 97%

---

# Migração do Marco para Link personalizado{#migrating-from-milestone-to-custom-link}

## Visão geral  {#overview}

Os principais conceitos de medição de vídeo são os mesmos para o rastreamento de Marco e Link personalizado, que estão realizando eventos do reprodutor de vídeo e mapeando-os para métodos de análise, além de capturar metadados e valores de reprodutores e mapeá-los para variáveis&#x200B;de análise. A abordagem de Link personalizado deve ser considerada como uma diminuição e simplificação da implementação e dos dados coletados. Com a solução de Link personalizado, nenhuma variável ou método é predefinido para a medição de vídeo, isso requer uma configuração personalizada completa. Deve ser possível atualizar o código de evento do reprodutor para apontar as chamadas de rastreamento de link personalizado para eventos básicos do reprodutor, como início e conclusão. Consulte [Guia de implementação de link personalizado](/help/legacy/measurement-options/cl-in-aa/cl-impl-guide.md) para obter mais informações.

As tabelas a seguir fornecem as traduções entre as soluções de Marco e Link personalizado.

## Guia de migração {#migration-guide}

### Referência da variável de vídeo

| Métrica de marco | Tipo de variável | Link personalizado |
| --- | --- | --- |
| Conteúdo | Expiração da eVar <br> padrão: Visita | Definir a própria eVar. |
| Tipo de conteúdo | Expiração da eVar <br> padrão: Visualização de página | Definir a própria eVar. |
| Tempo gasto no conteúdo | Tipo de evento:<br> Contador | Definir o próprio evento. |
| Inicialização de vídeo | Tipo de evento:<br> Contador | Definir o próprio evento. |
| Término de vídeo | Tipo de evento:<br> Contador | Definir o próprio evento. |

### Variáveis do módulo de mídia

| Milestone | Sintaxe do Milestone | Link personalizado | Sintaxe de link personalizado |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | linkTrackVars | `s.linkTrackVars` <br> `  = 'events,` <br> `  contextData.video.name’;` <br> `  s.contextData["video.name"]` <br> `  = mediaName;` |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | N/D | O mapeamento de dados de contexto para eVars, as propriedades e os eventos agora são concluídos por meio de regras de processamento. |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | linkTrackVars | `s.linkTrackVars` <br> `  = 'events,` <br> `    prop10,` <br> `    eVar10,` <br> `    eVar12,` <br> `    eVar13,` <br> `    eVar15,` <br> `    contextData.` <br> `       video.name,` <br> `     contextData.` <br> `       video.view';` <br> |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | linkTrackEvents | `s.linkTrackEvents` <br> `  = 'event2';` |

### Variáveis opcionais

| Milestone | Sintaxe do Milestone | Link personalizado | Sintaxe de link personalizado |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | N/D | Não disponível. |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | N/D | Não disponível. |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | N/D | Não disponível. |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | N/D | Não disponível. |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | Definir eVar ou variável dos dados de contexto na chamada de link. | `s.contextData['video.player']` <br> `  = "CustomPlayer Name";` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | N/D | Não disponível. |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | N/D | Não disponível. |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | N/D | Não disponível. |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | N/D | Não disponível. |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | N/D | Não disponível. |

### Variáveis de rastreamento de anúncios

| Milestone | Sintaxe do Milestone | Link personalizado | Sintaxe de link personalizado |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | N/D | Não disponível. |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | N/D | Não disponível. |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | N/D | Não disponível. |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | N/D | Não disponível. |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | N/D | Não disponível. |

### Métodos do módulo de mídia

| Milestone | Sintaxe do Milestone | Link personalizado | Sintaxe de link personalizado |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | `s.tl()` | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.video.name,` <br> `     contextData.video.view';` <br> `s.linkTrackEvents ` <br> `  = 'event2';` <br> `s.prop10` <br> `   = mediaName;` <br> `s.eVar10` <br> `  = mediaName;` <br> `s.eVar12` <br> `  = "video";` <br> `s.eVar15` <br> `  = mediaPlayerName;` <br> `s.events` <br> `  = 'event2';` <br> `s.contextData['video.name']` <br> `  = mediaName;` <br> `s.contextData['video.view']` <br> `  = 'true';` <br> `s.tl(this,'o','Video Start');` |
| mediaName | `mediaName`: (obrigatório) o nome do vídeo conforme você quer que ele seja exibido nos relatórios de vídeo. | Definir eVar ou variável dos dados de contexto na chamada de link. | `s.prop10 = mediaName;` <br> `s.eVar10 = mediaName;` <br> `s.contextData['video.name']` <br> `  = mediaName;` |
| mediaLength | `mediaLength`: (obrigatório) a duração do vídeo, em segundos. | Definir eVar ou variável dos dados de contexto na chamada de link. | `s.contextData['video.length']` <br> `  = "90";` |
| mediaPlayerName | `mediaPlayerName`: (obrigatório) o nome do reprodutor de mídia utilizado para exibir o vídeo, conforme você quer que ele seja exibido nos relatórios de vídeo. | Definir eVar ou variável dos dados de contexto na chamada de link. | `s.contextData['video.player']` <br> `  = "CustomPlayer Name";` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | N/D | Não disponível. |
| name | `name`: (obrigatório) o nome ou a ID do anúncio. | N/D | Não disponível. |
| length | `length`: (obrigatório) a duração do anúncio. | N/D | Não disponível. |
| playerName | `playerName`: (obrigatório) o nome do reprodutor de mídia utilizado para exibir o anúncio. | N/D | Não disponível. |
| parentName | `parentName`: O nome ou a ID do conteúdo principal no qual o anúncio está incorporado. | N/D | Não disponível. |
| parentPod | `parentPod`: A posição, no conteúdo principal, da reprodução do anúncio. | N/D | Não disponível. |
| parentPodPosition | `parentPodPosition`: A posição, no pod, da reprodução do anúncio. | N/D | Não disponível. |
| CPM | `CPM`: O CPM ou o CPM criptografado (com prefixo &quot;~&quot;) que se aplica a essa reprodução. | N/D | Não disponível. |
| Media.click | `s.Media.click(name, offset)` | `s.tl()` | Usar uma chamada de análise de link personalizado para rastrear os cliques. |
| Media.close | `s.Media.close(mediaName)` | N/D | Não disponível. |
| Media.complete | `s.Media.complete(` <br> `  name,` <br> `  offset)` | `s.tl()` | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.video.name,` <br> `     contextData.video.complete';` <br> `s.linkTrackEvents ` <br> `  = 'event3';` <br> `s.prop10` <br> `   = mediaName;` <br> `s.eVar10` <br> `  = mediaName;` <br> `s.eVar12` <br> `  = "video";` <br> `s.eVar15` <br> `  = mediaPlayerName;` <br> `s.events` <br> `  = 'event3';` <br> `s.contextData['video.name']` <br> `  = mediaName;` <br> `s.contextData['video.complete']` <br> `  = 'true';` <br> `s.tl(this,'o','Video Complete');` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | N/D | Não disponível. |
| Media.stop | `s.Media.stop(` <br> `  mediaName,` <br> `  mediaOffset)` | N/D | Não disponível. |
| Media.monitor | `s.Media.monitor(s, media)` | Definir eVar ou variável dos dados de contexto na chamada de link. | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.` <br> `       video.name,` <br> `     contextData.` <br> `       video.view';` <br> `s.linkTrackEvents = 'event2';` |
| Media.track | `s.Media.track(` <br> `  mediaName)` | N/D | Não disponível. |
