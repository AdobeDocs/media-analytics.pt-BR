---
title: Hora de início (dimensão)
description: Relata o tempo decorrido antes da renderização do primeiro quadro.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 5%

---


# Hora de início (dimensão)

>[!BEGINSHADEBOX]

*Esta página aborda a dimensão **Hora de início**. O Adobe Analytics preenche automaticamente uma [Hora de início (métrica)](/help/reporting/metrics/time-to-start.md) emparelhada a partir da mesma variável de dados de contexto `a.media.qoe.timeToStart`. O Customer Journey Analytics expõe um único campo `mediaReporting.qoeDataDetails.timeToStart` que você pode usar como dimensão ou métrica. Consulte [Hora de início](/help/implementation/variables/quality/time-to-start.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Tempo para iniciar** relata o tempo decorrido entre o início da sessão e a renderização do primeiro quadro. Use a dimensão para dividir o envolvimento por classificação de tempo de inicialização. O Adobe armazena o valor em segundos e converte na assimilação a partir dos milissegundos relatados pelo reprodutor.

## Como essa dimensão é preenchida

O reprodutor define `timeToStart` no objeto de QoE antes do acionamento da sessão. O backend relata o valor na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.qoe.timeToStart` quando a [[!UICONTROL Qualidade de Mídia]](/help/reporting/media-reports-enable.md) está habilitada. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feeds de dados | `videoqoetimetostartevar, post_videoqoetimetostartevar` |

## Itens de dimensão

Cada item é o valor literal de tempo de inicialização relatado na chamada de fechamento.
