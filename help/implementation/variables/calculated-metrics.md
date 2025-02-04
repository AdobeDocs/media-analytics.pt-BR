---
title: 'Métricas calculadas '
description: Saiba mais sobre métricas calculadas e fórmulas de métricas na Coleção de mídia de transmissão.
uuid: 9dd35155-58aa-4f05-896e-c5cbc4b13d59
exl-id: 253f6c61-70b5-4bdf-8e79-840545aeca0e
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 72%

---

# Métricas calculadas{#calculated-metrics}

As métricas calculadas para a Coleção de mídia de transmissão do Adobe são métricas personalizadas que permitem obter dados de mídia de transmissão direcionados, como o tempo médio de anúncio gasto ou anúncios médios por fluxo de mídia.

Para obter informações sobre métricas calculadas do Adobe Analytics, consulte [Métricas calculadas e calculadas avançadas (derivadas)](https://experienceleague.adobe.com/docs/analytics/components/calculated-metrics/cm-overview.html?lang=pt-BR) no Guia de componentes do Adobe Analytics.

>[!NOTE]
>
>Essas métricas calculadas foram introduzidas em 13/09/2018.

| Métrica | Descrição | Fórmula |
|---|---|---|
| Média de anúncios por transmissão da mídia | Anúncio iniciado por mídia iniciada | `Ad Starts / Media Starts` |
| Média de capítulos por transmissão da mídia | Capítulo iniciado por mídia iniciada | `Chapter Start / Media Starts` |
| Média Tempo gasto com a mídia | Tempo Total Gasto por Inicializações de Mídia (`HH:MM:SS`) | `Media Time Spent / Media Starts` |
| Média Tempo gasto no conteúdo | Tempo gasto no conteúdo por inicializações do conteúdo (`HH:MM:SS`) | `Content Time Spent / Content Start` |
| Média Tempo gasto com anúncio | Tempo gasto no anúncio por inicializações de anúncio (`HH:MM:SS`) | `Ad Time Spent / Ad Start` |
| Média Tempo gasto com capítulo | Tempo gasto com capítulo por inicializações de capítulo (`HH:MM:SS`) | `Chapter Time Spent / Chapter Start` |
| Taxa de conclusão da mídia | Taxa de Conclusão de conteúdo vs. Mídia iniciada (%) | `Content Completes/ Media Starts` |
| Taxa de conclusão do conteúdo | Taxa de Conclusão de conteúdo vs. Inícios de conteúdo (%) | `Content Completes / Content Starts` |
| Taxa de conclusão do anúncio | Taxa de Conclusões de anúncio vs. Inícios de anúncio (%) | `Ad Completes / Ad Starts` |
| Taxa de conclusão do capítulo | Taxa de Conclusões de capítulo vs. Inícios de capítulo (%) | `Chapter Completes / Chapter Starts` |
| Taxa de ignoradas antes do início | Taxa de abandono antes de iniciar vs. Inícios da mídia (%) | `Drops before Starts / Media Starts` |
| Taxa de duração da pausa do conteúdo | Taxa de Duração total da pausa vs. Tempo gasto com conteúdo (%) | `Total Pause Duration / Content Time Spent` |
| Taxa de duração do buffer do conteúdo | Taxa de Duração total do buffer vs. Tempo gasto com conteúdo (%) | `Total Buffer Duration / Content Time Spent` |
| Taxa da hora de início do conteúdo | Taxa de Tempo para iniciar vs. Tempo gasto com conteúdo (%) | `Time to Start / Content Time Spent` |
| Taxa de tempo gasto com anúncio | Taxa de Tempo gasto com anúncio vs.Tempo gasto com conteúdo (%) | `Ad Time Spent / Content Time Spent` |
