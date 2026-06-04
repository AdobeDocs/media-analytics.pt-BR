---
title: Mapeamento de parâmetros do Media Analytics para Adobe Experience Platform e Customer Journey Analytics
description: Mapeamento de caminho de campo XDM para parâmetros do Media Analytics usados com o Analytics Source Connector e o Customer Journey Analytics.
feature: Streaming Media
role: User, Admin, Developer
exl-id: 79203a2f-8158-44f2-83b2-146179be9180
TQID: https://experienceleague.adobe.com/ct8mDbIpg15Jzvf1MRaG4XFtuxbq-EUKPe106zyO7zQ
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: 1331
ht-degree: 19%

---

# Mapeamento de parâmetros do Media Analytics para Adobe Experience Platform e Customer Journey Analytics

Este documento fornece uma lista abrangente de todos os parâmetros do Media Analytics utilizados no Adobe Experience Platform e no Customer Journey Analytics. Ele tem como objetivo oferecer suporte à integração de dados importados do Adobe Analytics com a Platform por meio do [Conector Source do Analytics](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sources/connectors/adobe-applications/analytics) ou do [Conector Source do Analytics para Classificações](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sources/connectors/adobe-applications/classifications), mapeando cada parâmetro para o caminho do campo XDM correspondente.

>[!NOTE]
>
>Esta referência se aplica às organizações que usam o [conector de origem do Analytics](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sources/connectors/adobe-applications/analytics) para trazer dados de mídia de transmissão do Adobe Analytics para a Adobe Experience Platform para uso com relatórios do Customer Journey Analytics ou outros serviços da plataforma. Essas alterações não afetam o Adobe Analytics como um aplicativo independente, incluindo a coleta de dados, o processamento e os relatórios.

## Variáveis reservadas do Media Analytics

A partir de outubro de 2025, o caminho do campo XDM `media.mediaTimed` usado pelo conector de origem do Analytics foi totalmente descontinuado e substituído por `mediaReporting`. Os dados assimilados após outubro de 2025 incluem apenas `mediaReporting` campos. Os dados anteriores permanecem disponíveis no caminho do campo herdado, refletido nas tabelas abaixo em **Campo XDM herdado**.

### Comportamento de chamada keep-alive

Com o conector de origem do Analytics para mídia de transmissão, as chamadas keep-alive do Adobe Analytics agora são assimiladas no Adobe Experience Platform. Isso pode afetar os relatórios do Customer Journey Analytics:

* **Contagens de sessões**: chamadas keep-alive ajudam a manter sessões de usuários ativos mesmo sem interações diretas de mídia. Essas chamadas são geradas a cada 20 minutos após o último evento por reprodução de mídia. Para garantir o rastreamento ideal da sessão, configure a expiração da visita para 30 minutos na visualização de dados.

* **Contagens de eventos**: as chamadas keep-alive agora são contadas na métrica Eventos do Customer Journey Analytics. Para excluí-los, crie um filtro que exclua eventos com o Tipo de Evento `media.keepalive`.

## Parâmetros de streaming de mídia

