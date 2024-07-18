---
title: Explicação dos segmentos de transmissão de mídia
description: “Saiba mais sobre os segmentos de relatórios associados ao tipo de fluxo de mídia, incluindo o Segmento, a Descrição e a Regra do Tipo de fluxo de mídia.”
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
exl-id: a450801c-0d6b-4e2a-8662-f00aaaa6e4e0
feature: "Media Analytics, Segmentation"
role: User, Admin, Data Engineer
source-git-commit: b15a81dc8f08e94c9b80d66019f3d0fe95ef5a74
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 100%

---

# Segmentos de mídia{#segments}

Os segmentos permitem que você identifique subconjuntos de visitantes com base em características ou interações de site. Os segmentos de mídia de transmissão permitem identificar o tipo de fluxo do visitante, como fluxos de áudio, ao vivo ou podcast. Para obter informações sobre segmentos do Adobe Analytics, consulte [Sobre segmentos e containers](https://experienceleague.adobe.com/docs/analytics/components/segmentation/seg-overview.html?lang=pt-BR) no Guia de componentes do Adobe Analytics.

>[!NOTE]
>
>Esses segmentos de relatórios associados ao Tipo de fluxo de mídia foram introduzidos em 13/9/2018, juntamente com o parâmetro `streamType`.

| Segmento | Descrição | Regra |
|---|---|---|
| Tipo de transmissão da mídia: Tudo | Segmentar todos os dados de fluxo de *mídia* | “Conteúdo (ID) existe” |
| Tipo de transmissão da mídia: Áudio | Segmentar todos os dados de fluxo de *áudio* | “Conteúdo (ID) existe” E “Tipo de fluxo de mídia = `audio`” |
| Tipo de transmissão da mídia: Vídeo | Segmentar todos os dados de fluxo de *vídeo* | “Conteúdo (ID) existe” E “Tipo de fluxo de mídia != `audio`” |
| Tipo de conteúdo da mídia: VoD | Segmentar todo o conteúdo de VoD | “Tipo de conteúdo = `vod`” |
| Tipo de conteúdo da mídia: Em tempo real | Segmentar todo o conteúdo ao vivo | “Tipo de conteúdo = `live`” |
| Tipo de conteúdo da mídia: Linear | Segmentar todo o conteúdo linear | “Tipo de conteúdo = `linear`” |
| Tipo de conteúdo da mídia: Podcast | Segmentar todo o conteúdo de podcast | “Tipo de conteúdo = `podcast`” |
| Tipo de conteúdo da mídia: Áudiolivro | Segmentar todo o conteúdo de audiobook | “Tipo de conteúdo = `audiobook`” |
| Tipo de conteúdo da mídia: AoD | Segmentar todo o conteúdo de AoD | “Tipo de conteúdo = `aod`” |
