---
seo-title: Detalhes da chamada de teste
title: Detalhes da chamada de teste
uuid: d 3 a 0 e 62 f -2 fc 3-413 d-ac 56-adbbc 9 b 3 e 983
translation-type: tm+mt
source-git-commit: d694ced982140c1f8020c0be304492aee0495cdc

---


# Detalhes da chamada de teste{#test-call-details}

## Iniciar o player de mídia {#start-the-media-player}

### Chamada de início do Adobe Analytics (appmeasurement) {#aa-start-call}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| `pev2` | ms_s |
| `a.media.friendlyName` | Título do episódio |
| _**`a.media.name`**_ | _**123456**_ |
| _**`a.media.length`**_ | _**120**_ |
| `a.media.playerName` | HTML 5 |
| _**`a.media.view`**_ | _**true**_ |
| `a.contentType` | vod |
| _**`custom.[value]`**_ | _**Campos de metadados personalizados**_ |
| _**`a.media.[value]`**_ | _**Campos de metadados padrão**_ |

**Notas:**

* As variáveis de dados de contexto adicionais devem estar presentes e conter metadados. Veja os detalhes dos metadados abaixo.
* A duração dos fluxos lineares deve ser definida para a melhor estimativa do programa atual.

### Metadados padronizados na chamada do Adobe Analytics (appmeasurement) Start {#std-metadata-aa}

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

### Metadados personalizados na chamada do Adobe Analytics (appmeasurement) Start {#custom-metadata-aa}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| `custom.metadataA` | value |
| `custom.metadataB` | value |

### Chamada de início do Media Analytics (heartbeats) {#ma-start-call}

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

### Metadados padronizados na chamada de início do Media Analytics (heartbeats) {#std-metadata-ma}

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

### Metadados personalizados na chamada do Media Analytics (heartbeats) Start {#custom-metadata-ma}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Chamada de início do Media Analytics (heartbeats) Adobe Analytics {#ma-aa-start}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| _**`s:event:type`**_ | _**aa_start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | Título do episódio |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**Observações:**

* Esta chamada indica que o Media SDK solicitou que uma chamada do Adobe Analytics `pev2=ms_s` seja enviada para o servidor Adobe Analytics (appmeasurement).
* Esta chamada não contém metadados personalizados.

## Exibir a reprodução do anúncio {#view-ad-playback}

### Chamada de início de anúncio do Adobe Analytics (appmeasurement) {#aa-ad-start-call}

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

### Standard metadata in Adobe Analytics (AppMeasurement) Ad Start call {#std-metadata-aa-ad-start}

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

### Metadados personalizados na chamada de início de anúncio do Adobe Analytics (appmeasurement) {#custom-metadata-aa-ad-start}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| `custom.metadata` | value |
| `custom.metadata` | value |

### Chamada de anúncio do Media Analytics (heartbeats) {#ma-ad-start-call}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| _**`s:event:type`**_ | _**start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:ad_id` | 9378 |
| _**`l:asset:length`**_ | _**120**_ |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |
| _**`s:meta:custom.[value]`**_ | _**Campos de metadados personalizados**_ |
| _**`s:meta:a.media.[value]`**_ | _**Campos de metadados padrão**_ |

**Notas:**

* As variáveis de dados de contexto adicionais devem estar presentes e conter metadados. Veja os detalhes dos metadados abaixo.
* A duração do anúncio deverá ser definida para -1, se não estiver disponível no início do anúncio.

### Standard metadata in Media Analytics (heartbeats) Ad Start call {#std-metadata-ma-ad-start}

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

### Metadados personalizados na chamada do Media Analytics (heartbeats) chamada Ad Start {#custom-metadata-ma-ad-start}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Chamada de início de anúncio do Media Analytics (heartbeats) Adobe Analytics {#ma-aa-ad-start-call}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| _**`s:event:type`**_ | _**aa_ad_start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| `s:asset:type` | ad |

### Chamada Ad Analytics (heartbeats) Play Play {#ma-ad-play-call}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| _**`s:event:type`**_ | _**play**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

### Chamada de Media Analytics (heartbeats) chamada Pausar anúncio {#ma-ad-pause-call}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| _**`s:event:type`**_ | _**pause**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

### Chamada do Media Analytics (heartbeats) Adobe Analytics Ad Complete {#ma-aa-ad-complete-call}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| _**`s:event:type`**_ | _**complete**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

## Reproduzir conteúdo principal {#play-main-content}

### Chamada Play Analytics (heartbeats) Play {#ma-play-call}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| `s:event:type` | play |
| _**`l:event:playhead`**_ | _**29**_ |
| _**`l:event:duration`**_ | _**10189**_ |
| `s:asset:name` | Título do episódio |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**Observações:**

* A posição do indicador de reprodução deve aumentar em 10 segundos com cada chamada de play.
* O valor `l:event:duration` representa o número de milissegundos desde a última chamada de rastreamento e deve ser basicamente o mesmo valor em cada chamada de 10 segundos.

## Pausar conteúdo principal {#pause-main-content}

### Chamada de pausa do Media Analytics (heartbeats) {#ma-pause-call}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| _**`s:event:type`**_ | _**pause**_ |
| _**`l:event:playhead`**_ | _**29**_ |
| `l:event:duration` | 10189 |
| `s:asset:name` | Título do episódio |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |


