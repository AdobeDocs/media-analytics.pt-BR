---
title: Explicação dos segmentos de transmissão de mídia
description: '"Saiba mais sobre os segmentos de relatórios associados ao Tipo de fluxo de mídia, incluindo o Segmento, a Descrição e a Regra para o Tipo de fluxo de mídia."'
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
exl-id: a450801c-0d6b-4e2a-8662-f00aaaa6e4e0
feature: '"Media Analytics, Segmentação"'
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 66%

---

# Segmentos{#segments}

Os segmentos permitem que você identifique subconjuntos de visitantes com base em características ou interações de site. Segmentos de mídia de transmissão permitem identificar o tipo de fluxo de visitante, como fluxos de áudio, ao vivo ou podcast. Para obter informações sobre segmentos do Adobe Analytics, consulte [Sobre segmentos e contêineres](https://experienceleague.adobe.com/docs/analytics/components/segmentation/seg-overview.html?lang=en) no Guia de componentes do Adobe Analytics.

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
