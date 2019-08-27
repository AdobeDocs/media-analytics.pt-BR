---
seo-title: Descrições do parâmetro Heartbeat
title: Descrições do parâmetro Heartbeat
uuid: e 9 ddda 32-0952-43 d 0-a 702-49 f 5 b 1 bfd 8 cf
translation-type: tm+mt
source-git-commit: 10a5d921953339bef1cde2f802eb9ce0cb1bbe4b

---


# Descrições do parâmetro Media Analytics (heartbeats){#heartbeat-parameter-descriptions}

Lista de parâmetros do Media Analytics que a Adobe coleta e processa no servidor Media Analytics (heartbeats):

## Todos os eventos

| Nome | Fonte de Dados |  Descrição  |
| ---  | --- | --- |
| s:event:type | SDK do Media | (Required)<br/><br/>The type of the event being tracked. Tipos de evento: <ul> <li> s:event:type=start </li> <li> s:event:type=complete </li> <li> s:event:type=chapter_start </li> <li> s:event:type=chapter_complete </li> <li> s:event:type=buffer </li> <li> s:event:type=pause </li> <li> s:event:type=resume </li> <li> s:event:type=bitrate_change </li> <li> s:event:type=aa_start </li> <li> s:event:type=stall </li> <li> s:event:type=end </li> </ul> |
| l:event:prev_ts | SDK do Media | (Required)<br/><br/>The timestamp of the last event of the same type in this session. O valor é -1. |
| l:event:ts | SDK do Media | (Required)<br/><br/>The timestamp of the event. |
| l:event:duration | SDK do Media | (Required)<br/><br/>This value is set internally (in milliseconds) by the Media SDK, not by the player. É usado para calcular as métricas de tempo gasto no backend. Por exemplo: a. media. totaltimeplayed é calculada como uma soma da duração de todas as pulsações de Play (type = play) que são geradas. <br/>*Observação:* Esse parâmetro é definido como 0 para determinados eventos, pois eles são "eventos de alteração de estado" (por exemplo, type = complete, type = chapter_ complete ou type = bitrate_ change.) |
| l:event:playhead | Videoinfo | (Required)<br/><br/>The playhead was inside the currently active asset (main or ad), when the event was recorded. |
| s:event:sid | SDK do Media | (Required)<br/><br/>The session ID (a randomly generated string). Todos os eventos de uma sessão específica (vídeo + anúncios) devem ser idênticos. |
| l: ativo: duração/l: ativo: length <br/>(Renomeado da duração do comprimento) | Videoinfo | (Required)<br/><br/>The video asset length of the main asset. |
| s:asset:publisher | MediaHeartbeatConfig | (Required)<br/><br/>The publisher of the asset. |
| s:asset:video_id | Videoinfo | (Required)<br/><br/>An ID uniquely identifying the video in the publisher's catalog. |
| s:asset:type | SDK do Media | (Required)<br/><br/>The asset type (main or ad). |
| s:stream:type | Videoinfo | (Obrigatório)<br/><br/>O tipo de fluxo. Pode ser um dos seguintes: <ul> <li> live </li> <li> vod </li> <li> linear </li> </ul> |
| s:user:id | Objeto de configuração para VisitorID de medição de aplicativo móvel | (Optional)<br/><br/>User's specifically set Visitor ID. |
| s:user:aid | Org. da Experience Cloud | (Optional)<br/><br/>The user's Analytics Visitor ID value. |
| s:user:mid | Org. da Experience Cloud | (Required)<br/><br/>The user's Experience cloud visitor ID value. |
| s:cuser:customer_user_ids_x | MediaHeartbeatConfig | (Optional)<br/><br/>All customer user IDs set on Audience Manager. |
| l:aam:loc_hint | MediaHeartbeatConfig | (Required)<br/><br/>AAM data sent on each payload after aa_start |
| s:aam:blob | MediaHeartbeatConfig | (Required)<br/><br/>AAM data sent on each payload after aa_start |
| s:sc:rsid | ID (ou IDs) do conjunto de relatórios | (Obrigatório)<br/><br/>RSID do Adobe Analytics em que os relatórios devem ser enviados. |
| s:sc:tracking_server | MediaHeartbeatConfig | (Obrigatório)<br/><br/>Servidor de rastreamento do Adobe Analytics. |
| h:sc:ssl | MediaHeartbeatConfig | (Required)<br/><br/>Whether the traffic is over HTTPS (if set to 1) or over HTTP (is set to 0). |
| s:sp:ovp | MediaHeartbeatConfig | (Optional)<br/><br/>Set to "primetime" for Primetime players, or the actual OVP for other players. |
| s:sp:sdk | MediaHeartbeatConfig | (Required)<br/><br/>The OVP version string. |
| s:sp:player_name | Videoinfo | (Required)<br/><br/>Video player name (the actual player software, used to identify the player). |
| s:sp:channel | MediaHeartbeatConfig | (Optional)<br/><br/>The channel where the user is watching the content. Para um aplicativo de dispositivo móvel, o nome do aplicativo. Para um site, o nome do domínio. |
| s:sp:hb_version | SDK do Media | (Obrigatório)<br/><br/>O número da versão da biblioteca do SDK de mídia que emitiu a chamada. |
| l:stream:bitrate | Qosinfo | (Required)<br/><br/>The current value of the stream bitrate (in bps). |

