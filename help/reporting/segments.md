---
title: Explicação dos segmentos de transmissão de mídia
description: Saiba mais sobre os segmentos de relatórios associados ao Tipo de fluxo de mídia, incluindo o Segmento, a Descrição e a Regra do Tipo de fluxo de mídia.
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
exl-id: a450801c-0d6b-4e2a-8662-f00aaaa6e4e0
feature: Streaming Media, Segmentation
role: User, Admin, Developer
TQID: 'https://experienceleague.adobe.com/7RwJQtw-jHlMMV1yc80lUyEYIwIxR-3oh7vN04cPcRg'
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
    internal-label: Reports
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
    internal-label: API
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
  - id: c47a19a5-f47b-4e53-afe0-e230da195ebe
    internal-label: Segmentation
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 75%
---
# Segmentos de mídia de transmissão

Os segmentos permitem que você identifique subconjuntos de visitantes com base em características ou interações de site. Os segmentos de mídia de transmissão permitem identificar o tipo de fluxo do visitante, como fluxos de áudio, ao vivo ou podcast. Para obter informações sobre segmentos do Adobe Analytics, consulte [Sobre segmentos](https://experienceleague.adobe.com/pt-br/docs/analytics/components/segmentation/seg-overview) no Guia de componentes do Adobe Analytics.

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
