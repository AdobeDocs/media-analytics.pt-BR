---
title: Explicação sobre as chaves de metadados do Roku
description: Saiba mais sobre as chaves de metadados do Roku disponíveis e visualize toda a lista de constantes de metadados padrão.
uuid: 2ca6bb1d-c545-43d3-9c3e-63b890aa268d
exl-id: 687dbaa5-4723-4b3f-ab1e-4d5bf447cddf
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 91%

---

# Chaves de metadados do Roku{#roku-metadata-keys}

Os metadados padrão de vídeo, áudio e anúncios podem ser definidos em objetos de informação de mídia e anúncio respectivamente. Usando as chaves de constantes para metadados de vídeo/anúncio, defina o dicionário que contém os metadados padrão em um objeto de informação antes de chamar as APIs de rastreamento. Consulte as tabelas abaixo para obter a lista completa de constantes de metadados padrão, seguida de exemplos.

## Constantes de metadados de vídeo {#video-metadata-constants}

| Nome dos metadados | Chave de dados de contexto | Nome da constante |
| --- | --- | --- |
| Programa | `a.media.show` | `MEDIA_VideoMetadataKeySHOW` |
| Temporada | `a.media.season` | `MEDIA_VideoMetadataKeySEASON` |
| Episódio | `a.media.episode` | `MEDIA_VideoMetadataKeyEPISODE` |
| Ativo | `a.media.asset` | `MEDIA_VideoMetadataKeyASSET_ID` |
| Gênero | `a.media.genre` | `MEDIA_VideoMetadataKeyGENRE` |
| Data da primeira exibição | `a.media.airDate` | `MEDIA_VideoMetadataKeyFIRST_AIR_DATE` |
| Data da primeira exibição digital | `a.media.digitalDate` | `MEDIA_VideoMetadataKeyFIRST_DIGITAL_DATE` |
| Classificação | `a.media.rating` | `MEDIA_VideoMetadataKeyRATING` |
| Originador | `a.media.originator` | `MEDIA_VideoMetadataKeyORIGINATOR` |
| Rede | `a.media.network` | `MEDIA_VideoMetadataKeyNETWORK` |
| Mostrar tipo | `a.media.type` | `MEDIA_VideoMetadataKeySHOW_TYPE` |
| Carregamento do anúncio | `a.media.adLoad` | `MEDIA_VideoMetadataKeyAD_LOAD` |
| MVPD | `a.media.pass.mvpd` | `MEDIA_VideoMetadataKeyMVPD` |
| Autorizado | `a.media.pass.auth` | `MEDIA_VideoMetadataKeyAUTHORIZED` |
| Faixa de horário | `a.media.dayPart` | `MEDIA_VideoMetadataKeyDAY_PART` |
| Feed | `a.media.feed` | `MEDIA_VideoMetadataKeyFEED` |
| Formato de transmissão | `a.media.format` | `MEDIA_VideoMetadataKeySTREAM_FORMAT` |

## Constantes de metadados de áudio {#audio-metadata-constants}

| Nome dos metadados | Chave de dados de contexto | Nome da constante |
| --- | --- | --- |
| Artista | `a.media.artist` | `MEDIA_AudioMetadataKeyARTIST` |
| Álbum | `a.media.album` | `MEDIA_AudioMetadataKeyALBUM` |
| Rótulo | `a.media.label` | `MEDIA_AudioMetadataKeyLABEL` |
| Autor | `a.media.author` | `MEDIA_AudioMetadataKeyAUTHOR` |
| Estação | `a.media.station` | `MEDIA_AudioMetadataKeySTATION` |
| Editor | `a.media.publisher` | `MEDIA_AudioMetadataKeyPUBLISHER` |

## Constantes de metadados de anúncio {#ad-metadata-constants}

| Nome dos metadados | Chave de dados de contexto | Nome da constante |
| --- | --- | --- |
| Anunciante | `a.media.ad.advertiser` | `MEDIA_AdMetadataKeyADVERTISER` |
| ID da campanha | `a.media.ad.campaign` | `MEDIA_AdMetadataKeyCAMPAIGN_ID` |
| ID de criação | `a.media.ad.creative` | `MEDIA_AdMetadataKeyCREATIVE_ID` |
| ID de posicionamento | `a.media.ad.placement` | `MEDIA_AdMetadataKeyPLACEMENT_ID` |
| ID do site | `a.media.ad.site` | `MEDIA_AdMetadataKeyPLACEMENT_ID` |
| URL da arte | `a.media.ad.creativeURL` | `MEDIA_AdMetadataKeyCREATIVE_URL` |

