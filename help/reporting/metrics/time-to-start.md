---
title: Hora de início (métrica)
description: Tempo de inicialização de relatórios para somas e médias entre sessões.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 7%

---


# Hora de início (métrica)

>[!BEGINSHADEBOX]

*Esta página aborda a métrica **Hora de início**. O Adobe Analytics preenche automaticamente uma [Hora de início (dimensão)](/help/reporting/dimensions/time-to-start.md) emparelhada a partir da mesma variável de dados de contexto `a.media.qoe.timeToStart`. O Customer Journey Analytics expõe um único campo `xdm.mediaReporting.qoeDataDetails.timeToStart` que você pode usar como dimensão ou métrica. Consulte [Hora de início](/help/implementation/variables/quality/time-to-start.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A métrica **Tempo para iniciar** relata o tempo de inicialização entre sessões, adequado para somas, médias e acúmulos de percentil. Use a métrica para calcular o tempo médio de inicialização em um período de relatório e comparar o desempenho de inicialização em conteúdo, redes ou players. O Adobe armazena o valor em segundos e converte na assimilação a partir dos milissegundos relatados pelo reprodutor.

## Como essa métrica é calculada

O reprodutor define `timeToStart` no objeto de QoE antes do acionamento da sessão. O backend relata o valor na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.qoe.timeToStart` quando a [[!UICONTROL Qualidade de Mídia]](/help/reporting/setup/analytics-reporting.md) está habilitada. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.timeToStart` |
