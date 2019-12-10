---
title: Métricas calculadas
description: null
uuid: 9dd35155-58aa-4f05-896e-c5cbc4b13d59
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Métricas calculadas {#calculated-metrics}

>[!NOTE]
>
>Essas métricas calculadas foram introduzidas em 13/09/2018.

| Métrica | Descrição | Fórmula |
|---|---|---|
| Média Anúncios por fluxo de mídia | Anúncio iniciado por mídia iniciada | `Ad Starts / Media Starts` |
| Média Capítulos por fluxo de mídia | Capítulo iniciado por mídia iniciada | `Chapter Start / Media Starts` |
| Média Tempo gasto com a mídia | Tempo total gasto por mídia iniciada (HH:MM:SS) | `Media Time Spent / Media Starts` |
| Média Tempo gasto no conteúdo | Tempo gasto com conteúdo por Inícios de conteúdo (HH:MM:SS) | `Content Time Spent / Content Start` |
| Média Tempo gasto com anúncio | Tempo gasto no anúncio por Inícios de anúncio (HH:MM:SS) | `Ad Time Spent / Ad Start` |
| Média Tempo gasto com capítulo | Tempo gasto com capítulo por Inícios de capítulo (HH:MM:SS) | `Chapter Time Spent / Chapter Start` |
| Taxa de conclusão de mídia | Taxa de Conclusão de conteúdo vs. Mídia iniciada (%) | `Content Completes/ Media Starts` |
| Taxa de conclusão de conteúdo | Taxa de Conclusão de conteúdo vs. Inícios de conteúdo (%) | `Content Completes / Content Starts` |
| Taxa de conclusão de anúncio | Taxa de Conclusões de anúncio vs. Inícios de anúncio (%) | `Ad Completes / Ad Starts` |
| Taxa de conclusão de capítulo | Taxa de Conclusões de capítulo vs. Inícios de capítulo (%) | `Chapter Completes / Chapter Starts` |
| Taxa de ignoradas antes do início | Taxa de abandono antes de iniciar vs. Inícios da mídia (%) | `Drops before Starts / Media Starts` |
| Taxa de duração da pausa do conteúdo | Taxa de Duração total da pausa vs. Tempo gasto com conteúdo (%) | `Total Pause Duration / Content Time Spent` |
| Taxa de duração do buffer de conteúdo | Taxa de Duração total do buffer vs. Tempo gasto com conteúdo (%) | `Total Buffer Duration / Content Time Spent` |
| Taxa de tempo para iniciar conteúdo | Taxa de Tempo para iniciar vs. Tempo gasto com conteúdo (%) | `Time to Start / Content Time Spent` |
| Taxa de tempo gasto no anúncio | Taxa de Tempo gasto com anúncio vs.Tempo gasto com conteúdo (%) | `Ad Time Spent / Content Time Spent` |
