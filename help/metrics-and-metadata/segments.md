---
title: Segmentos
description: '"Saiba mais sobre os segmentos de relatórios associados ao Tipo de fluxo de mídia, incluindo o Segmento, a Descrição e a Regra para o Tipo de fluxo de mídia."'
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
exl-id: a450801c-0d6b-4e2a-8662-f00aaaa6e4e0
feature: '"Media Analytics, Segmentação"'
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 84%

---

# Segmentos{#segments}

>[!NOTE]
>
>Esses segmentos de relatórios associados ao Tipo de fluxo de mídia foram introduzidos em 13/9/2018, juntamente com o parâmetro `streamType`.

| Segmento | Descrição | Regra |
|---|---|---|
| Tipo de transmissão da mídia: Tudo | Segmentar todos os dados de fluxo de *mídia* | &quot;Conteúdo (ID) existe&quot; |
| Tipo de transmissão da mídia: Áudio | Segmentar todos os dados de fluxo de *áudio* | &quot;A ID de conteúdo existe&quot; E &quot;Tipo de fluxo de mídia = `audio`&quot; |
| Tipo de transmissão da mídia: Vídeo | Segmentar todos os dados de fluxo de *vídeo* | &quot;A ID de conteúdo existe&quot; E &quot;Tipo de fluxo de mídia != `audio`&quot; |
| Tipo de conteúdo da mídia: VoD | Segmentar todo o conteúdo de VoD | &quot;Tipo de conteúdo = `vod`&quot; |
| Tipo de conteúdo da mídia: Em tempo real | Segmentar todo o conteúdo ao vivo | &quot;Tipo de conteúdo = `live`&quot; |
| Tipo de conteúdo da mídia: Linear | Segmentar todo o conteúdo linear | &quot;Tipo de conteúdo = `linear`&quot; |
| Tipo de conteúdo da mídia: Podcast | Segmentar todo o conteúdo de podcast | &quot;Tipo de conteúdo = `podcast`&quot; |
| Tipo de conteúdo da mídia: Áudiolivro | Segmentar todo o conteúdo de audiobook | &quot;Tipo de conteúdo = `audiobook`&quot; |
| Tipo de conteúdo da mídia: AoD | Segmentar todo o conteúdo de AoD | &quot;Tipo de conteúdo = `aod`&quot; |
