---
seo-title: Migração do Marco para Link personalizado
title: Migração do Marco para Link personalizado
uuid: 1 c 8 edde 5-0 ef 1-4 bc 0-a 62 d -1747 f 4907 f 09
translation-type: tm+mt
source-git-commit: 530973abc12fcb2567a3742c202d992944048b8b

---


# Migração do Marco para Link personalizado{#migrating-from-milestone-to-custom-link}

## Visão geral {#section_xlc_fc2_dfb}

Os principais conceitos de medição de vídeo são os mesmos para o rastreamento de Marco e Link personalizado, que estão realizando eventos do reprodutor de vídeo e mapeando-os para métodos de análise, além de capturar metadados e valores de reprodutores e mapeá-los para variáveis&#x200B;de análise. A abordagem de Link personalizado deve ser considerada como uma diminuição e simplificação da implementação e dos dados coletados. Com a solução de Link personalizado, nenhuma variável ou método é predefinido para a medição de vídeo, isso requer uma configuração personalizada completa. Deve ser possível atualizar o código de evento do reprodutor para apontar as chamadas de rastreamento de link personalizado para eventos básicos do reprodutor, como início e conclusão. Consulte o [guia de implementação do Link personalizado](../../measurement-options/cl-in-aa/cl-impl-guide.md) e o [Rastreamento de link manual usando um código de link personalizado](https://marketing.adobe.com/resources/help/en_US/sc/implement/link_manual.html) para obter mais detalhes.

As tabelas a seguir fornecem as traduções entre as soluções de Marco e Link personalizado.

## Guia de migração {#section_btt_fc2_dfb}

### Referência da variável de vídeo

<table>
<thead>
<tr>
<th><strong>Métrica de marco</strong></th>
<th><strong>Tipo de variável</strong></th>
<th><strong>Link Personalizado</strong></th>
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
<td>Término do vídeo</td>
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
<th>Etapa
</th>
<th>Sintaxe do marco
</th>
<th>Link personalizado
</th>
<th>Link personalizado  Sintaxe
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
  Trackusingcontextdata 
 = true;
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s. linktrackvars
 =' events, 
contextdata. video. name '; 
s. contextdata [' video. name ']
 = medianame;
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
  Contextdatamapping = {"a. media. name":
 " Evar 2, prop 2 ","
 a. media. segment ":
 " Evar 3 ","
 a. contenttype ":
 " Evar 1 ","
 a. media. timeplayed ":
 " event 3 ","
 a. media. view ":
 " event 1 ","
 a. media. segmentview ":
 " event 2 ","
 a. media. complete ":
 " event 7 ","
 a. media. milestones ": {25: " event 4 ",
 50: " event 5 ",
 75: " event 6 "}};
</pre>
</td>
<td>N/A
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
s. Media. trackvars
 = "events,
 prop 2,
 evar 1,
 evar 2,
 evar 3";
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s. linktrackvars
 =' events,
 prop 10,
 evar 10,
 evar 12,
 evar 13,
 evar 15,
 contextdata.
 video. name,
 contextdata.
 video. view ';
</pre>
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s. Media. trackevents
 = "event 1,
 event 2,
 event 3,
 event 4,
 event 5,
 event 6,
 event 7"
</pre>
</td>
<td>
linkTrackEvents
</td>
<td>
<pre>
s. linktrackevents
 =' event 2 ';
</pre>
</td>
</tr>
</tbody>
</table>

<table>
<thead>
<tr>
<th>Etapa
</th>
<th>Sintaxe do marco
</th>
<th>Link personalizado
</th>
<th>Link personalizado  Sintaxe
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
  Trackusingcontextdata 
 = true;
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s. linktrackvars
 =' events, 
contextdata. video. name '; 
s. contextdata [' video. name ']
 = medianame;
</pre>
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
</td>
<td>
<pre>
s. Media. contextdatamapping = {"a. media. name": " Evar 2, prop 2 ","
 a. media. segment ": " Evar 3 ","
 a. contenttype ": " Evar 1 ","
 a. media. timeplayed ": " event 3 ","
 a. media. view ": " event 1 ","
 a. media. segmentview ": " event 2 ","
 a. media. complete ": " event 7 ","
 a. media. milestones ": {25: " event 4 ",
 50: " event 5 ",
 75: " event 6 "}};
</pre>
</td>
<td>N/A
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
s. Media. trackvars
 = "events,
 prop 2,
 evar 1,
 evar 2,
 evar 3";
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s. linktrackvars
 =' events,
 prop 10,
 evar 10,
 evar 12,
 evar 13,
 evar 15,
 contextdata.
 video. name,
 contextdata.
 video. view ';
</pre>
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s. Media. trackevents
 = "event 1,
 event 2,
 event 3,
 event 4,
 event 5,
 event 6,
 event 7"
</pre>
</td>
<td>
linkTrackEvents
</td>
<td>
<pre>
s. linktrackevents
 =' event 2 ';
