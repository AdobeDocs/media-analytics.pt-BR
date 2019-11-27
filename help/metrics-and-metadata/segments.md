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
| Tipo de fluxo de mídia: todos | Segmentar todos os dados de fluxo de *mídia* | "A ID de conteúdo existe" |
| Tipo de fluxo de mídia: áudio | Segmentar todos os dados de fluxo de *áudio* | "A ID de conteúdo existe" E "Tipo de fluxo de mídia = `audio`" |
| Tipo de fluxo de mídia: vídeo | Segmentar todos os dados de fluxo de *vídeo* | "A ID de conteúdo existe" E "Tipo de fluxo de mídia != `audio`" |
| Tipo de conteúdo de mídia: VoD | Segmentar todo o conteúdo de VoD | "Tipo de conteúdo = `vod`" |
| Tipo de conteúdo de mídia: em tempo real | Segmentar todo o conteúdo em tempo real | "Tipo de conteúdo = `live`" |
| Tipo de conteúdo de mídia: linear | Segmentar todo o conteúdo linear | "Tipo de conteúdo = `linear`" |
| Tipo de conteúdo de mídia: podcast | Segmentar todo o conteúdo de podcast | "Tipo de conteúdo = `podcast`" |
| Tipo de conteúdo de mídia: audiobook | Segmentar todo o conteúdo de audiobook | "Tipo de conteúdo = `audiobook`" |
| Tipo de conteúdo de mídia: AoD | Segmentar todo o conteúdo de AoD | "Tipo de conteúdo = `aod`" |

