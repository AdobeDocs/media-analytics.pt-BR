---
title: Migração do Marco para o Media Analytics
description: null
uuid: fdc96146-af63-48ce-b938-c0ca70729277
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Migração do Marco para o Media Analytics {#migrating-from-milestone-to-media-analytics}

## Visão geral {#overview}

Os principais conceitos de medição de vídeo são os mesmos para Marco e Media Analytics, que estão realizando eventos do reprodutor de vídeo e mapeando-os para os métodos de análise, além de capturar metadados e valores do reprodutor e mapeá-los para variáveis&#x200B;de análise. A solução do Media Analytics surgiu no Marco, portanto, muitos dos métodos e métricas são os mesmos. No entanto, a abordagem e o código de configuração mudaram significativamente. Deve ser possível atualizar o código de evento do reprodutor para apontar para os novos métodos do Media Analytics. Consulte [Visão geral do SDK](/help/sdk-implement/setup/setup-overview.md) e [Visão geral do rastreamento](/help/sdk-implement/track-av-playback/track-core-overview.md) para obter mais detalhes sobre a implementação do Media Analytics.

As tabelas a seguir fornecem as traduções entre as soluções de Marco e do Media Analytics.

## Guia de migração {#migration-guide}

### Referência da variável

| Métrica de marco | Tipo de variável | Métrica do Media Analytics |
| --- | --- | --- |
| Conteúdo | eVar<br/><br/>Expiração padrão: visita | Conteúdo |
| Tipo de conteúdo | Expiração <br/>padrão do eVar: Visualização de página<br/> | Tipo de conteúdo |
| Tempo gasto no conteúdo | Tipo <br/>de evento: Contador<br/> | Tempo gasto no conteúdo |
| Inicialização de vídeo | Tipo <br/>de evento: Contador<br/> | Inicialização de vídeo |
| Término do vídeo | Tipo <br/>de evento: Contador<br/> | Conteúdo concluído |

### Variáveis do módulo de mídia

<table>
<thead>
<tr>
<th>Etapa
</th>
<th>Sintaxe do marco
</th>
<th>Media Analytics
</th>
<th>Sintaxe do Media Analytics
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.trackUsingContextData
</td>
<td>
<pre>
s.Media.trackUsingContextData = true;
</pre>
</td>
<td>N/D
</td>
<td>Todos os dados do Media Analytics são enviados somente usando os dados de contexto.
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
</td>
<td>
<pre>
s.Media.contextDataMapping = {
  "a.media.name":"eVar2,prop2",
  "a.media.segment":"eVar3",
  "a.contentType":"eVar1",
  "a.media.timePlayed":"event3",
  "a.media.view":"event1",
  "a.media.segmentView":"event2",
  "a.media.complete":"event7",
  "a.media.milestones": {
    25:"event4",
    50:"event5",
    75:"event6"
  }
};
</pre>
</td>
<td>N/D
</td>
<td>Os dados de contexto do Media Analytics são preenchidos automaticamente em variáveis reservadas. O mapeamento para eVars, as propriedades e os eventos que não são mais necessários no código de implementação. Os clientes podem mapear dados de contexto para variáveis usando regras de processamento.
</td>
</tr>
<tr>
<td>
Media.trackVars
</td>
<td>
<pre>
s.Media.trackVars = 
  "events,
  prop2,
  eVar1,
  eVar2,
  eVar3";
</pre>
</td>
<td>N/D
</td>
<td>Não é mais necessário, pois o mapeamento ocorre por meio de variáveis reservadas e regras de processamento.
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s.Media.trackEvents = 
  "event1,
  event2,
  event3,
  event4,
  event5,
  event6,
  event7"
</pre>
</td>
<td>N/D
</td>
<td>Não é mais necessário, pois o mapeamento ocorre por meio de variáveis reservadas e regras de processamento.
</td>
</tr>
</tbody>
</table>

### Variáveis opcionais

<table>
<thead>
<tr>
<th>Etapa
</th>
<th>Sintaxe do marco
</th>
<th>Media Analytics
</th>
<th>Sintaxe do Media Analytics
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.autoTrack
</td>
<td>
<pre>
s.Media.autoTrack = true;
</pre>
</td>
<td>N/D
</td>
<td>Os mapeamentos de reprodutores criados previamente não são mais fornecidos.
</td>
</tr>
<tr>
<td>
Media.autoTrackNetStreams
</td>
<td>
<pre>
s.Media.
  autoTrackNetStreams
  = true
</pre>
</td>
<td>N/D
</td>
<td>Os mapeamentos de reprodutores criados previamente não são mais fornecidos.
</td>
</tr>
<tr>
<td>
Media.completeByCloseOffset
</td>
<td>
<pre>
s.Media.
  completeByCloseOffset
  = true
</pre>
</td>
<td>N/D
</td>
<td>O Conteúdo concluído suporta apenas um marcador de 100% de progresso.
</td>
</tr>
<tr>
<td>
Media.completeCloseOffsetThreshold
</td>
<td>
<pre>
s.Media.
  completeCloseOffsetThreshold
  = 1
</pre>
</td>
<td>N/D
</td>
<td>O Conteúdo concluído suporta apenas um marcador de 100% de progresso.
</td>
</tr>
<tr>
<td>
Media.playerName
</td>
<td>
<pre>
s.Media.playerName = "Custom Player Name"
</pre>
</td>
<td>
Chave do SDK: playerName; 
Chave da API: media.playerName
</td>
<td>
<pre>
MediaHeartbeatConfig.
  playerName
</pre>
</p>
</td>
</tr>
<tr>
<td>
Media.trackSeconds
</td>
<td>
<pre>
s.Media.
  trackSeconds
  = 15
</pre>
</td>
<td>N/D
</td>
<td>O Media Analytics está definido para 10 segundos para conteúdo e 1 segundo para anúncios. Nenhuma outra opção está disponível.
</td>
</tr>
<tr>
<td>
Media.trackMilestones
</td>
<td>
<pre>
s.Media.
  trackMilestones
  = "25,50,75";
</pre>
</td>
<td>N/D
</td>
<td>Media Analytics sempre rastreia marcadores de progresso em 10%, 25%, 50%, 75%, 95%
</td>
</tr>
<tr>
<td>
Media.trackOffsetMilestones
</td>
<td>
<pre>
s.Media.
  trackOffsetMilestones
  = "20,40,60";
</pre>
</td>
<td>N/D
</td>
<td>Media Analytics sempre rastreia marcadores de progresso em 10%, 25%, 50%, 75%, 95%
</td>
</tr>
<tr>
<td>
Media.segmentByMilestones
</td>
<td>
<pre>
s.Media.segmentByMilestones = true;
</pre>
</td>
<td>N/D
</td>
<td>A faixa automática não está mais disponível
</td>
</tr>
<tr>
<td>
Media.segmentByOffsetMilestones
</td>
<td>
<pre>
s.Media.
  segmentByOffsetMilestones
  = true;
</pre>
</td>
<td>N/D
</td>
<td>A faixa automática não está mais disponível
</td>
</tr>
</tbody>
</table>

### Variáveis de rastreamento de anúncios

<table>
<thead>
<tr>
<th>Etapa
</th>
<th>Sintaxe do marco
</th>
<th>Media Analytics
</th>
<th>Sintaxe do Media Analytics
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.adTrackSeconds
</td>
<td>
<pre>
s.Media.
  adTrackSeconds
  = 15
</pre>
</td>
<td>N/D
</td>
<td>O Media Analytics está definido para 10 segundos para conteúdo e 1 segundo para anúncios. Nenhuma outra opção está disponível.
</td>
</tr>
<tr>
<td>
Media.adTrackMilestones
</td>
<td>
<pre>
s.Media.
  adTrackMilestones
  = "25,50,75";
</pre>
</td>
<td>N/D
</td>
<td>Os marcadores de progresso não são fornecidos aos anúncios por padrão. Use as métricas calculadas para criar marcadores de progresso de anúncios.
</td>
</tr>
<tr>
<td>
Media.adTrackOffsetMilestones
</td>
<td>
<pre>
s.Media.
  adTrackOffsetMilestones
  = "20,40,60";
</pre>
</td>
<td>N/D
</td>
<td>Media Analytics está definido para 1 segundo para anúncios. Nenhuma outra opção está disponível.
</td>
</tr>
<tr>
<td>
Media.adSegmentByMilestones
</td>
<td>
<pre>
s.Media.
  adSegmentByMilestones
  = true;
</pre>
</td>
<td>N/D
</td>
<td>A faixa automática não está mais disponível
</td>
</tr>
<tr>
<td>
Media.adSegmentByOffsetMilestones
</td>
<td>
<pre>
s.Media.
  adSegmentByOffsetMilestones
  = true;
</pre>
</td>
<td>N/D
</td>
<td>A faixa automática não está mais disponível
</td>
</tr>
</tbody>
</table>

### Métodos do módulo de mídia

<table>
<thead>
<tr>
<th>Etapa
</th>
<th>Sintaxe do marco
</th>
<th>Media Analytics
</th>
<th>Sintaxe do Media Analytics
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.open
</td>
<td>
<pre>
s.Media.open(mediaName,mediaLength,mediaPlayerName)
</pre>
</td>
<td>
<pre>
trackSessionStart
</pre>
</td>
<td>
<pre>
trackSessionStart(
  mediaObject, 
  contextData)
</pre>
</td>
</tr>
<tr>
<td>
mediaName — (obrigatório) O nome do vídeo conforme você quer que ele seja exibido nos relatórios de vídeo.
</td>
<td>
<pre>
mediaName
</pre>
</td>
<td>
<pre>
name
</pre>
</td>
<td>
<pre>
createMediaObject(
  name, 
  mediaId, 
  length, 
  streamType)
</pre>
</td>
</tr>
<tr>
<td>
mediaLength — (obrigatório) A duração do vídeo, em segundos.
</td>
<td>
<pre>
mediaLength
</pre>
</td>
<td>
<pre>
length
</pre>
</td>
<td>
<pre>
createMediaObject(
  name, 
  mediaId, 
  length, 
  streamType)
</pre>
</td>
</tr>
<tr>
<td>
mediaPlayerName — (obrigatório) O nome do reprodutor de mídia utilizado para exibir o vídeo, conforme você quer que ele seja exibido nos relatórios de vídeo.
</td>
<td>
<pre>
mediaPlayerName
</pre>
</td>
<td>
<pre>
playerName
</pre>
</td>
<td>
<pre>
MediaHeartbeatConfig.
  playerName
</pre>
</td>
</tr>
<tr>
<td>
Media.openAd
</td>
<td>
<pre>
s.Media.openAd(name,length,playerName,parentName,parentPod,parentPodPosition,CPM)
</pre>
</td>
<td>
<pre>
trackEvent
</pre>
</td>
<td>
<pre>
mediaHeartbeat.trackEvent(
  MediaHeartbeat.
    Evento.
    AdBreakStart, 
  adBreakObject);
...
trackEvent(
  MediaHeartbeat.
    Evento.
    AdStart, 
  adObject, 
  adCustomMetadata);
</pre>
</td>
</tr>
<tr>
<td>
name — (obrigatório) o nome ou a ID do anúncio.
</td>
<td>
<pre>
name
</pre>
</td>
<td>
<pre>
name
</pre>
</td>
<td>
<pre>
createAdObject(
  name, 
  adId, 
  position, 
  length)
</pre>
</td>
</tr>
<tr>
<td>
length
(obrigatório) a duração do anúncio.
</td>
<td>
<pre>
length
</pre>
</td>
<td>
<pre>
length
</pre>
</td>
<td>
<pre>
createAdObject(
  name, 
  adId, 
  position, 
  length)
</pre>
</td>
</tr>
<tr>
<td>
playerName — (obrigatório) O nome do reprodutor de mídia utilizado para exibir o anúncio.
</td>
<td>
<pre>
playerName
</pre>
</td>
<td>
<pre>
playerName
</pre>
</td>
<td>
<pre>
MediaHeartbeatConfig.
  playerName
</pre>
</td>
</tr>
<tr>
<td>
parentName — o nome ou a ID do conteúdo principal no qual o anúncio está incorporado.
</td>
<td>
<pre>
parentName
</pre>
</td>
<td>N/D
</td>
<td>Herdado automaticamente
</td>
</tr>
<tr>
<td>
parentPod — a posição, no conteúdo principal, em que o anúncio foi reproduzido.
</td>
<td>
<pre>
parentPod
</pre>
</td>
<td>
<pre>
position
</pre>
</td>
<td>
<pre>
createAdBreakObject(
  name, 
  position, 
  startTime)
</pre>
</td>
</tr>
<tr>
<td>
parentPodPosition — a posição, no pod, de reprodução do anúncio.
</td>
<td>
<pre>
parentPodPosition
</pre>
</td>
<td>
<pre>
position
</pre>
</td>
<td>
<pre>
createAdObject(
  name, 
  adId, 
  position, 
  length)
</pre>
</td>
</tr>
<tr>
<td>
CPM
O CPM ou o CPM criptografado (com prefixo “~”) que se aplica a essa reprodução.
</td>
<td>
<pre>
CPM
</pre>
</td>
<td>N/D
</td>
<td>Por padrão, não disponível no Media Analytics
</td>
</tr>
<tr>
<td>
Media.click
</td>
<td>
<pre>
s.Media.click(name,offset)
</pre>
</td>
<td>N/D
</td>
<td>Usar uma chamada de análise de link personalizado para rastrear os cliques.
</td>
</tr>
<tr>
<td>
Media.close
</td>
<td>
<pre>
s.Media.close(mediaName)
</pre>
</td>
<td>
<pre>
trackSessionEnd
</pre>
</td>
<td>
<pre>
trackSessionEnd()
</pre>
</td>
</tr>
<tr>
<td>
Media.complete
</td>
<td>
<pre>
s.Media.complete(name,offset)
</pre>
</td>
<td>
<pre>
trackComplete
</pre>
</td>
<td>
<pre>
trackComplete()
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.play
</pre>
</td>
<td>
<pre>
s.Media.play(name,offset,segmentNum,segment,segmentLength)
</pre>
</td>
<td>
<pre>
trackPlay
</pre>
</td>
<td>
<pre>
trackPlay()
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.stop
</pre>
</td>
<td>
<pre>
s.Media.stop(mediaName,mediaOffset)
</pre>
</td>
<td>
<pre>
trackPause
</pre> ou 
<pre>
trackEvent
</pre>
</td>
<td>
<pre>
trackPause()
</pre> 
ou
<pre>
trackEvent(
  MediaHeartbeat.
  Evento.
  SeekStart)
</pre> ou
<pre>
trackEvent(
  MediaHeartbeat.
  Evento.
  BufferStart);
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.monitor
</pre>
</td>
<td>
<pre>
s.Media.monitor(s, media)
</pre>
</td>
<td>Use os metadados personalizados ou padrão para definir variáveis adicionais.
</td>
<td>
<pre>
var customVideoMetadata = 
{
  isUserLoggedIn: 
    "false",
  tvStation: 
    "Sample TV station",
  programmer: 
    "Sample programmer"
};
...
var standardVideoMetadata 
  = {};
standardVideoMetadata
  [MediaHeartbeat.
   VideoMetadataKeys.
   EPISODE] = 
  "Episódio de amostra";
standardVideoMetadata
  [MediaHeartbeat.
   VideoMetadataKeys.
   SHOW] = "Show de amostra";
...
mediaObject.setValue(
  MediaHeartbeat.
  MediaObjectKey.
  StandardVideoMetadata, 
  standardVideoMetadata);
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.track
</pre>
</td>
<td>
<pre>
s.Media.track(mediaName)
</pre>
</td>
<td>N/D
</td>
<td>O rastreamento da frequência de chamada é automaticamente definido.
</td>
</tr>
</tbody>
</table>

