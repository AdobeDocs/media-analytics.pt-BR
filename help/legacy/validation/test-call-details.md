---
title: Detalhes da chamada de teste
description: Explore as chamadas que você deve fazer para validar sua implementação.
uuid: d3a0e62f-2fc3-413d-ac56-adbbc9b3e983
exl-id: 5e167714-3f0c-4afa-b171-7d51cff6522e
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/98Oa98xntOkB9Fe3NQ30FUdvVk0JNKJMyzjgSTvncdI
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: e992d880-33bc-4949-a648-aa7d410276cd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 616
ht-degree: 86%

---

# Detalhes da chamada de teste{#test-call-details}

## Iniciar o player de mídia {#start-the-media-player}

### Chamada de início do Adobe Analytics (AppMeasurement) {#aa-start-call}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| `pev2` | ms_s |
| `a.media.friendlyName` | Título do episódio |
| _&#x200B;**`a.media.name`**&#x200B;_ | _&#x200B;**123456**&#x200B;_ |
| _&#x200B;**`a.media.length`**&#x200B;_ | _&#x200B;**120**&#x200B;_ |
| `a.media.playerName` | HTML 5 |
| _&#x200B;**`a.media.view`**&#x200B;_ | _&#x200B;**true**&#x200B;_ |
| `a.contentType` | vod |
| _&#x200B;**`custom.[value]`**&#x200B;_ | _&#x200B;**Campos de metadados personalizados**&#x200B;_ |
| _&#x200B;**`a.media.[value]`**&#x200B;_ | _&#x200B;**Campos de metadados padrão**&#x200B;_ |

**Notas:**

* As variáveis de dados de contexto adicionais devem estar presentes e conter metadados. Consulte os detalhes dos metadados abaixo.
* O comprimento para fluxos lineares deve ser definido de acordo com a melhor estimativa para a exibição atual.

### Metadados padrão na chamada de início do Adobe Analytics (AppMeasurement) {#std-metadata-aa}

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

### Metadados personalizados na chamada de início do Adobe Analytics (AppMeasurement) {#custom-metadata-aa}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| `custom.metadataA` | valor |
| `custom.metadataB` | valor |

### Chamada de início do Media Analytics (heartbeats) {#ma-start-call}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| `s:event:type` | start |
| _&#x200B;**`l:event:playhead`**&#x200B;_ | _&#x200B;**0**&#x200B;_ |
| `l:event:duration` | 4 |
| `s:asset:name` | Título do episódio |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |
| _&#x200B;**`s:meta:custom.[value]`**&#x200B;_ | _&#x200B;**Campos de metadados personalizados**&#x200B;_ |
| _&#x200B;**`s:meta:a.media.[value]`**&#x200B;_ | _&#x200B;**Campos de metadados padrão**&#x200B;_ |

**Notas:**

* As variáveis de dados de contexto adicionais devem estar presentes e conter metadados. Consulte os detalhes dos metadados abaixo.
* A posição do indicador de reprodução para fluxos lineares no início do vídeo deve ser definida como os segundos decorridos desde o início do programa atual, não como 0.

### Metadados padrão na chamada de início do Media Analytics (heartbeats) {#std-metadata-ma}

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

### Metadados personalizados na chamada de início do Media Analytics (heartbeats) {#custom-metadata-ma}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| `s:meta:custom.metadata` | valor |
| `s:meta:custom.metadata` | valor |

### Chamada de início do Adobe Analytics do Media Analytics (heartbeats) {#ma-aa-start}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**aa_start**&#x200B;_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | Título do episódio |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**Notas:**

* Esta chamada indica que o SDK do Media solicitou que uma chamada `pev2=ms_s` do Adobe Analytics seja enviada para o servidor do Adobe Analytics (AppMeasurement).
* Esta chamada não contém metadados personalizados.

## Exibir a reprodução do anúncio {#view-ad-playback}

### Chamada de início de anúncio do Adobe Analytics (AppMeasurement) {#aa-ad-start-call}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| _&#x200B;**`pev2`**&#x200B;_ | _&#x200B;**msa_s**&#x200B;_ |
| `a.media.name` | 123456 |
| _&#x200B;**`a.media.ad.name`**&#x200B;_ | _&#x200B;**9378**&#x200B;_ |
| `a.media.ad.friendlyName` | Video_VPAID_DFA |
| `a.media.ad.podFriendlyName` | pré-rolagem |
| _&#x200B;**`a.media.ad.length`**&#x200B;_ | _&#x200B;**15**&#x200B;_ |
| `a.media.ad.playerName` | HTML 5 |
| `a.media.ad.pod` | c27aaf3ff8224bb6b9ebfe1b2e79073d_1 |
| `a.media.ad.podPosition` | 1 |
| `a.media.ad.podSecond` | 0.0 |
| _&#x200B;**`a.media.ad.view`**&#x200B;_ | _&#x200B;**true**&#x200B;_ |
| _&#x200B;**`custom.[value]`**&#x200B;_ | _&#x200B;**Campos de metadados**&#x200B;_ |
| _&#x200B;**`a.media.[value]`**&#x200B;_ | _&#x200B;**Campos de metadados padrão**&#x200B;_ |

