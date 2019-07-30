---
seo-title: Migração do Marco para o Media Analytics
title: Migração do Marco para o Media Analytics
uuid: fdc 96146-af 63-48 ce-b 938-c 0 ca 70729277
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Migração do Marco para o Media Analytics {#migrating-from-milestone-to-media-analytics}

## Visão geral {#section_ihl_nbz_cfb}

Os principais conceitos de medição de vídeo são os mesmos para Marco e Media Analytics, que estão realizando eventos do reprodutor de vídeo e mapeando-os para os métodos de análise, além de capturar metadados e valores do reprodutor e mapeá-los para variáveis&#x200B;de análise. A solução do Media Analytics surgiu no Marco, portanto, muitos dos métodos e métricas são os mesmos. No entanto, a abordagem e o código de configuração mudaram significativamente. Deve ser possível atualizar o código de evento do reprodutor para apontar para os novos métodos do Media Analytics. See [SDK Overview](/help/sdk-implement/setup/setup-overview.md) and [Tracking Overview](/help/sdk-implement/track-av-playback/track-core-overview.md) for more details on implementing Media Analytics.

As tabelas a seguir fornecem as traduções entre as soluções de Marco e do Media Analytics.

## Guia de migração {#section_iyb_pbz_cfb}

### Referência da variável

| Métrica de marco | Tipo de variável | Métrica do Media Analytics |
| --- | --- | --- |
| Conteúdo | eVar<br/><br/>Default expiration: Visit | Conteúdo |
| Tipo de conteúdo | eVar<br/><br/> Expiração padrão: visualização de página | Tipo de conteúdo |
| Tempo gasto no conteúdo | Evento<br/><br/> Tipo: contador | Tempo gasto no conteúdo |
| Inicialização de vídeo | Evento<br/><br/> Tipo: contador | Inicialização de vídeo |
| Término do vídeo | Evento<br/><br/> Tipo: contador | Conteúdo concluído |

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
<td>N/A
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
<td>Os dados de contexto do Media Analytics são preenchidos automaticamente em variáveis reservadas. O mapeamento para eVars, as propriedades e os eventos que não são mais necessários no código de implementação. Os clientes podem mapear dados de contexto para variáveis usando regras de processamento.
</td>
</tr>
<tr>
<td>
Media.trackVars
</td>
<td>
<pre>
s. Media. trackvars = 
 " events,
 prop 2,
 evar 1,
 evar 2,
 evar 3 ";
</pre>
</td>
<td>N/A
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
s. Media. trackevents = 
 " event 1,
 event 2,
 event 3,
 event 4,
 event 5,
 event 6,
 event 7 "
</pre>
</td>
<td>N/A
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
<td>N/A
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
  Autotracknetstreams
 = true
</pre>
</td>
<td>N/A
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
  Completebycloseoffset
 = true
</pre>
</td>
<td>N/A
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
  Completecloseoffsetthreshold
 = 1
</pre>
</td>
<td>N/A
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
Chave do SDK: Playername; 
Chave da API: media. playername
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
  Trackseconds
 = 15
</pre>
</td>
<td>N/A
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
  Trackmilestones
 = "25,50,75";
</pre>
</td>
<td>N/A
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
  Trackoffsetmilestones
 = "20,40,60";
</pre>
</td>
<td>N/A
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
<td>N/A
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
  Segmentbyoffsetmilestones
 = true;
</pre>
</td>
<td>N/A
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
  Adtrackseconds
 = 15
</pre>
</td>
<td>N/A
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
  Adtrackmilestones
 = "25,50,75";
</pre>
</td>
<td>N/A
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
  Adtrackoffsetmilestones
 = "20,40,60";
</pre>
</td>
<td>N/A
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
  Adsegmentbymilestones
 = true;
</pre>
</td>
<td>N/A
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
  Adsegmentbyoffsetmilestones
 = true;
</pre>
</td>
<td>N/A
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
Tracksessionstart (mediaobject, 
 Contextdata)
</pre>
</td>
</tr>
<tr>
<td>
Medianame - (obrigatório) o nome do vídeo como
você deseja que seja exibido nos relatórios de vídeo.
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
Createmediaobject (nome, 
 Mediaid, 
 length, 
 Streamtype)
</pre>
</td>
</tr>
<tr>
<td>
Medialength - (obrigatório) a duração do vídeo
em segundos.
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
Createmediaobject (nome, 
 Mediaid, 
 length, 
 Streamtype)
</pre>
</td>
</tr>
<tr>
<td>
Mediaplayername - (obrigatório) o nome do player de mídia usado para exibir o vídeo, 
como você quer que ele seja exibido nos relatórios de vídeo.
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
Mediaheartbeat. trackevent (mediaheartbeat.
 Evento.
    Adbreakstart, 
 Adbreakobject);
…
Trackevent (mediaheartbeat.
 Evento.
    Adstart, 
 Adobject, 
 Adcustommetadata);
</pre>
</td>
</tr>
<tr>
<td>
name - (obrigatório) o nome ou ID do anúncio.
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
Createadobject (nome, 
 Adid, 
 position, 
 length)
</pre>
</td>
</tr>
<tr>
<td>
length
(obrigatório) O comprimento do anúncio.
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
Createadobject (nome, 
 Adid, 
 position, 
 length)
</pre>
</td>
</tr>
<tr>
<td>
Playername - (obrigatório) o nome do player de mídia
usado para exibir o anúncio.
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
Parentname - o nome ou ID do conteúdo principal no qual o anúncio está incorporado.
</td>
<td>
<pre>
parentName
</pre>
</td>
<td>N/A
</td>
<td>Herdado automaticamente
</td>
</tr>
<tr>
<td>
Parentpod - a posição no conteúdo principal que o anúncio foi reproduzido.
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
Createadbreakobject (nome, 
 position, 
 Starttime)
</pre>
</td>
</tr>
<tr>
<td>
Parentpodposition - a posição no pod em que o anúncio é reproduzido.
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
Createadobject (nome, 
 Adid, 
 position, 
 length)
</pre>
</td>
</tr>
<tr>
<td>
CPM
O CPM ou CPM criptografado (com prefixo «~») que se aplica a essa reprodução.
</td>
<td>
<pre>
CPM
</pre>
</td>
<td>N/A
</td>
<td>Não disponível por padrão no Media Analytics
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
<td>N/A
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
Trackevent (mediaheartbeat.
 Evento.
  SeekStart)
</pre> ou
<pre>
Trackevent (mediaheartbeat.
 Evento.
  bufferStart);
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
var customvideometadata = 
{isuserloggedin: 
 " false ",
 tvstation: 
 " Amostra de estação de TV ",
 programador: 
 " Exemplo de programador "};
…
var standardvideometadata 
 = {};
Standardvideometadata
 [mediaheartbeat.
 VideoMetadataKeys.
   EPISODE] = 
 " Amostra de episódio ";
Standardvideometadata
 [mediaheartbeat.
 VideoMetadataKeys.
   SHOW] = "Exemplo de exibição";
…
Mediaobject. setvalue (mediaheartbeat.
 Mediaobjectkey.
 Standardvideometadata, 
 Standardvideometadata);
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
<td>N/A
</td>
<td>O rastreamento da frequência de chamada é automaticamente definido.
</td>
</tr>
</tbody>
</table>

