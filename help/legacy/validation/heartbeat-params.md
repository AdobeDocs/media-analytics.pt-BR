---
title: Descrições do parâmetro do Heartbeat
description: Uma lista de parâmetros de heartbeat que a Adobe coleta e processa no servidor do Media Analytics (heartbeats).
uuid: e9ddda32-0952-43d0-a702-49f5b1bfd8cf
exl-id: ffa67b5e-ee54-4a5b-8064-decd108f944b
feature: "Media Analytics, Variables"
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '810'
ht-degree: 100%

---

# Descrições dos parâmetros do Media Analytics (heartbeats) {#heartbeat-parameter-descriptions}

Lista de parâmetros do Media Analytics que a Adobe coleta e processa no servidor do Media Analytics (heartbeats):

## Todos os eventos

| Nome | Fonte de dados |  Descrição  |
| ---  | --- | --- |
| s:event:type | SDK de mídia | (Obrigatório)<br/><br/>O tipo de evento que está sendo rastreado. Tipos de evento: <ul> <li> s:event:type=start </li> <li> s:event:type=complete </li> <li> s:event:type=chapter_start </li> <li> s:event:type=chapter_complete </li> <li> s:event:type=buffer </li> <li> s:event:type=pause </li> <li> s:event:type=resume </li> <li> s:event:type=bitrate_change </li> <li> s:event:type=aa_start </li> <li> s:event:type=stall </li> <li> s:event:type=end </li> </ul> |
| l:event:prev_ts | SDK de mídia | (Obrigatório)<br/><br/>O carimbo de data e hora do último evento deste tipo nesta sessão. O valor é -1. |
| l:event:ts | SDK de mídia | (Obrigatório)<br/><br/>O carimbo de data e hora do evento. |
| l:event:duration | SDK de mídia | (Obrigatório)<br/><br/>Esse valor é definido internamente (em milissegundos) pelo SDK do Media, e não pelo reprodutor. É usado para calcular as métricas de tempo gasto no backend. Por exemplo: a.media.totalTimePlayed é calculado como uma soma da duração de todas os heartbeats de reprodução (type=play) gerados. <br/>*Observação:* Esse parâmetro é definido como 0 para determinados eventos, pois eles são &quot;eventos de alteração de estado&quot; (por exemplo, type=complete, type=chapter_complete ou type=bitrate_change). |
| l:event:playhead | VideoInfo | (Obrigatório)<br/><br/>O indicador de reprodução estava dentro do ativo (principal ou anúncio) em operação no momento em que o evento foi gravado. |
| s:event:sid | SDK de mídia | (Obrigatório)<br/><br/>A ID da sessão (uma sequência de caracteres gerada aleatoriamente). Todos os eventos de uma sessão específica (vídeo + anúncios) devem ser idênticos. |
| l:asset:duration / l:asset:length <br/>(renomeado a partir da duração) | VideoInfo | (Obrigatório)<br/><br/>O comprimento do ativo de vídeo do ativo principal. |
| s:asset:publisher | MediaHeartbeatConfig | (Obrigatório)<br/><br/>O editor do ativo. |
| s:asset:video_id | VideoInfo | (Obrigatório)<br/><br/>Uma ID que identifica exclusivamente o vídeo no catálogo do editor. |
| s:asset:type | SDK de mídia | (Obrigatório)<br/><br/>O tipo de ativo (principal ou anúncio). |
| s:stream:type | VideoInfo | (Obrigatório)<br/><br/>O tipo de fluxo. Pode ser um dos seguintes: <ul> <li> live </li> <li> vod </li> <li> linear </li> </ul> |
| s:user:id | Objeto de configuração do VisitorID móvel do App Measurement | (Opcional)<br/><br/>ID de visitante especificamente definida pelo usuário. |
| s:user:aid | Org. da Experience Cloud | (Opcional)<br/><br/>O valor da ID de visitante do Analytics do usuário. |
| s:user:mid | Org. da Experience Cloud | (Obrigatório)<br/><br/>O valor da ID de visitante da Experience Cloud do usuário. |
| s:cuser:customer_user_ids_x | MediaHeartbeatConfig | (Opcional)<br/><br/>Todas as IDs de usuário cliente definidas no Audience Manager. |
| l:aam:loc_hint | MediaHeartbeatConfig | (Obrigatório)<br/><br/>Dados de AAM enviados em cada carga após aa_start |
| s:aam:blob | MediaHeartbeatConfig | (Obrigatório)<br/><br/>Dados de AAM enviados em cada carga após aa_start |
| s:sc:rsid | ID (ou IDs) do conjunto de relatórios | (Obrigatório)<br/><br/>RSID do Adobe Analytics para o qual os relatórios devem ser enviados. |
| s:sc:tracking_server | MediaHeartbeatConfig | (Obrigatório)<br/><br/>Servidor de rastreamento do Adobe Analytics. |
| h:sc:ssl | MediaHeartbeatConfig | (Obrigatório)<br/><br/>Se o tráfego será por HTTPS (caso esteja definido como 1) ou por HTTP (definido como 0). |
| s:sp:ovp | MediaHeartbeatConfig | (Opcional)<br/><br/>Definido como &quot;primetime&quot; para reprodutores do Primetime ou OVP real para outros reprodutores. |
| s:sp:sdk | MediaHeartbeatConfig | (Obrigatório)<br/><br/>A sequência de caracteres da versão de OVP. |
| s:sp:player_name | VideoInfo | (Obrigatório)<br/><br/>Nome do reprodutor de vídeo (o software do reprodutor real, usado para identificá-lo). |
| s:sp:channel | MediaHeartbeatConfig | (Opcional)<br/><br/>O canal no qual o usuário está assistindo ao conteúdo. Para um aplicativo móvel, o nome do aplicativo. Para um site, o nome do domínio. |
| s:sp:hb_version | SDK de mídia | (Obrigatório)<br/><br/>O número da versão da biblioteca do SDK do Media que emitiu a chamada. |
| l:stream:bitrate | QoSInfo | (Obrigatório)<br/><br/>O valor atual da taxa de bits do fluxo (em bps). |