| Nome do campo | Campo XDM herdado | Caminho do campo XDM do relatório | Tipo de dados | Campo derivado | Notas |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL Tipo de fluxo]](/help/reporting/dimensions/stream-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference.streamType` | `xdm.mediaReporting.`<br>`sessionDetails.streamType` | Dimensão | [[!UICONTROL Tipo de fluxo]](/help/reporting/dimensions/stream-type.md) | |
| [[!UICONTROL ID de conteúdo]](/help/reporting/dimensions/asset-id.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._id` | `xdm.mediaReporting.`<br>`sessionDetails.name` | Dimensão | [[!UICONTROL ID de conteúdo]](/help/reporting/dimensions/asset-id.md) | |
| [[!UICONTROL Duração do conteúdo]](/help/reporting/dimensions/content-length.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._xmpDM.duration` | `xdm.mediaReporting.`<br>`sessionDetails.length` | Dimensão | [[!UICONTROL Duração do conteúdo]](/help/reporting/dimensions/content-length.md) | |
| [[!UICONTROL Tipo de conteúdo]](/help/reporting/dimensions/content-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.broadcastContentType` | `xdm.mediaReporting.`<br>`sessionDetails.contentType` | Dimensão | [[!UICONTROL Tipo de conteúdo]](/help/reporting/dimensions/content-type.md) | |
| [[!UICONTROL ID da Sessão de Mídia]](/help/reporting/dimensions/media-session-id.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails._id` | `xdm.mediaReporting.`<br>`sessionDetails.ID` | Dimensão | [[!UICONTROL ID da Sessão de Mídia]](/help/reporting/dimensions/media-session-id.md) | |
| [[!UICONTROL Nome do reprodutor de conteúdo]](/help/reporting/dimensions/content-player-name.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.playerName` | `xdm.mediaReporting.`<br>`sessionDetails.playerName` | Dimensão | [[!UICONTROL Nome do reprodutor de conteúdo]](/help/reporting/dimensions/content-player-name.md) | |
| [[!UICONTROL Canal de conteúdo]](/help/reporting/dimensions/content-channel.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.broadcastChannel` | `xdm.mediaReporting.`<br>`sessionDetails.channel` | Dimensão | [[!UICONTROL Canal de conteúdo]](/help/reporting/dimensions/content-channel.md) | |
| [[!UICONTROL Segmento de conteúdo]](/help/reporting/dimensions/content-segment.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.videoSegment` | `xdm.mediaReporting.`<br>`sessionDetails.segment` | Dimensão | [[!UICONTROL Segmento de conteúdo]](/help/reporting/dimensions/content-segment.md) | |
| [[!UICONTROL Nome do conteúdo]](/help/reporting/dimensions/content-name.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._dc.title` | `xdm.mediaReporting.`<br>`sessionDetails.friendlyName` | Dimensão | [[!UICONTROL Nome do conteúdo]](/help/reporting/dimensions/content-name.md) | |
| Caminho do vídeo | *Não usado no AEP/CJA* | | | | propriedade específica do Adobe Analytics |
| [[!UICONTROL Programa]](/help/reporting/dimensions/show.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Series._iptc4xmpExt.Name` | `xdm.mediaReporting.`<br>`sessionDetails.show` | Dimensão | [[!UICONTROL Programa]](/help/reporting/dimensions/show.md) | |
| [[!UICONTROL Temporada]](/help/reporting/dimensions/season.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Season._iptc4xmpExt.Name` | `xdm.mediaReporting.`<br>`sessionDetails.season` | Dimensão | [[!UICONTROL Temporada]](/help/reporting/dimensions/season.md) | |
| [[!UICONTROL Episódio]](/help/reporting/dimensions/episode.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Episode._iptc4xmpExt.Name` | `xdm.mediaReporting.`<br>`sessionDetails.episode` | Dimensão | [[!UICONTROL Episódio]](/help/reporting/dimensions/episode.md) | |
| [[!UICONTROL Gênero]](/help/reporting/dimensions/genre.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._iptc4xmpExt.Genre` | `xdm.mediaReporting.`<br>`sessionDetails.genreList` | Dimensão | não suportado | Usar campo `mediaReporting` |
| [[!UICONTROL Rede]](/help/reporting/dimensions/network.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.broadcastNetwork` | `xdm.mediaReporting.`<br>`sessionDetails.network` | Dimensão | [[!UICONTROL Rede]](/help/reporting/dimensions/network.md) | |
| [[!UICONTROL Mostrar tipo]](/help/reporting/dimensions/show-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference.showType` | `xdm.mediaReporting.`<br>`sessionDetails.showType` | Dimensão | [[!UICONTROL Mostrar tipo]](/help/reporting/dimensions/show-type.md) | |
| [[!UICONTROL MVPD]](/help/reporting/dimensions/mvpd.md) | `xdm.media.mediaTimed.`<br>`idp` | `xdm.mediaReporting.`<br>`sessionDetails.mvpd` | Dimensão | [[!UICONTROL MVPD]](/help/reporting/dimensions/mvpd.md) | |
| [[!UICONTROL Autorizado]](/help/reporting/metrics/authorized.md) | Não suportado | `xdm.mediaReporting.`<br>`sessionDetails.authorized` | Dimensão | [[!UICONTROL Autorizado]](/help/reporting/metrics/authorized.md) | |
| [[!UICONTROL Parte do dia]](/help/reporting/dimensions/day-part.md) | Não suportado | `xdm.mediaReporting.`<br>`sessionDetails.dayPart` | Dimensão | [[!UICONTROL Parte do dia]](/help/reporting/dimensions/day-part.md) | |
| [[!UICONTROL Tipo de Feed de Mídia]](/help/reporting/dimensions/media-feed-type.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.sourceFeed` | `xdm.mediaReporting.`<br>`sessionDetails.feed` | Dimensão | [[!UICONTROL Tipo de Feed de Mídia]](/help/reporting/dimensions/media-feed-type.md) | |
| [[!UICONTROL Artista]](/help/reporting/dimensions/artist.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._xmpDM.artist` | `xdm.mediaReporting.`<br>`sessionDetails.artist` | Dimensão | [[!UICONTROL Artista]](/help/reporting/dimensions/artist.md) | |
| [[!UICONTROL Álbum]](/help/reporting/dimensions/album.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._xmpDM.album` | `xdm.mediaReporting.`<br>`sessionDetails.album` | Dimensão | [[!UICONTROL Álbum]](/help/reporting/dimensions/album.md) | |
| [[!UICONTROL Rótulo]](/help/reporting/dimensions/label.md) | Não suportado | `xdm.mediaReporting.`<br>`sessionDetails.label` | Dimensão | [[!UICONTROL Rótulo]](/help/reporting/dimensions/label.md) | |
| [[!UICONTROL Autor]](/help/reporting/dimensions/author.md) | Não suportado | `xdm.mediaReporting.`<br>`sessionDetails.author` | Dimensão | [[!UICONTROL Autor]](/help/reporting/dimensions/author.md) | |
| [[!UICONTROL Estação]](/help/reporting/dimensions/station.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._id3.Audio._id3.TRSN` | `xdm.mediaReporting.`<br>`sessionDetails.station` | Dimensão | [[!UICONTROL Estação]](/help/reporting/dimensions/station.md) | |
| [[!UICONTROL Publicador]](/help/reporting/dimensions/publisher.md) | `xdm.media.mediaTimed.`<br>`primaryAssetReference._id3.Audio._id3.TPUB` | `xdm.mediaReporting.`<br>`sessionDetails.publisher` | Dimensão | [[!UICONTROL Publicador]](/help/reporting/dimensions/publisher.md) | |
| [[!UICONTROL Inícios da mídia]](/help/reporting/metrics/media-starts.md) | `xdm.media.mediaTimed.`<br>`impressions.value` | `xdm.mediaReporting.`<br>`sessionDetails.isViewed` | Métrica | [[!UICONTROL Inícios da mídia]](/help/reporting/metrics/media-starts.md) | |
| [[!UICONTROL Início do conteúdo]](/help/reporting/metrics/content-starts.md) | `xdm.media.mediaTimed.`<br>`starts.value` | `xdm.mediaReporting.`<br>`sessionDetails.isPlayed` | Métrica | [[!UICONTROL Início do conteúdo]](/help/reporting/metrics/content-starts.md) | |
| [[!UICONTROL Conteúdo concluído]](/help/reporting/metrics/content-completes.md) | `xdm.media.mediaTimed.`<br>`completes.value` | `xdm.mediaReporting.`<br>`sessionDetails.isCompleted` | Métrica | [[!UICONTROL Conteúdo concluído]](/help/reporting/metrics/content-completes.md) | |
| [[!UICONTROL Tempo gasto com conteúdo]](/help/reporting/metrics/content-time-spent.md) | `xdm.media.mediaTimed.`<br>`timePlayed.value` | `xdm.mediaReporting.`<br>`sessionDetails.timePlayed` | Métrica | [[!UICONTROL Tempo gasto com conteúdo]](/help/reporting/metrics/content-time-spent.md) | |
| [[!UICONTROL Tempo gasto com a mídia]](/help/reporting/metrics/media-time-spent.md) | `xdm.media.mediaTimed.`<br>`totalTimePlayed.value` | `xdm.mediaReporting.`<br>`sessionDetails.totalTimePlayed` | Métrica | [[!UICONTROL Tempo gasto com a mídia]](/help/reporting/metrics/media-time-spent.md) | |
| [[!UICONTROL Tempo de reprodução exclusivo]](/help/reporting/metrics/unique-time-played.md) | Não suportado | `xdm.mediaReporting.`<br>`sessionDetails.uniqueTimePlayed` | Métrica | [[!UICONTROL Tempo de reprodução exclusivo]](/help/reporting/metrics/unique-time-played.md) | |
| [[!UICONTROL Marcador de progresso de 10%]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress10.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress10` | Métrica | [[!UICONTROL Marcador de progresso de 10%]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL Marcador de progresso de 25%]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress25.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress25` | Métrica | [[!UICONTROL Marcador de progresso de 25%]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL Marcador de progresso de 50%]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress50.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress50` | Métrica | [[!UICONTROL Marcador de progresso de 50%]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL Marcador de progresso de 75%]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress75.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress75` | Métrica | [[!UICONTROL Marcador de progresso de 75%]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL Marcador de progresso de 95%]](/help/reporting/metrics/progress-markers.md) | `xdm.media.mediaTimed.`<br>`progress95.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasProgress95` | Métrica | [[!UICONTROL Marcador de progresso de 95%]](/help/reporting/metrics/progress-markers.md) | |
| [[!UICONTROL Audiência média por minuto]](/help/reporting/metrics/average-minute-audience.md) | Não suportado | `xdm.mediaReporting.`<br>`sessionDetails.averageMinuteAudience` | Métrica | [[!UICONTROL Audiência média por minuto]](/help/reporting/metrics/average-minute-audience.md) | |
| Segundos desde a última chamada | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.sessionTimeout` | `xdm.mediaReporting.`<br>`sessionDetails.secondsSinceLastCall` | Métrica | Segundos desde a última chamada | |
| [[!UICONTROL Fluxos Impactados Pausados]](/help/reporting/metrics/paused-impacted-streams.md) | Não suportado | `xdm.mediaReporting.`<br>`sessionDetails.hasPauseImpactedStreams` | Métrica | [[!UICONTROL Fluxos Impactados Pausados]](/help/reporting/metrics/paused-impacted-streams.md) | cobrimos mediaTimed calculando esse valor a partir de outros eventos |
| [[!UICONTROL Pausar Eventos]](/help/reporting/metrics/pause-events.md) | `xdm.media.mediaTimed.`<br>`pauses.value` | `xdm.mediaReporting.`<br>`sessionDetails.pauseCount` | Métrica | [[!UICONTROL Pausar Eventos]](/help/reporting/metrics/pause-events.md) | |
| [[!UICONTROL Duração total da pausa]](/help/reporting/metrics/total-pause-duration.md) | `xdm.media.mediaTimed.`<br>`pauseTime.value` | `xdm.mediaReporting.`<br>`sessionDetails.pauseTime` | Métrica | [[!UICONTROL Duração total da pausa]](/help/reporting/metrics/total-pause-duration.md) | |
| [[!UICONTROL Resumo do conteúdo]](/help/reporting/metrics/content-resumes.md) | `xdm.media.mediaTimed.`<br>`resumes.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasResume` | Métrica | [[!UICONTROL Resumo do conteúdo]](/help/reporting/metrics/content-resumes.md) | |
| [[!UICONTROL Exibições do segmento de conteúdo]](/help/reporting/metrics/content-segment-views.md) | `xdm.media.mediaTimed.`<br>`mediaSegmentViews.value` | `xdm.mediaReporting.`<br>`sessionDetails.hasSegmentView` | Métrica | [[!UICONTROL Exibições do segmento de conteúdo]](/help/reporting/metrics/content-segment-views.md) | |

## Atualização dos parâmetros de estado do player

| Nome do campo | Campo XDM herdado | Caminho do campo XDM do relatório | Tipo de dados | Campo derivado | Notas |
| --- | --- | --- | --- | --- | --- |
| Fluxos afetados pelos Estados do player | Não suportado | `xdm.mediaReporting.`<br>`states.isSet` | Métrica | não suportado | usar o campo `mediaReporting` |
| Contagens de estados do player | Não suportado | `xdm.mediaReporting.`<br>`states.count` | Métrica | não suportado | usar o campo `mediaReporting` |
| Duração total dos estados do player | Não suportado | `xdm.mediaReporting.`<br>`states.time` | Métrica | não suportado | usar o campo `mediaReporting` |
| Nome do estado do player | Não suportado | `xdm.mediaReporting.`<br>`states.name` | Dimensão | não suportado | usar o campo `mediaReporting` |

## Parâmetros de capítulo

| Nome do campo | Campo XDM herdado | Caminho do campo XDM do relatório | Tipo de dados | Campo derivado | Notas |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL Capítulo]](/help/reporting/dimensions/chapter.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.chapterAssetReference._id` | `xdm.mediaReporting.`<br>`chapterDetails.ID` | Dimensão | [[!UICONTROL Capítulo]](/help/reporting/dimensions/chapter.md) | |
| [[!UICONTROL Início do capítulo]](/help/reporting/metrics/chapter-starts.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.impressions.value` | `xdm.mediaReporting.`<br>`chapterDetails.isStarted` | Métrica | [[!UICONTROL Início do capítulo]](/help/reporting/metrics/chapter-starts.md) | |
| [[!UICONTROL Capítulo concluído]](/help/reporting/metrics/chapter-completes.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.completes.value` | `xdm.mediaReporting.`<br>`chapterDetails.isCompleted` | Métrica | [[!UICONTROL Capítulo concluído]](/help/reporting/metrics/chapter-completes.md) | |
| [[!UICONTROL Tempo gasto com capítulo]](/help/reporting/metrics/chapter-time-spent.md) | `xdm.media.mediaTimed.`<br>`mediaChapter.timePlayed.value` | `xdm.mediaReporting.`<br>`chapterDetails.timePlayed` | Métrica | [[!UICONTROL Tempo gasto com capítulo]](/help/reporting/metrics/chapter-time-spent.md) | |

## Parâmetros de anúncio

| Nome do campo | Campo XDM herdado | Caminho do campo XDM do relatório | Tipo de dados | Campo derivado | Notas |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL ID do anúncio]](/help/reporting/dimensions/ad.md) | `xdm.advertising.`<br>`adAssetReference._id` | `xdm.mediaReporting.`<br>`advertisingDetails.name` | Dimensão | [[!UICONTROL ID do anúncio]](/help/reporting/dimensions/ad.md) | |
| [[!UICONTROL Anúncio Na Posição Do Pod]](/help/reporting/dimensions/ad-in-pod-position.md) | `xdm.advertising.`<br>`adAssetViewDetails.index` | `xdm.mediaReporting.`<br>`advertisingDetails.podPosition` | Dimensão | [[!UICONTROL Anúncio Na Posição Do Pod]](/help/reporting/dimensions/ad-in-pod-position.md) | |
| [[!UICONTROL Comprimento do anúncio]](/help/reporting/dimensions/ad-length.md) | `xdm.advertising.`<br>`adAssetReference._xmpDM.duration` | `xdm.mediaReporting.`<br>`advertisingDetails.length` | Métrica | [[!UICONTROL Comprimento do anúncio]](/help/reporting/dimensions/ad-length.md) | |
| [[!UICONTROL Nome do player do anúncio]](/help/reporting/dimensions/ad-player-name.md) | `xdm.advertising.`<br>`adAssetViewDetails.playerName` | `xdm.mediaReporting.`<br>`advertisingDetails.playerName` | Dimensão | [[!UICONTROL Nome do player do anúncio]](/help/reporting/dimensions/ad-player-name.md) | |
| [[!UICONTROL ID do ad break]](/help/reporting/dimensions/ad-pod.md) | `xdm.advertising.`<br>`adAssetViewDetails.adBreak._id` | `xdm.mediaReporting.`<br>`advertisingPodDetails.ID` | Dimensão | [[!UICONTROL ID do ad break]](/help/reporting/dimensions/ad-pod.md) | |
| [[!UICONTROL Nome do anúncio]](/help/reporting/dimensions/ad-name.md) | `xdm.advertising.`<br>`adAssetReference._dc.title` | `xdm.mediaReporting.`<br>`advertisingDetails.friendlyName` | Dimensão | [[!UICONTROL Nome do anúncio]](/help/reporting/dimensions/ad-name.md) | |
| [[!UICONTROL Anunciante]](/help/reporting/dimensions/advertiser.md) | `xdm.advertising.`<br>`adAssetReference.advertiser` | `xdm.mediaReporting.`<br>`advertisingDetails.advertiser` | Dimensão | [[!UICONTROL Anunciante]](/help/reporting/dimensions/advertiser.md) | |
| [[!UICONTROL ID da campanha]](/help/reporting/dimensions/campaign-id.md) | `xdm.advertising.`<br>`adAssetReference.campaign` | `xdm.mediaReporting.`<br>`advertisingDetails.campaignID` | Dimensão | [[!UICONTROL ID da campanha]](/help/reporting/dimensions/campaign-id.md) | |
| [[!UICONTROL Início do anúncio]](/help/reporting/metrics/ad-starts.md) | `xdm.advertising.`<br>`impressions.value` | `xdm.mediaReporting.`<br>`advertisingDetails.isStarted` | Métrica | [[!UICONTROL Início do anúncio]](/help/reporting/metrics/ad-starts.md) | |
| [[!UICONTROL Anúncio concluído]](/help/reporting/metrics/ad-completes.md) | `xdm.advertising.`<br>`completes.value` | `xdm.mediaReporting.`<br>`advertisingDetails.isCompleted` | Métrica | [[!UICONTROL Anúncio concluído]](/help/reporting/metrics/ad-completes.md) | |
| [[!UICONTROL Tempo gasto com anúncio]](/help/reporting/metrics/ad-time-spent.md) | `xdm.advertising.`<br>`timePlayed.value` | `xdm.mediaReporting.`<br>`advertisingDetails.timePlayed` | Métrica | [[!UICONTROL Tempo gasto com anúncio]](/help/reporting/metrics/ad-time-spent.md) | |

## Parâmetros de qualidade

| Nome do campo | Campo XDM herdado | Caminho do campo XDM do relatório | Tipo de dados | Campos derivados | Notas |
| --- | --- | --- | --- | --- | --- |
| [[!UICONTROL Taxa média de bits]](/help/reporting/metrics/average-bitrate.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.bitrateAverage.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bitrateAverage` | Ambos | [[!UICONTROL Taxa média de bits]](/help/reporting/metrics/average-bitrate.md) | |
| [[!UICONTROL Hora De Início]](/help/reporting/metrics/time-to-start.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.timeToStart.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.timeToStart` | Ambos | [[!UICONTROL Hora De Início]](/help/reporting/metrics/time-to-start.md) | |
| [[!UICONTROL Quadros Ignorados]](/help/reporting/metrics/dropped-frames.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.droppedFrames.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.droppedFrames` | Ambos | [[!UICONTROL Quadros Ignorados]](/help/reporting/metrics/dropped-frames.md) | |
| [[!UICONTROL Eventos de buffer]](/help/reporting/metrics/buffer-events.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.buffers.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bufferCount` | Ambos | [[!UICONTROL Eventos de buffer]](/help/reporting/metrics/buffer-events.md) | |
| [[!UICONTROL Duração total do buffer]](/help/reporting/metrics/total-buffer-duration.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.bufferTime.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bufferTime` | Ambos | [[!UICONTROL Duração total do buffer]](/help/reporting/metrics/total-buffer-duration.md) | |
| [[!UICONTROL Alterações na taxa de bits]](/help/reporting/metrics/bitrate-changes.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.bitrateChanges.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.bitrateChangeCount` | Ambos | [[!UICONTROL Alterações na taxa de bits]](/help/reporting/metrics/bitrate-changes.md) | |
| [[!UICONTROL Erros/Eventos de Erro]](/help/reporting/metrics/error-events.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.errors.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.errorCount` | Ambos | [[!UICONTROL Erros/Eventos de Erro]](/help/reporting/metrics/error-events.md) | |
| [[!UICONTROL IDs de erro do Player SDK]](/help/reporting/dimensions/player-sdk-error-ids.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.playerSdkErrors` | `xdm.mediaReporting.`<br>`qoeDataDetails.playerSdkErrors` | Dimensão | não suportado | usar o campo `mediaReporting` |
| [[!UICONTROL IDs de Erro Externo]](/help/reporting/dimensions/external-error-ids.md) | `xdm.media.mediaTimed.`<br>`primaryAssetViewDetails.qoe.externalSdkErrors` | `xdm.mediaReporting.`<br>`qoeDataDetails.externalErrors` | Dimensão | não suportado | usar o campo `mediaReporting` |
| [[!UICONTROL Desistências antes do início]](/help/reporting/metrics/drops-before-start.md) | `xdm.media.mediaTimed.`<br>`dropBeforeStarts.value` | `xdm.mediaReporting.`<br>`qoeDataDetails.isDroppedBeforeStart` | Métrica | [[!UICONTROL Desistências antes do início]](/help/reporting/metrics/drops-before-start.md) | |
| [[!UICONTROL Fluxos Impactados pelo Buffer]](/help/reporting/metrics/buffer-impacted-streams.md) | Não suportado | `xdm.mediaReporting.`<br>`qoeDataDetails.hasBufferImpactedStreams` | Métrica | [[!UICONTROL Fluxos Impactados pelo Buffer]](/help/reporting/metrics/buffer-impacted-streams.md) | calculado a partir de outros eventos |
| [[!UICONTROL A Alteração Na Taxa De Bits Afetou Os Fluxos]](/help/reporting/metrics/bitrate-change-impacted-streams.md) | Não suportado | `xdm.mediaReporting.`<br>`qoeDataDetails.hasBitrateChangeImpactedStreams` | Métrica | [[!UICONTROL A Alteração Na Taxa De Bits Afetou Os Fluxos]](/help/reporting/metrics/bitrate-change-impacted-streams.md) | calculado a partir de outros eventos |
| [[!UICONTROL Fluxos Impactados por Erros]](/help/reporting/metrics/error-impacted-streams.md) | Não suportado | `xdm.mediaReporting.`<br>`qoeDataDetails.hasErrorImpactedStreams` | Métrica | [[!UICONTROL Fluxos Impactados por Erros]](/help/reporting/metrics/error-impacted-streams.md) | calculado a partir de outros eventos |
| [[!UICONTROL Fluxos impactados por Quedas de Quadros]](/help/reporting/metrics/dropped-frame-impacted-streams.md) | Não suportado | `xdm.mediaReporting.`<br>`qoeDataDetails.hasDroppedFrameImpactedStreams` | Métrica | [[!UICONTROL Fluxos impactados por Quedas de Quadros]](/help/reporting/metrics/dropped-frame-impacted-streams.md) | calculado a partir de outros eventos |

## Classificações do Media Analytics

As classificações do Media Analytics são assimiladas na AEP por meio de um fluxo separado conhecido como ACDC. Cada grupo de classificação listado na tabela abaixo corresponde a um conjunto de dados exclusivo na AEP. No CJA, é necessário estabelecer uma conexão entre o conjunto de dados de eventos do Media Analytics e cada um dos conjuntos de dados de classificação.

### Conectar conjuntos de dados na Customer Journey Analytics

Para configurar a conexão no Customer Journey Analytics:

* Navegue até a guia **Conexões** e selecione **Criar nova conexão**.
* Na interface das Conexões, escolha **Adicionar conjuntos de dados** e localize o conjunto de dados de eventos do Media Analytics (usado para importar dados de mídia pelo ADC), juntamente com os quatro conjuntos de dados de classificação relevantes.

### Detalhes de configuração

Para cada conjunto de dados de pesquisa (conjunto de dados de classificação), configure da seguinte maneira:

* **conjunto de dados de vídeo**:
   * Chave: `_sandbox.key`
   * Chave correspondente: `Asset ID (media.mediaTimed.primaryAssetReference._id)`
   * Tipo de fonte de dados: `Web Data`

* **conjunto de dados de videoad**:
   * Chave: `_sandbox.key`
   * Chave correspondente: `Ad ID (advertising.adAssetReference._id)`
   * Tipo de fonte de dados: `Web Data`

* **conjunto de dados videoadpod**:
   * Chave: `_sandbox.key`
   * Chave correspondente: `Ad Pod ID (advertising.adAssetViewDetails.adBreak._id)`
   * Tipo de fonte de dados: `Web Data`

* **conjunto de dados videochapter**:
   * Chave: `_sandbox.key`
   * Chave correspondente: `Chapter identity (media.mediaTimed.mediaChapter.chapterAssetReference._id)`
   * Tipo de fonte de dados: `Web Data`

### Considerações sobre relatórios

Ao trabalhar com os conjuntos de dados de classificação durante os relatórios, faça referência aos caminhos de campo específicos da classificação (`ACDC XDM Path`) em vez dos campos XDM padrão do Media Analytics.

## Tabela de classificações

| Nome da classificação (grupo) | Nome do campo | Caminho XDM da ACDC |
| --- | --- | --- |
| vídeo | Chave/ID do ativo | `xdm.<_sandbox>.key` |
| vídeo | Duração do vídeo | `xdm.<_sandbox>.video_length` |
| vídeo | Nome do vídeo | `xdm.<_sandbox>.video_name` |
| vídeo | [[!UICONTROL ID do ativo]](/help/reporting/dimensions/asset-id.md) | `xdm.<_sandbox>.asset_id` |
| vídeo | [[!UICONTROL Primeira Transmissão]](/help/reporting/dimensions/first-air-date.md) | `xdm.<_sandbox>.first_air_date` |
| vídeo | [[!UICONTROL Primeira data digital]](/help/reporting/dimensions/first-digital-date.md) | `xdm.<_sandbox>.first_digital_date` |
| vídeo | [[!UICONTROL Classificação de conteúdo]](/help/reporting/dimensions/content-rating.md) | `xdm.<_sandbox>.content_rating` |
| vídeo | [[!UICONTROL Originador]](/help/reporting/dimensions/originator.md) | `xdm.<_sandbox>.originator` |
| videoad | Chave/ID do anúncio | `xdm.<_sandbox>.key` |
| videoad | [[!UICONTROL Comprimento do anúncio]](/help/reporting/dimensions/ad-length.md) | `xdm.<_sandbox>.ad_length` |
| videoad | [[!UICONTROL Nome do anúncio]](/help/reporting/dimensions/ad-name.md) | `xdm.<_sandbox>.ad_name` |
| videoad | [[!UICONTROL Creative ID]](/help/reporting/dimensions/creative-id.md) | `xdm.<_sandbox>.creative_id` |
| videoadpod | ID da chave/pod de anúncio | `xdm.<_sandbox>.key` |
| videoadpod | [[!UICONTROL Posição do pod]](/help/reporting/dimensions/pod-position.md) | `xdm.<_sandbox>.pod_position` |
| videoadpod | [[!UICONTROL Nome do pod]](/help/reporting/dimensions/pod-name.md) | `xdm.<_sandbox>.pod_name` |
| videochapter | Chave / Capítulo | `xdm.<_sandbox>.key` |
| videochapter | [[!UICONTROL Comprimento do capítulo]](/help/reporting/dimensions/chapter-length.md) | `xdm.<_sandbox>.chapter_length` |
| videochapter | [[!UICONTROL Deslocamento de capítulo]](/help/reporting/dimensions/chapter-offset.md) | `xdm.<_sandbox>.chapter_offset` |
| videochapter | [[!UICONTROL Posição do capítulo]](/help/reporting/dimensions/chapter-position.md) | `xdm.<_sandbox>.chapter_position` |
| videochapter | [[!UICONTROL Nome do capítulo]](/help/reporting/dimensions/chapter-name.md) | `xdm.<_sandbox>.chapter_name` |

## Variáveis personalizadas do Media Analytics

No Adobe Analytics, as variáveis personalizadas são atribuídas a eventos ou eVars diferentes, dependendo das regras de implementação definidas em cada conjunto de relatórios. Como resultado, quando essas variáveis personalizadas são importadas para o Adobe Experience Platform (AEP), elas são mapeadas para caminhos XDM diferentes.

* Os eventos são armazenados no caminho:

  `_experience.analytics.event<x>to<y>.event<number>.value`

* As eVars são armazenadas no caminho:

  `_experience.analytics.customDimensions.eVars.eVar<number>`

Em ambos os casos, o `<number>` corresponde ao evento específico ou ao número do eVar usado na configuração original do conjunto de relatórios do Adobe Analytics.

### Variáveis personalizadas

| Nome do campo | Caminho XDM | Tipo de dados |
| --- | --- | --- |
| [[!UICONTROL Sinalizador de mídia baixada]](/help/reporting/dimensions/media-downloaded-flag.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Métrica |
| Versão do SDK | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimensão |
| Versão da biblioteca de mídia | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimensão |
| [[!UICONTROL Formato de fluxo]](/help/reporting/dimensions/stream-format.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimensão |
| [[!UICONTROL Primeira Transmissão]](/help/reporting/dimensions/first-air-date.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimensão |
| [[!UICONTROL Primeira data digital]](/help/reporting/dimensions/first-digital-date.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimensão |
| [[!UICONTROL Dados Federados]](/help/reporting/metrics/federated-data.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>`<br>e<br>`xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Ambos |
| [[!UICONTROL Fluxos Estimados]](/help/reporting/metrics/estimated-streams.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Métrica |
| [[!UICONTROL Contagem de anúncios]](/help/reporting/metrics/ad-count.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Métrica |
| [[!UICONTROL Contagem de capítulos]](/help/reporting/metrics/chapter-count.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Métrica |
| [[!UICONTROL Creative ID]](/help/reporting/dimensions/creative-id.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimensão |
| [[!UICONTROL ID do Site]](/help/reporting/dimensions/site-id.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimensão |
| [[!UICONTROL URL DO Creative]](/help/reporting/dimensions/creative-url.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimensão |
| [[!UICONTROL ID de posicionamento]](/help/reporting/dimensions/placement-id.md) | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>` | Dimensão |
| Quadros por segundo | `xdm._experience.analytics.`<br>`customDimensions.eVars.eVar<number>`<br>e<br>`xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Ambos |
| IDs de erro do SDK do Media | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Métrica |
| [[!UICONTROL Fluxos Afetados pela Paralisação]](/help/reporting/metrics/stall-impacted-streams.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Métrica |
| [[!UICONTROL Parando Eventos]](/help/reporting/metrics/stall-events.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Métrica |
| [[!UICONTROL Duração total da paralisação]](/help/reporting/metrics/total-stalling-duration.md) | `xdm._experience.analytics.`<br>`event<x>to<y>.event<number>.value` | Métrica |
