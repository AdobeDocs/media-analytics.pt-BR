---
title: Segmentos
description: null
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Segmentos {#segments}

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