## Eventos de erro

| Nome | Fonte de dados | Descrição   |
| ---  | --- | --- |
| s:event:source | SDK de mídia | (Obrigatório)<br/><br/>A origem do erro, seja ela interna do reprodutor ou no nível do aplicativo. |
| s:event:id | SDK de mídia | (Obrigatório)<br/><br/>ID do erro, identifica o erro exclusivamente. |

## Eventos de anúncios

| Nome | Fonte de dados | Descrição   |
| ---  | --- | --- |
| s:asset:ad_id | AdInfo | (Obrigatório)<br/><br/>O nome do anúncio. |
| s:asset:ad_sid | SDK de mídia | (Obrigatório)<br/><br/>Um identificador exclusivo gerado pelo SDK do Media, anexado a todos os pings relacionados a anúncios. |
| s:asset:pod_id | SDK de mídia | (Obrigatório)<br/><br/>ID do pod dentro do vídeo. Esse valor é calculado automaticamente com base na seguinte fórmula: <br/>`MD5(video_id) + `<br/>`"_" + `<br/>`[pod index]` |
| s:asset:pod_position | AdBreakInfo | (Obrigatório)<br/><br/>Índice do anúncio dentro do pod (o índice do primeiro anúncio é 0, do segundo é 1, etc.). |
| s:asset:resolver | AdBreakInfo | (Obrigatório)<br/><br/>O resolvedor de anúncios. |
| s:meta:custom_ad_metadata.x | MediaHeartbeat | (Opcional)<br/><br/>Os metadados de anúncios personalizados. |

## Eventos de capítulo

| Nome | Fonte de dados | Descrição   |
| ---  | --- | --- |
| s:stream:chapter_sid | SDK de mídia | (Obrigatório)<br/><br/>O identificador exclusivo associado à ocorrência de reprodução do capítulo.  <br/> **Observação:** um capítulo pode ser reproduzido várias vezes devido às operações de retorno executadas pelo usuário. |
| s:stream:chapter_name | ChapterInfo | (Opcional)<br/><br/>O nome amigável do capítulo (ou seja, em formato legível). |
| s:stream:chapter_id | SDK de mídia | (Obrigatório)<br/><br/>A ID exclusiva do capítulo. Esse valor é calculado automaticamente com base na seguinte fórmula: <br/>`MD5(video_id) +`<br/>` "_" +`<br/>`chapter_pos` |
| l:stream:chapter_pos | ChapterInfo | (Obrigatório)<br/><br/>O índice do capítulo na lista de capítulos (começando em 1). |
| l:stream:chapter_offset | ChapterInfo | (Obrigatório)<br/><br/>O deslocamento do capítulo (expresso em segundos) dentro do conteúdo principal, excluindo anúncios. |
| l:stream:chapter_length | ChapterInfo | (Obrigatório)<br/><br/>A duração do capítulo (expresso em segundos). |
| s:meta:custom_chapter_metadata.x | ChapterInfo | (Opcional)<br/><br/>Metadados de capítulo personalizados. |

## Evento de fim de sessão

| Nome | Fonte de dados | Descrição   |
| ---  | --- | --- |
| s:event:type=end | SDK de mídia | (Obrigatório)<br/><br/> A `end` `close` |
