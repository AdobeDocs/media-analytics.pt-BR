---
title: Migração do Marco para Link personalizado
description: null
uuid: 1c8edde5-0ef1-4bc0-a62d-1747f4907f09
translation-type: tm+mt
source-git-commit: ccdc3e170d125a76d798be7ce1fa5c12eef1f76a

---


# Migração do Marco para Link personalizado {#migrating-from-milestone-to-custom-link}

## Visão geral {#overview}

Os principais conceitos de medição de vídeo são os mesmos para o rastreamento de Marco e Link personalizado, que estão realizando eventos do reprodutor de vídeo e mapeando-os para métodos de análise, além de capturar metadados e valores de reprodutores e mapeá-los para variáveis&#x200B;de análise. A abordagem de Link personalizado deve ser considerada como uma diminuição e simplificação da implementação e dos dados coletados. Com a solução de Link personalizado, nenhuma variável ou método é predefinido para a medição de vídeo, isso requer uma configuração personalizada completa. Deve ser possível atualizar o código de evento do reprodutor para apontar as chamadas de rastreamento de link personalizado para eventos básicos do reprodutor, como início e conclusão. Consulte o [guia de implementação do Link personalizado](/help/measurement-options/cl-in-aa/cl-impl-guide.md) e o [Rastreamento de link manual usando um código de link personalizado](https://docs.adobe.com/content/help/en/media-analytics/using/measurement-options/cl-in-aa/cl-impl-guide.html) para obter mais detalhes.

As tabelas a seguir fornecem as traduções entre as soluções de Marco e Link personalizado.

## Guia de migração {#migration-guide}

### Referência da variável de vídeo

<table>
<thead>
<tr>
<th><strong>Métrica de marco</strong></th>
<th><strong>Tipo de variável</strong></th>
<th><strong>Link personalizado</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>Conteúdo</td>
<td>
<p>eVar</p>
<p>Expiração padrão: visita</p>
</td>
<td>Definir a própria eVar</td>
</tr>
<tr>
<td>Tipo de conteúdo</td>
<td>
<p>eVar</p>
<p>Expiração padrão: visualização de página</p>
</td>
<td>Definir a própria eVar</td>
</tr>
<tr>
<td>Tempo gasto no conteúdo</td>
<td>
<p>Evento</p>
<p>Tipo: contador</p>
</td>
<td>Definir o próprio evento</td>
</tr>
<tr>
<td>Inicialização de vídeo</td>
<td>
<p>Evento</p>
<p>Tipo: contador</p>
</td>
<td>Definir o próprio evento</td>
</tr>
<tr>
<td>Término de vídeo</td>
<td>
<p>Evento</p>
<p>Tipo: contador</p>
</td>
<td>Definir o próprio evento</td>
</tr>
</tbody>
</table>

### Variáveis do módulo de mídia

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Sintaxe do Milestone
</th>
<th>Link personalizado
</th>
<th>Link personalizado Sintaxe
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
s.Media.
  trackUsingContextData 
  = true;
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars
  = 'events, 
