---
title: Detalhes da chamada de teste
description: Explore as chamadas que devem ser feitas para validar sua implementação.
uuid: d3a0e62f-2fc3-413d-ac56-adbbc9b3e983
exl-id: 5e167714-3f0c-4afa-b171-7d51cff6522e
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 98%

---

# Detalhes da chamada de teste{#test-call-details}

## Iniciar o reprodutor de mídia {#start-the-media-player}

### Chamada de início do Adobe Analytics (AppMeasurement)  {#aa-start-call}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| `pev2` | ms_s |
| `a.media.friendlyName` | Título do episódio |
| _**`a.media.name`**_ | _**123456**_ |
| _**`a.media.length`**_ | _**120º**_ |
| `a.media.playerName` | HTML 5 |
| _**`a.media.view`**_ | _**true**_ |
| `a.contentType` | vod |
| _**`custom.[value]`**_ | _**Campos de metadados personalizados**_ |
| _**`a.media.[value]`**_ | _**Campos de metadados padrão**_ |

**Notas:**

* As variáveis de dados de contexto adicionais devem estar presentes e conter metadados. Veja os detalhes dos metadados abaixo.
* A duração dos fluxos lineares deve ser definida para a melhor estimativa do programa atual.

### Metadados padrão na chamada de início do Adobe Analytics (AppMeasurement)  {#std-metadata-aa}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| `a.media.show` | Mostrar título |
| `a.media.season` | 6 |
| `a.media.episode` | Título do episódio |
| `a.media.asset_id` | 123456 |
| `a.media.genre` | comédia |
| `a.media.first_air_date` | 2016-07-04 |
| `a.media.rating` | TV-14 |
| `a.media.originator` | casa de produção |
| `a.media.network` | rede |
| `a.media.ad_load` | 1 |
| `a.media.mvpd` | mvpd |
| `a.media.authorized` | desbloqueado |
| `a.media.feed` | nenhum feed |
| `a.media.stream_format` | 0 |

### Metadados personalizados na chamada de início do Adobe Analytics (AppMeasurement)  {#custom-metadata-aa}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| `custom.metadataA` | valor |
| `custom.metadataB` | valor |

### Chamada de início do Media Analytics (heartbeats)  {#ma-start-call}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| `s:event:type` | start |
| _**`l:event:playhead`**_ | _**0**_ |
| `l:event:duration` | 4 |
| `s:asset:name` | Título do episódio |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |
| _**`s:meta:custom.[value]`**_ | _**Campos de metadados personalizados**_ |
| _**`s:meta:a.media.[value]`**_ | _**Campos de metadados padrão**_ |

**Notas:**

* As variáveis de dados de contexto adicionais devem estar presentes e conter metadados. Veja os detalhes dos metadados abaixo.
* A posição do indicador de reprodução para fluxos lineares no início do vídeo deve ser definida para os segundos decorridos desde o início do programa atual, não 0.

### Metadados padrão na chamada de início do Media Analytics (heartbeats)  {#std-metadata-ma}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| `s:meta:a.media.show` | Programa |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | Título do episódio |
| `s:meta:a.media.asset_id` | 123456 |
| `s:meta:a.media.genre` | comédia |
| `s:meta:a.media.first_air_date` | 2018-07-04 |
| `s:meta:a.media.rating` | TV-14 |
| `s:meta:a.media.originator` | casa de produção |
| `s:meta:a.media.network` | rede |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | desbloqueado |
| `s:meta:a.media.feed` | nenhum feed |
| `s:meta:a.media.stream_format` | 0 |

### Metadados personalizados na chamada de início do Media Analytics (heartbeats)  {#custom-metadata-ma}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| `s:meta:custom.metadata` | valor |
| `s:meta:custom.metadata` | valor |

### Chamada de início do Adobe Analytics do Media Analytics (heartbeats)  {#ma-aa-start}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| _**`s:event:type`**_ | _**aa_start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | Título do episódio |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120º |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**Notas:**

* Esta chamada indica que o SDK do Media solicitou que uma chamada `pev2=ms_s` do Adobe Analytics seja enviada para o servidor do Adobe Analytics (AppMeasurement).
* Esta chamada não contém metadados personalizados.

## Exibir a reprodução do anúncio {#view-ad-playback}

### Chamada de início de anúncio do Adobe Analytics (AppMeasurement)  {#aa-ad-start-call}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| _**`pev2`**_ | _**msa_s**_ |
| `a.media.name` | 123456 |
| _**`a.media.ad.name`**_ | _**9378**_ |
| `a.media.ad.friendlyName` | Video_VPAID_DFA |
| `a.media.ad.podFriendlyName` | pré-rolagem |
| _**`a.media.ad.length`**_ | _**15**_ |
| `a.media.ad.playerName` | HTML 5 |
| `a.media.ad.pod` | c27aaf3ff8224bb6b9ebfe1b2e79073d_1 |
| `a.media.ad.podPosition` | 1 |
| `a.media.ad.podSecond` | 0.0 |
| _**`a.media.ad.view`**_ | _**Verdadeiro**_ |
| _**`custom.[value]`**_ | _**Campos de metadados**_ |
| _**`a.media.[value]`**_ | _**Campos de metadados padrão**_ |

