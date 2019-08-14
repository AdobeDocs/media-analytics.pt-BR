---
seo-title: Detalhes da chamada de teste
title: Detalhes da chamada de teste
uuid: d 3 a 0 e 62 f -2 fc 3-413 d-ac 56-adbbc 9 b 3 e 983
translation-type: tm+mt
source-git-commit: 1b785378750349c4f316748d228754cb64f70bca

---


# Detalhes da chamada de teste{#test-call-details}

## Iniciar o reprodutor de vídeo {#section_qts_xff_f2b}

### Chamada de início do Media Analytics

| Parâmetro | Valor (exemplo)  |
|---|---|
| `pev2` | ms_s |
| `a.media.friendlyName` | Título do episódio |
| `a.media.name` | 123456 |
| `a.media.length` | 120 |
| `a.media.playerName` | HTML 5 |
| `a.media.view` | true |
| `a.contentType` | vod |
| `custom.[value]` | Campos de metadados personalizados |
| `a.media.[value]` | Campos de metadados padrão |

**Notas:**

* As variáveis de dados de contexto adicionais devem estar presentes e conter metadados. Veja os detalhes dos metadados abaixo.
* A duração dos fluxos lineares deve ser definida para a melhor estimativa do programa atual.

### Metadados padronizados na chamada de início do Media Analytics

| Parâmetro | Valor (exemplo)  |
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

### Chamada de início do Heartbeat

| Parâmetro | Valor (exemplo)  |
|---|---|
| `s:event:type` | start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | Título do episódio |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |
| `s:meta:custom.[value]` | Campos de metadados personalizados |
| `s:meta:a.media.[value]` | Campos de metadados padrão |

### Metadados de mídia na chamada de início do Media Analytics

| Parâmetro | Valor (exemplo)  |
|---|---|
| `custom.metadataA` | value |
| `custom.metadataB` | value |

**Notas:**

* As variáveis de dados de contexto adicionais devem estar presentes e conter metadados. Veja os detalhes dos metadados abaixo.
* A posição do indicador de reprodução para fluxos lineares no início do vídeo deve ser definida para os segundos decorridos desde o início do programa atual, não 0.

### Chamada de início do Heartbeat Analytics

| Parâmetro | Valor (exemplo)  |
|---|---|
| `s:event:type` | aa_start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | Título do episódio |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

### Metadados de mídia na chamada de início do Heartbeat

| Parâmetro | Valor (exemplo)  |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Metadados padrão na chamada de início do Heartbeat

| Parâmetro | Valor (exemplo)  |
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

**Observações:**

* Essa chamada indica que a biblioteca do heartbeat solicitou o envio de uma chamada de análise pev2=ms_s ao servidor de análises.
* Esta chamada não contém metadados personalizados.

## Exibir a reprodução do anúncio {#section_wz3_yff_f2b}

### Chamada de início de anúncio do Media Analytics

| Parâmetro | Valor (exemplo)  |
|---|---|
| `pev2` | msa_s |
| `a.media.name` | 123456 |
| `a.media.ad.name` | 9378 |
| `a.media.ad.friendlyName` | Video_VPAID_DFA |
| `a.media.ad.podFriendlyName` | pré-rolagem |
| `a.media.ad.length` | 15 |
| `a.media.ad.playerName` | HTML 5 |
| `a.media.ad.pod` | c27aaf3ff8224bb6b9ebfe1b2e79073d_1 |
| `a.media.ad.podPosition` | 1 |
| `a.media.ad.podSecond` | 0.0 |
| `a.media.ad.view` | Verdadeiro |
| `custom.[value]` | Campos de metadados |
| `a.media.[value]` | Campos de metadados padrão |

**Observação:** as variáveis de dados de contexto adicionais devem estar presentes e conter metadados. Veja os detalhes dos metadados abaixo.

### Chamada de início do anúncio do Heartbeat

| Parâmetro | Valor (exemplo)  |
|---|---|
| `s:event:type` | start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:ad_id` | 9378 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | ad |
| `s:meta:custom.[value]` | Campos de metadados personalizados |
| `s:meta:a.media.[value]` | Campos de metadados padrão |

### Metadados de mídia na chamada de início de anúncio do Media Analytics

| Parâmetro | Valor (exemplo)  |
|---|---|
| `custom.metadata` | value |
| `custom.metadata` | value |

### Metadados padronizados na chamada de início de anúncio do Media Analytics

| Parâmetro | Valor (exemplo)  |
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

**Notas:**

* As variáveis de dados de contexto adicionais devem estar presentes e conter metadados. Veja os detalhes dos metadados abaixo.
* A duração do anúncio deverá ser definida para -1, se não estiver disponível no início do anúncio.

### Chamada de início do anúncio do Heartbeat Analytics

| Parâmetro | Valor (exemplo)  |
|---|---|
| `s:event:type` | aa_ad_start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| `s:asset:type` | ad |

### Metadados de mídia na chamada de início do anúncio Heartbeat

| Parâmetro | Valor (exemplo)  |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Metadados padrão na chamada de início do anúncio do Heartbeat

| Parâmetro | Valor (exemplo)  |
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

**Notas:**

* As variáveis de dados de contexto adicionais devem estar presentes e conter metadados. Veja os detalhes dos metadados abaixo.
* A duração do anúncio deverá ser definida para -1, se não estiver disponível no início do anúncio.

### Chamada Heartbeat Ad Complete

| Parâmetro | Valor (exemplo)  |
|---|---|
| `s:event:type` | concluído |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| `s:asset:type` | ad |

### Chamada Heartbeat Ad Play

| Parâmetro | Valor (exemplo)  |
|---|---|
| `s:event:type` | play |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| `s:asset:type` | ad |

## Reproduzir conteúdo principal {#section_u1l_1gf_f2b}

### Chamada Heartbeat Play

| Parâmetro | Valor (exemplo)  |
|---|---|
| `s:event:type` | play |
| `l:event:playhead` | 29 |
| `l:event:duration` | 10189 |
| `s:asset:name` | Título do episódio |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**Notas:**

* A posição do indicador de reprodução deve ser incrementada em 10 com cada chamada de reprodução.
* O valor `l:event:duration` representa o número de milissegundos desde a última chamada de rastreamento e deve ser basicamente o mesmo valor em cada chamada de 10 segundos.