## Constantes {#constants}

Você pode usar as seguintes constantes para rastrear eventos de mídia:

### Outras constantes

| Constante | Descrição   |
|---|---|
| `ERROR_SOURCE_PLAYER` | Constante para a fonte do erro como Reprodutor |

### Constantes de MediaObjectkey (usadas como chaves nas instâncias MediaObject)

| Constante | Descrição   |
| --- | --- |
| `MEDIA_STANDARD_MEDIA_METADATA` | Constante para definir metadados no `MediaInfo` `trackLoad` |
| `MEDIA_STANDARD_AD_METADATA` | Constante para definir os metadados de anúncios no `EventData` `trackEvent` |
| `MEDIA_RESUMED` | Constante para enviar um heartbeat de vídeo retomada. Para retomar o rastreamento de vídeo de um conteúdo anteriormente interrompido, você precisa definir a propriedade `MEDIA_RESUMED` no objeto `mediaInfo` quando chamar `mediaTrackLoad`. (`MEDIA_RESUMED` não é um evento que você pode rastrear usando a API `mediaTrackEvent`.) `MEDIA_RESUMED` deve ser definido como verdadeiro quando um aplicativo deseja continuar a rastrear o conteúdo que um usuário parou de assistir, mas que agora pretende retomar. <br/><br/>Por exemplo, digamos que um usuário assista 30% do conteúdo e então feche o aplicativo. Isso levará à sessão que está sendo encerrada. Posteriormente, se o usuário retornar ao mesmo conteúdo e o aplicativo permitir que ele retome do ponto em que parou, o aplicativo deverá definir `MEDIA_RESUMED` como &quot;true&quot; enquanto chama a API `mediaTrackLoad`. O resultado é que essas duas sessões de mídia diferentes para o mesmo conteúdo de vídeo podem ser vinculadas. Este é um exemplo de implementação: <br/><br/> `mediaInfo =` <br/>   `adb_media_init_mediainfo(` <br/>     `"test_media_name",` <br/>     `"test_media_id",`<br/>      `10,` <br/>     `"vod"` <br/> `)` <br/> `mediaInfo[ADBMobile().MEDIA_RESUMED] = true` <br/> `mediaContextData = {}` <br/>  `ADBMobile().mediaTrackLoad(mediaInfo, mediaContextData)` <br/><br/>Isso criará uma nova sessão para o vídeo, mas também fará com que o SDK envie uma solicitação de heartbeat contendo o tipo de evento “retomar”, que pode ser usado nos relatórios para vincular duas sessões de mídia diferentes. |

### Constantes de tipo de conteúdo

| Constante | Descrição   |
|---|---|
| `MEDIA_STREAM_TYPE_LIVE` | Constante para o tipo de fluxo LIVE |
| `MEDIA_STREAM_TYPE_VOD` | Constante para o tipo de fluxo de VOD |

### Constantes de tipo de evento (usadas para a chamada trackEvent)

| Constante | Descrição   |
|---|---|
| `MEDIA_BUFFER_START` | Tipo de evento para Início do buffer |
| `MEDIA_BUFFER_COMPLETE` | Tipo de evento para Buffer concluído |
| `MEDIA_SEEK_START` | Tipo de evento para Início da busca |
| `MEDIA_SEEK_COMPLETE` | Tipo de evento para Busca concluída |
| `MEDIA_BITRATE_CHANGE` | Tipo de evento para Alteração na taxa de bits |
| `MEDIA_CHAPTER_START` | Tipo de evento para Início do capítulo |
| `MEDIA_CHAPTER_COMPLETE` | Tipo de evento para capítulo concluído |
| `MEDIA_CHAPTER_SKIP` | Tipo de evento para Início do anúncio |
| `MEDIA_AD_BREAK_START` | Tipo de evento para Início do anúncio |
| `MEDIA_AD_BREAK_COMPLETE` | Tipo de evento para AdBreak concluído |
| `MEDIA_AD_BREAK_SKIP` | Tipo de evento para AdBreak ignorado |
| `MEDIA_AD_START` | Tipo de evento para Início do anúncio |
| `MEDIA_AD_COMPLETE` | Tipo de evento para Anúncio concluído |
| `MEDIA_AD_SKIP` | Tipo de evento para Anúncio ignorado |
