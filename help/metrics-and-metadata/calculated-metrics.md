---
title: Métricas calculadas
description: Saiba mais sobre as métricas calculadas e fórmulas de métricas da mídia de transmissão Adobe.
uuid: 9dd35155-58aa-4f05-896e-c5cbc4b13d59
exl-id: 253f6c61-70b5-4bdf-8e79-840545aeca0e
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 78%

---

# Métricas calculadas{#calculated-metrics}

>[!NOTE]
>
>Essas métricas calculadas foram introduzidas em 13/09/2018.

| Métrica | Descrição | Fórmula |
|---|---|---|
| Média de anúncios por transmissão da mídia | Anúncio iniciado por mídia iniciada | `Ad Starts / Media Starts` |
| Média de capítulos por transmissão da mídia | Capítulo iniciado por mídia iniciada | `Chapter Start / Media Starts` |
| Média Tempo gasto com a mídia | Tempo total gasto por mídia iniciada (HH:MM:SS) | `Media Time Spent / Media Starts` |
| Média Tempo gasto no conteúdo | Tempo gasto com conteúdo por inicializações de conteúdo (HH:MM:SS) | `Content Time Spent / Content Start` |
| Média Tempo gasto com anúncio | Tempo gasto no anúncio por Inícios de anúncio (HH:MM:SS) | `Ad Time Spent / Ad Start` |
| Média Tempo gasto com capítulo | Tempo gasto com capítulo por inicializações de capítulo (HH:MM:SS) | `Chapter Time Spent / Chapter Start` |
| Taxa de conclusão da mídia | Taxa de Conclusão de conteúdo vs. Mídia iniciada (%) | `Content Completes/ Media Starts` |
| Taxa de conclusão do conteúdo | Taxa de Conclusão de conteúdo vs. Inícios de conteúdo (%) | `Content Completes / Content Starts` |
| Taxa de conclusão do anúncio | Taxa de Conclusões de anúncio vs. Inícios de anúncio (%) | `Ad Completes / Ad Starts` |
| Taxa de conclusão do capítulo | Taxa de Conclusões de capítulo vs. Inícios de capítulo (%) | `Chapter Completes / Chapter Starts` |
| Taxa de ignoradas antes do início | Taxa de abandono antes de iniciar vs. Inícios da mídia (%) | `Drops before Starts / Media Starts` |
| Taxa de duração da pausa do conteúdo | Taxa de Duração total da pausa vs. Tempo gasto com conteúdo (%) | `Total Pause Duration / Content Time Spent` |
| Taxa de duração do buffer do conteúdo | Taxa de Duração total do buffer vs. Tempo gasto com conteúdo (%) | `Total Buffer Duration / Content Time Spent` |
| Taxa da hora de início do conteúdo | Taxa de Tempo para iniciar vs. Tempo gasto com conteúdo (%) | `Time to Start / Content Time Spent` |
| Taxa de tempo gasto com anúncio | Taxa de Tempo gasto com anúncio vs.Tempo gasto com conteúdo (%) | `Ad Time Spent / Content Time Spent` |