</pre>
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
<th>Link personalizado
</th>
<th>Link personalizado  Sintaxe
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
<td>N/A
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
<td>N/A
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
<td>N/A
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
  Completecloseoffsetthreshold
 = 1
</pre>
</td>
<td>N/A
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
s. contextdata [' video. player ']
 =» Nome do customplayer»;
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
<td>N/A
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
<td>N/A
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
s.Media.trackOffsetMilestones = "20,40,60";
</pre>
</td>
<td>N/A
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
s.Media.segmentByMilestones = true;
</pre>
</td>
<td>N/A
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
  Segmentbyoffsetmilestones
 = true;
</pre>
</td>
<td>N/A
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
<th>Etapa
</th>
<th>Sintaxe do marco
</th>
<th>Link personalizado
</th>
<th>Link personalizado  Sintaxe
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
<td>N/A
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
<td>N/A
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
  Adtrackoffsetmilestones 
 = "20,40,60";
</pre>
</td>
<td>N/A
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
  Adsegmentbymilestones
 = true;
</pre>
</td>
<td>N/A
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
  Adsegmentbyoffsetmilestones
 = true;
</pre>
</td>
<td>N/A
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
<th>Etapa
</th>
<th>Sintaxe do marco
</th>
<th>Link personalizado
</th>
<th>Link personalizado  Sintaxe
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
s. linktrackvars
 =' events,
 prop 10,
 evar 10,
 evar 12,
 contar 15,
 contextdata. video. name,
 contextdata. video. view ';
s. linktrackevents 
 =' event 2 ';
s. prop 10 
 = Medianame;
s. evar 10 
 = Medianame;
s. evar 12 
 = "video";
s. evar 15 
 = Mediaplayername;
s. events 
 =' event 2 ';
s. contextdata [' video. name '] 
 = Medianame;
s. contextdata [' video. view '] 
 =' true ';
s. tl (this,' o ',' Video Start ');
</pre>
</td>
</tr>
<tr>
<td>mediaName</td>
<td><b>Medianame:</b> (obrigatório) O nome do vídeo como você deseja que seja exibido nos relatórios de vídeo.</td>
<td>Definir eVar ou variável dos dados de contexto na chamada de link</td>
<td>
<pre>
s. prop 10 = medianame;
s. evar 10 = medianame;
s. contextdata [' video. name ']
 = medianame;
</pre>
</td>
</tr>
<tr>
<td>
mediaLength
</td>
<td>
<b>Medialength:</b> (obrigatório) O tamanho do vídeo em
segundos.
</td>
<td>
Definir eVar ou variável dos dados de contexto na chamada de link
</td>
<td>
<pre>
s. contextdata [' video. length ']
 =» 90»;
</pre>
</td>
</tr>
<tr>
<td>
mediaPlayerName
</td>
<td>
<b>Mediaplayername:</b> (obrigatório) O nome do player
de mídia usado para exibir o vídeo, conforme você deseja que ele seja exibido nos relatórios de vídeo.
</td>
<td>
Definir eVar ou variável dos dados de contexto na chamada de link
</td>
<td>
<pre>
s. contextdata [' video. player ']
 =» Nome do customplayer»;
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
<td>N/A
</td>
<td>Não disponível</td>
</tr>
<tr>
<td>name</td>
<td><b>name:</b> (obrigatório) O nome ou ID do anúncio.</td>
<td>N/A</td>
<td>Não disponível</td>
</tr>
<tr>
<td>
length
</td>
<td>
<b>length:</b> (obrigatório) O comprimento do anúncio.
</td>
<td>N/A
</td>
<td>Não disponível
</td>
</tr>
<tr>
<td>
playerName
</td>
<td>
<b>Playername:</b> (obrigatório) O nome do player de mídia usado
para exibir o anúncio.
</td>
<td>N/A
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
<td>N/A
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
<td>N/A
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
<td>N/A
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
<td>N/A
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
<td>N/A
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
s. linktrackvars
 =' events,
 prop 10,
 evar 10,
 evar 12,
 evar 15,
 contextdata.
 video. name,
 contextdata.
 video. complete ';
s. linktrackevents 
 =' event 3 ';
s. prop 10 
 = Medianame;
s. evar 10 
 = Medianame;
s. evar 12 
 = "video";
s. evar 15 
 = Mediaplayername;
s. events 
 =' event 3 ';
s. contextdata [' video. name ']
 = medianame;
s. contextdata [' video. complete ']
 =' true ';
s. tl (this,' o ',' Video Complete ');
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
<td>N/A
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
<td>N/A 
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
s. linktrackvars
 =' events,
 prop 10,
 evar 10,
 evar 12,
 evar 15,
 contextdata.
 video. name,
 contextdata.
 video. view ';
s. linktrackevents =' event 2 ';
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
<td>N/A
</td>
<td>Não disponível
</td>
</tr>
</tbody>
</table>