**Notas:**

* As variáveis de dados de contexto adicionais devem estar presentes e conter metadados. Consulte os detalhes dos metadados abaixo.
* O comprimento do anúncio pode ser definido como -1 se não estiver disponível no início do anúncio.

### Metadados padrão na chamada de início do anúncio do Adobe Analytics (AppMeasurement) {#std-metadata-aa-ad-start}

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

### Metadados personalizados na chamada de início de anúncio do Adobe Analytics (AppMeasurement) {#custom-metadata-aa-ad-start}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| `custom.metadata` | valor |
| `custom.metadata` | valor |

### Chamada de início de anúncio do Media Analytics (heartbeats) {#ma-ad-start-call}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**start**&#x200B;_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:ad_id` | 9378 |
| _&#x200B;**`l:asset:length`**&#x200B;_ | _&#x200B;**120**&#x200B;_ |
| `s:stream:type` | vod |
| _&#x200B;**`s:asset:type`**&#x200B;_ | _&#x200B;**Publicidade**&#x200B;_ |
| _&#x200B;**`s:meta:custom.[value]`**&#x200B;_ | _&#x200B;**Campos de metadados personalizados**&#x200B;_ |
| _&#x200B;**`s:meta:a.media.[value]`**&#x200B;_ | _&#x200B;**Campos de metadados padrão**&#x200B;_ |

**Notas:**

* As variáveis de dados de contexto adicionais devem estar presentes e conter metadados. Consulte os detalhes dos metadados abaixo.
* O comprimento do anúncio pode ser definido como -1 se não estiver disponível no início do anúncio.

### Metadados padrão na chamada de início do Media Analytics (heartbeats) {#std-metadata-ma-ad-start}

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

### Metadados personalizados na chamada de início de anúncio do Media Analytics (heartbeats) {#custom-metadata-ma-ad-start}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| `s:meta:custom.metadata` | valor |
| `s:meta:custom.metadata` | valor |

### Chamada de início de anúncio do Adobe Analytics do Media Analytics (heartbeats) {#ma-aa-ad-start-call}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**aa_ad_start**&#x200B;_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| `s:asset:type` | Publicidade |

### Chamada de reprodução de anúncio do Media Analytics (heartbeats) {#ma-ad-play-call}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**play**&#x200B;_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _&#x200B;**`s:asset:type`**&#x200B;_ | _&#x200B;**Publicidade**&#x200B;_ |

### Chamada de pausa de anúncio do Media Analytics (heartbeats) {#ma-ad-pause-call}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**pause**&#x200B;_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _&#x200B;**`s:asset:type`**&#x200B;_ | _&#x200B;**Publicidade**&#x200B;_ |

### Chamada de anúncio concluído do Adobe Analytics do Media Analytics (heartbeats) {#ma-aa-ad-complete-call}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**complete**&#x200B;_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _&#x200B;**`s:asset:type`**&#x200B;_ | _&#x200B;**Publicidade**&#x200B;_ |

## Reproduzir conteúdo principal {#play-main-content}

### Chamada de reprodução do Media Analytics (heartbeats) {#ma-play-call}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| `s:event:type` | play |
| _&#x200B;**`l:event:playhead`**&#x200B;_ | _&#x200B;**29**&#x200B;_ |
| _&#x200B;**`l:event:duration`**&#x200B;_ | _&#x200B;**10189**&#x200B;_ |
| `s:asset:name` | Título do episódio |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**Notas:**

* A posição do indicador de reprodução deve ser incrementada em 10 segundos com cada chamada de reprodução.
* O valor `l:event:duration` representa o número de milissegundos desde a última chamada de rastreamento e deve ser basicamente o mesmo valor em cada chamada de 10 segundos.

## Pausar conteúdo principal {#pause-main-content}

### Chamada de pausa do Media Analytics (heartbeats) {#ma-pause-call}

| Parâmetro |  Valor (exemplo)  |
|---|---|
| _&#x200B;**`s:event:type`**&#x200B;_ | _&#x200B;**pause**&#x200B;_ |
| _&#x200B;**`l:event:playhead`**&#x200B;_ | _&#x200B;**29**&#x200B;_ |
| `l:event:duration` | 10189 |
| `s:asset:name` | Título do episódio |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |
