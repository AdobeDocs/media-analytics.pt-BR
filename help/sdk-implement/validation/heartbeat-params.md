---
seo-title: Descrições do parâmetro Heartbeat
title: Descrições do parâmetro Heartbeat
uuid: e 9 ddda 32-0952-43 d 0-a 702-49 f 5 b 1 bfd 8 cf
translation-type: tm+mt
source-git-commit: 6e13e9a6250949a3a7f059445da772b4db1fdb71

---


# Descrições do parâmetro Heartbeat{#heartbeat-parameter-descriptions}

Lista de parâmetros de pulsação que a Adobe coleta e processa no servidor Heartbeats:

## Todos os eventos

| Nome | Obrigatório/Opcional | Fonte de dados | Descrição  |
| ---  | :---: | --- | --- |
| `s:event:type` | Obr. | SDK do Media | O tipo de evento que está sendo rastreado. Tipos de evento: <ul> <li> `s:event:type=start` </li> <li> `s:event:type=complete` </li> <li> `s:event:type=chapter_start` </li> <li> `s:event:type=chapter_complete` </li> <li> `s:event:type=buffer` </li> <li> `s:event:type=pause` </li> <li> `s:event:type=resume` </li> <li> `s:event:type=bitrate_change` </li> <li> `s:event:type=aa_start` </li> <li> `s:event:type=stall` </li> <li> `s:event:type=end` </li> </ul> |
| `l:event:prev_ts` | Obr. | SDK do Media | O carimbo de data e hora do último evento deste tipo nesta sessão. The value is `-1` |
| `l:event:ts` | Obr. | SDK do Media | O carimbo de data e hora do evento. |
| `l:event:duration` | Obr. | SDK do Media | Esse valor é definido internamente (em milissegundos) pela Biblioteca do VHL, e não pelo reprodutor. É usado para calcular as métricas de tempo gasto no backend. For example `a.media.totalTimePlayed` `type=play` Note:  For some of the HB that are sent This parameter is set to 0 for certain events because they are "state change events" (e.g., `type=complete` `type=chapter_complete` `type=bitrate_change` |
| `l:event:playhead` | Obr. | `VideoInfo` | O indicador de reprodução estava dentro do ativo (principal ou anúncio) em operação no momento em que o evento foi gravado. |
| `s:event:sid` | Obr. | SDK do Media | A ID da sessão (uma sequência de caracteres gerada aleatoriamente). Todos os eventos de uma sessão específica (vídeo + anúncios) devem ser idênticos. |
| `l:asset:duration / l:asset:length` (Renomeado de `length``duration` | Obr. | `VideoInfo` | O comprimento do ativo de vídeo do ativo principal. |
| `s:asset:publisher` | Obr. | `MediaHeartbeatConfig` | O editor do ativo. |
| `s:asset:video_id` | Obr. | `VideoInfo` | Uma ID que identifica exclusivamente o vídeo no catálogo do editor. |
| `s:asset:type` | Obr. | SDK do Media | O tipo de ativo (principal ou anúncio). |
| `s:stream:type` | Obr. | `VideoInfo` | O tipo de fluxo. Pode ser um dos seguintes: <ul> <li> `live` </li> <li> `vod` </li> <li> `linear` </li> </ul>. |
| `s:user:id` | Op. | Objeto de configuração para VisitorID de medição de aplicativo móvel | ID de visitante especificamente definida pelo usuário. |
| `s:user:aid` | Op. | Org. da Experience Cloud | O valor da ID de visitante do Analytics do usuário. |
| `s:user:mid` | Obr. | Org. da Experience Cloud | O valor da ID de visitante da Experience Cloud do usuário. |
| `s:cuser:customer_user_ids_x` | Op. | `MediaHeartbeatConfig` | Todas as IDs de usuário cliente definidas no Audience Manager. |
| `l:aam:loc_hint` | Obr. | `MediaHeartbeatConfig` | AAM data sent on each payload after `aa_start` |
| `s:aam:blob` | Obr. | `MediaHeartbeatConfig` | AAM data sent on each payload after `aa_start` |
| `s:sc:rsid` | Obr. | ID (ou IDs) do conjunto de relatórios | RSID do SiteCatalyst, para onde os relatórios devem ser enviados. |
| `s:sc:tracking_server` | Obr. | `MediaHeartbeatConfig` | Servidor de rastreamento do SiteCatalyst. |
| `h:sc:ssl` | Obr. | `MediaHeartbeatConfig` | Se o tráfego será por HTTPS (caso esteja definido como 1) ou por HTTP (definido como 0). |
| `s:sp:ovp` | Op. | `MediaHeartbeatConfig` | Definido como "primetime" para reprodutores Primetime ou OVP real para outros reprodutores. |
| `s:sp:sdk` | Obr. | `MediaHeartbeatConfig` | A sequência de caracteres da versão de OVP. |
| `s:sp:player_name` | Obr. | `VideoInfo` | Nome do reprodutor de vídeo (o software do reprodutor real; usado para identificá-lo). |
| `s:sp:channel` | Op. | `MediaHeartbeatConfig` | O canal no qual o usuário está assistindo o conteúdo. Para um aplicativo de dispositivo móvel, o nome do aplicativo. Para um site, o nome do domínio. |
| `s:sp:hb_version` | Obr. | SDK do Media | O número da versão da biblioteca do VideoHeartbeat responsável por emitir a chamada. |
| `l:stream:bitrate` | Obr. | `QoSInfo` | O valor atual da taxa de bits do fluxo (em bps). |

## Eventos de erro

| Nome | Obrigatório/Opcional | Fonte de dados | Descrição  |
| ---  | :---: | --- | --- |
| `s:event:source` | Obr. | SDK do Media | A origem do erro, seja ela interna do reprodutor ou no nível do aplicativo. |
| `s:event:id` | Obr. | SDK do Media | ID do erro, identifica o erro exclusivamente. |

## Eventos de anúncios

| Nome | Obrigatório/Opcional | Fonte de dados | Descrição  |
| ---  | :---: | --- | --- |
| `s:asset:ad_id` | Obr. | `AdInfo` | O nome do anúncio. |
| `s:asset:ad_sid` | Obr. | SDK do Media | Um identificador exclusivo gerado pelo SDK do Media, anexado a todos os pings relacionados a anúncios. |
| `s:asset:pod_id` | Obr. | SDK do Media | ID do pod dentro do vídeo. Esse valor é calculado automaticamente com base na seguinte fórmula: `MD5(video_id) + "_" + [pod index]` |
| `s:asset:pod_position` | Obr. | `AdBreakInfo` | Índice do anúncio dentro do pod (o índice do primeiro anúncio é 0, do segundo é 1 etc.). |
| `s:asset:resolver` | Obr. | `AdBreakInfo` | O resolvedor de anúncios. |
| `s:meta:custom_ad_metadata.x` | Op. | `MediaHeartbeat` | Os metadados de anúncios personalizados. |

## Eventos de capítulo

| Nome | Obrigatório/Opcional | Fonte de dados | Descrição  |
| ---  | :---: | --- | --- |
| `s:stream:chapter_sid` | Obr. | SDK do Media | O identificador exclusivo associado à ocorrência de reprodução do capítulo.  Observação: um capítulo pode ser reproduzido várias vezes devido às operações de retorno executadas pelo usuário. |
| `s:stream:chapter_name` | Op. | `ChapterInfo` | O nome amigável do capítulo (ou seja, em formato legível por humanos). |
| `s:stream:chapter_id` | Obr. | SDK do Media | A ID exclusiva do capítulo. Esse valor é calculado automaticamente com base na seguinte fórmula: `MD5(video_id) + "_" + chapter_pos` |
| `l:stream:chapter_pos` | Obr. | `ChapterInfo` | O índice do capítulo na lista de capítulos (começando em 1). |
| `l:stream:chapter_offset` | Obr. | `ChapterInfo` | O deslocamento do capítulo (expresso em segundos) dentro do conteúdo principal, excluindo anúncios. |
| `l:stream:chapter_length` | Obr. | `ChapterInfo` | A duração do capítulo (expresso em segundos). |
| `s:meta:custom_chapter_metadata.x` | Op. | `ChapterInfo` | Metadados de capítulo personalizados. |

## Evento de fim de sessão

| Nome | Obrigatório/Opcional | Fonte de dados | Descrição  |
| ---  | :---: | --- | --- |
| `s:event:type=end` | Obr. | SDK do Media | A `end` `close` |