**Notas:**

* As variáveis de dados de contexto adicionais devem estar presentes e conter metadados. Veja os detalhes dos metadados abaixo.
* A duração do anúncio deverá ser definida para -1, se não estiver disponível no início do anúncio.

### Metadados padrão na chamada de início do anúncio do Adobe Analytics (AppMeasurement)  {#std-metadata-aa-ad-start}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| `a.media.show` | Mostrar título |
| `a.media.season` | 6 |
| `a.media.episode` | Título do episódio |
| `a.media.asset_id` | 123456 |
| `a.media.genre` | comédia |
| `a.media.first_air_date` | 2016-07-04 |
| `a.media.rating` | TV-14 |
| `a.media.originator` | casa de produção |
| `a.media.network` | rede |
| `a.media.ad_load` | 1 |
| `a.media.mvpd` | mvpd |
| `a.media.authorized` | desbloqueado |
| `a.media.feed` | nenhum feed |
| `a.media.stream_format` | 0 |

### Metadados personalizados na chamada de início de anúncio do Adobe Analytics (AppMeasurement)  {#custom-metadata-aa-ad-start}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| `custom.metadata` | valor |
| `custom.metadata` | valor |

### Chamada de início de anúncio do Media Analytics (heartbeats)  {#ma-ad-start-call}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| _**`s:event:type`**_ | _**start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:ad_id` | 9378 |
| _**`l:asset:length`**_ | _**120º**_ |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |
| _**`s:meta:custom.[value]`**_ | _**Campos de metadados personalizados**_ |
| _**`s:meta:a.media.[value]`**_ | _**Campos de metadados padrão**_ |

**Notas:**

* As variáveis de dados de contexto adicionais devem estar presentes e conter metadados. Veja os detalhes dos metadados abaixo.
* A duração do anúncio deverá ser definida para -1, se não estiver disponível no início do anúncio.

### Metadados padrão na chamada de início do Media Analytics (heartbeats)  {#std-metadata-ma-ad-start}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| `s:meta:a.media.show` | Programa |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | Título do episódio |
| `s:meta:a.media.asset_id` | 123456 |
| `s:meta:a.media.genre` | comédia |
| `s:meta:a.media.first_air_date` | 2018-07-04 |
| `s:meta:a.media.rating` | TV-14 |
| `s:meta:a.media.originator` | casa de produção |
| `s:meta:a.media.network` | rede |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | desbloqueado |
| `s:meta:a.media.feed` | nenhum feed |
| `s:meta:a.media.stream_format` | 0 |

### Metadados personalizados na chamada de início de anúncio do Media Analytics (heartbeats)  {#custom-metadata-ma-ad-start}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| `s:meta:custom.metadata` | valor |
| `s:meta:custom.metadata` | valor |

### Chamada de início de anúncio do Adobe Analytics do Media Analytics (heartbeats)  {#ma-aa-ad-start-call}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| _**`s:event:type`**_ | _**aa_ad_start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| `s:asset:type` | ad |

### Chamada de reprodução de anúncio do Media Analytics (heartbeats)  {#ma-ad-play-call}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| _**`s:event:type`**_ | _**play**_ |
| `l:event:playhead` | 15. |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15. |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

### Chamada de pausa de anúncio do Media Analytics (heartbeats)  {#ma-ad-pause-call}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| _**`s:event:type`**_ | _**pause**_ |
| `l:event:playhead` | 15. |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15. |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

### Chamada de anúncio concluído do Adobe Analytics do Media Analytics (heartbeats)  {#ma-aa-ad-complete-call}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| _**`s:event:type`**_ | _**complete**_ |
| `l:event:playhead` | 15. |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15. |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

## Reproduzir conteúdo principal {#play-main-content}

### Chamada de reprodução do Media Analytics (heartbeats)  {#ma-play-call}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| `s:event:type` | play |
| _**`l:event:playhead`**_ | _**29º**_ |
| _**`l:event:duration`**_ | _**10189**_ |
| `s:asset:name` | Título do episódio |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120º |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**Notas:**

* A posição do indicador de reprodução deve ser incrementada em 10 segundos com cada chamada de reprodução.
* O valor `l:event:duration` representa o número de milissegundos desde a última chamada de rastreamento e deve ser basicamente o mesmo valor em cada chamada de 10 segundos.

## Pausar conteúdo principal {#pause-main-content}

### Chamada de pausa do Media Analytics (heartbeats)  {#ma-pause-call}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| _**`s:event:type`**_ | _**pause**_ |
| _**`l:event:playhead`**_ | _**29º**_ |
| `l:event:duration` | 10189 |
| `s:asset:name` | Título do episódio |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120º |
| `s:stream:type` | vod |
| `s:asset:type` | main |