contextData.video.name’; 
s.contextData[‘video.name']
  = mediaName;
</pre>
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
</td>
<td>
<pre>
s.Media.
  contextDataMapping = {
  "a.media.name":
    "eVar2,prop2",
  "a.media.segment":
    "eVar3",
  "a.contentType":
    "eVar1",
  "a.media.timePlayed":
    "event3",
  "a.media.view":
    "event1",
  "a.media.segmentView":
    "event2",
  "a.media.complete":
    "event7",
  "a.media.milestones":{
    25:"event4",
    50:"event5",
    75:"event6"
  }
};
</pre>
</td>
<td>N/D
</td>
<td>O mapeamento de dados de contexto para eVars, as propriedades e os eventos agora são concluídos por meio de regras de processamento.
</td>
</tr>
<tr>
<td>
Media.trackVars
</td>
<td>
<pre>
s.Media.trackVars
  = "events,
     prop2,
     eVar1,
     eVar2,
     eVar3";
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars
  = 'events,
     prop10,
     eVar10,
     eVar12,
     eVar13,
     eVar15,
     contextData.
       video.name,
     contextData.
       video.view';
</pre>
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s.Media.trackEvents
  = "event1,
     event2,
     event3,
     event4,
     event5,
     event6,
     event7"
</pre>
</td>
<td>
linkTrackEvents
</td>
<td>
<pre>
s.linkTrackEvents
  = 'event2';
</pre>
</td>
</tr>
</tbody>
</table>

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Sintaxe do Milestone
</th>
<th>Link personalizado
</th>
<th>Link personalizado Sintaxe
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
s.Media.
  trackUsingContextData 
  = true;
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars
  = 'events, 
contextData.video.name’; 
s.contextData[‘video.name']
  = mediaName;
</pre>
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
  "a.media.milestones":{
    25:"event4",
    50:"event5",
    75:"event6"
  }
};
</pre>
</td>
<td>N/D
</td>
<td>O mapeamento de dados de contexto para eVars, as propriedades e os eventos agora são concluídos por meio de regras de processamento.
</td>
</tr>
<tr>
<td>
Media.trackVars
</td>
<td>
<pre>
s.Media.trackVars
  = "events,
     prop2,
     eVar1,
     eVar2,
     eVar3";
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars
  = 'events,
     prop10,
     eVar10,
     eVar12,
     eVar13,
     eVar15,
     contextData.
       video.name,
     contextData.
       video.view';
</pre>
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s.Media.trackEvents
  = "event1,
     event2,
     event3,
     event4,
     event5,
     event6,
     event7"
</pre>
</td>
<td>
linkTrackEvents
</td>
<td>
<pre>
s.linkTrackEvents
  = 'event2';
</pre>
</td>
</tr>
</tbody>
</table>

### Variáveis opcionais

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Sintaxe do Milestone
</th>
<th>Link personalizado
</th>
<th>Link personalizado Sintaxe
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
s.Media.autoTrack
  = true;
</pre>
</td>
<td>N/D
</td>
<td>Não disponível
</td>
</tr>
<tr>
<td>
Media.autoTrackNetStreams
</td>
<td>
<pre>
s.Media.autoTrackNetStreams = true
</pre>
</td>
<td>N/D
</td>
<td>Não disponível
</td>
</tr>
<tr>
<td>
Media.completeByCloseOffset
</td>
<td>
<pre>
s.Media.completeByCloseOffset = true
</pre>
</td>
<td>N/D
</td>
<td>Não disponível
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
<td>Não disponível
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
Definir eVar ou variável dos dados de contexto na chamada de link
</td>
<td>
<pre>
s.contextData['video.player']
  = ”CustomPlayer Name”;
</pre>
</td>
</tr>
<tr>
<td>
Media.trackSeconds
</td>
<td>
<pre>
s.Media.trackSeconds = 15
</pre>
</td>
<td>N/D
</td>
<td>Não disponível
</td>
</tr>
<tr>
<td>
Media.trackMilestones
</td>
<td>
<pre>
s.Media.trackMilestones = "25,50,75";
</pre>
</td>
<td>N/D
</td>
<td>Não disponível
</td>
</tr>
<tr>
<td>
Media.trackOffsetMilestones
</td>
<td>
<pre>
s.Media.trackOffsetMilestones 
  = "20,40,60";
</pre>
</td>
<td>N/D
</td>
<td>Não disponível
</td>
</tr>
<tr>
<td>
Media.segmentByMilestones
</td>
<td>
<pre>
s.Media.segmentByMilestones
  = true;
</pre>
</td>
<td>N/D
</td>
<td>Não disponível
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
<td>Não disponível
</td>
</tr>
</tbody>
</table>

### Variáveis de rastreamento de anúncios

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Sintaxe do Milestone
</th>
<th>Link personalizado
</th>
<th>Link personalizado Sintaxe
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
s.Media.adTrackSeconds = 15 
</pre>
</td>
<td>N/D
</td>
<td>Não disponível
</td>
</tr>
<tr>
<td>
Media.adTrackMilestones
</td>
<td>
<pre>
s.Media.adTrackMilestones = "25,50,75";
</pre>
</td>
<td>N/D
</td>
<td>Não disponível
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
<td>Não disponível
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
<td>Não disponível
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
<td>Não disponível
</td>
</tr>
</tbody>
</table>

### Métodos do módulo de mídia

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Sintaxe do Milestone
</th>
<th>Link personalizado
</th>
<th>Link personalizado Sintaxe
</th>
</tr>
</thead>
<tbody>
<tr>
<td>Media.open</td>
<td>
<pre>
s.Media.open(mediaName,mediaLength,mediaPlayerName)
</pre>
</td>
<td>s.tl()</td>
<td>
<pre>
s.linkTrackVars
  = 'events,
     prop10,
     eVar10,
     eVar12,
     eVar15,
     contextData.video.name,
     contextData.video.view';
s.linkTrackEvents 
  = 'event2';
s.prop10 
  = mediaName;
s.eVar10 
  = mediaName;
s.eVar12 
  = "video";
s.eVar15 
  = mediaPlayerName;
s.events 
  = 'event2';
s.contextData['video.name'] 
  = mediaName;
s.contextData['video.view'] 
  = 'true';
s.tl(this,'o','Video Start');
</pre>
</td>
</tr>
<tr>
<td>mediaName</td>
<td><b>mediaName:</b> (obrigatório) o nome do vídeo conforme você quer que ele seja exibido nos relatórios de vídeo.</td>
<td>Definir eVar ou variável dos dados de contexto na chamada de link</td>
<td>
<pre>
s.prop10 = mediaName;
s.eVar10 = mediaName;
s.contextData['video.name']
  = mediaName;
</pre>
</td>
</tr>
<tr>
<td>
mediaLength
</td>
<td>
<b>mediaLength:</b> (obrigatório) a duração do vídeo, em segundos.
</td>
<td>
Definir eVar ou variável dos dados de contexto na chamada de link
</td>
<td>
<pre>
s.contextData['video.length']
  = ”90”;
</pre>
</td>
</tr>
<tr>
<td>
mediaPlayerName
</td>
<td>
<b>mediaPlayerName:</b> (obrigatório) o nome do reprodutor de mídia utilizado para exibir o vídeo, conforme você quer que ele seja exibido nos relatórios de vídeo.
</td>
<td>
Definir eVar ou variável dos dados de contexto na chamada de link
</td>
<td>
<pre>
s.contextData['video.player']
  = ”CustomPlayer Name”;
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
<td>N/D
</td>
<td>Não disponível</td>
</tr>
<tr>
<td>name</td>
<td><b>name:</b> (obrigatório) o nome ou ID do anúncio.</td>
<td>N/D</td>
<td>Não disponível</td>
</tr>
<tr>
<td>
length
</td>
<td>
<b>length:</b> (obrigatório) a duração do anúncio.
</td>
<td>N/D
</td>
<td>Não disponível
</td>
</tr>
<tr>
<td>
playerName
</td>
<td>
<b>playerName:</b> (obrigatório) o nome do reprodutor de mídia utilizado para exibir o anúncio.
</td>
<td>N/D
</td>
<td>Não disponível
</td>
</tr>
<tr>
<td>
parentName
</td>
<td>
<b>parentName:</b> o nome ou a ID do conteúdo principal no qual o anúncio está incorporado.
</td>
<td>N/D
</td>
<td>Não disponível
</td>
</tr>
<tr>
<td>
parentPod
</td>
<td>
<b>parentPod:</b> a posição, no conteúdo principal, de reprodução do anúncio.
</td>
<td>N/D
</td>
<td>Não disponível
</td>
</tr>
<tr>
<td>
parentPodPosition
</td>
<td>
<b>parentPodPosition:</b> a posição, no pod, de reprodução do anúncio.
</td>
<td>N/D
</td>
<td>Não disponível
</td>
</tr>
<tr>
<td>
CPM
</td>
<td>
<b>CPM:</b> o CPM ou o CPM criptografado (com prefixo "~") que se aplica a essa reprodução.
</td>
<td>N/D
</td>
<td>Não disponível
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
<td>
<pre>
s.tl()
</pre>
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
<td>N/D
</td>
<td>Não disponível
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
s.tl()
</td>
<td>
<pre>
s.linkTrackVars
  = 'events,
     prop10,
     eVar10,
     eVar12,
     eVar15,
     contextData.
       video.name,
     contextData.
       video.complete';
s.linkTrackEvents 
  = 'event3';
s.prop10 
  = mediaName;
s.eVar10 
  = mediaName;
s.eVar12 
  = "video";
s.eVar15 
  = mediaPlayerName;
s.events 
  = 'event3';
s.contextData['video.name']
 =  mediaName;
s.contextData['video.complete']
 = 'true';
s.tl(this,'o','Video Complete');
</pre>
</td>
</tr>
<tr>
<td>
Media.play
</td>
<td>
<pre>
s.Media.play(name,offset,segmentNum,segment,segmentLength)
</pre>
</td>
<td>N/D
</td>
<td>Não disponível
</td>
</tr>
<tr>
<td>
Media.stop
</td>
<td>
<pre>
s.Media.stop(mediaName,mediaOffset)
</pre>
</td>
<td>N/D 
</td>
<td>Não disponível
</td>
</tr>
<tr>
<td>
Media.monitor
</td>
<td>
<pre>
s.Media.monitor(s, media)
</pre>
</td>
<td>
Definir eVar ou variável dos dados de contexto na chamada de link
</td>
<td>
<pre>
s.linkTrackVars
  = 'events,
     prop10,
     eVar10,
     eVar12,
     eVar15,
     contextData.
       video.name,
     contextData.
       video.view';
s.linkTrackEvents = 'event2';
</pre>
</td>
</tr>
<tr>
<td>
Media.track
</td>
<td>
<pre>
s.Media.track(mediaName)
</pre>
</td>
<td>N/D
</td>
<td>Não disponível
</td>
</tr>
</tbody>
</table>