## Eventos de erro

| Nome | Fonte de Dados | Descrição   |
| ---  | --- | --- |
| s:event:source | SDK do Media | (Required)<br/><br/>The source of the error, either player-internal, or the application-level. |
| s:event:id | SDK do Media | (Required)<br/><br/>Error ID, uniquely identifies the error. |

## Eventos de anúncios

| Nome | Fonte de Dados | Descrição   |
| ---  | --- | --- |
| s:asset:ad_id | Adinfo | (Obrigatório)<br/><br/>O nome do anúncio. |
| s:asset:ad_sid | SDK do Media | (Required)<br/><br/>A unique identifier generated by the Media SDK, appended to all ad-related pings. |
| s:asset:pod_id | SDK do Media | (Required)<br/><br/>Pod ID inside the video. Esse valor é calculado automaticamente com base na seguinte fórmula: <br/>`MD5(video_id) + `<br/>`"_" + `<br/>`[pod index]` |
| s:asset:pod_position | Adbreakinfo | (Required)<br/><br/>Index of the ad inside the pod (the first ad has index 0, the second ad has index 1, etc.). |
| s:asset:resolver | Adbreakinfo | (Obrigatório)<br/><br/>O resolver do anúncio. |
| s:meta:custom_ad_metadata.x | MediaHeartbeat | (Optional)<br/><br/>The custom ad metadata. |

## Eventos de capítulo

| Nome | Fonte de Dados | Descrição   |
| ---  | --- | --- |
| s:stream:chapter_sid | SDK do Media | (Required)<br/><br/>The unique identifier associated to the playback instance of the chapter.  <br/> **Observação:** um capítulo pode ser reproduzido várias vezes devido às operações de retorno executadas pelo usuário. |
| s:stream:chapter_name | Chapterinfo | (Optional)<br/><br/>The chapter's friendly (i.e., human readable) name. |
| s:stream:chapter_id | SDK do Media | (Required)<br/><br/>The unique ID of the chapter. Esse valor é calculado automaticamente com base na seguinte fórmula: <br/>`MD5(video_id) +`<br/>` "_" +`<br/>`chapter_pos` |
| l:stream:chapter_pos | Chapterinfo | (Required)<br/><br/>The chapter's index in the list of chapters (starting with 1). |
| l:stream:chapter_offset | Chapterinfo | (Required)<br/><br/>The chapter's offset (expressed in seconds) inside the main content, excluding ads. |
| l:stream:chapter_length | Chapterinfo | (Required)<br/><br/>The chapter's duration (expressed in seconds). |
| s:meta:custom_chapter_metadata.x | Chapterinfo | (Opcional)<br/><br/>Metadados de capítulo personalizados. |

## Evento de fim de sessão

| Nome | Fonte de Dados | Descrição   |
| ---  | --- | --- |
| s:event:type=end | SDK do Media | (Obrigatório)<br/><br/> A variável `end``close` |

