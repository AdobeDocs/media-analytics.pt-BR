---
title: Hora de início (dimensão)
description: Relata o tempo decorrido antes da renderização do primeiro quadro.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 6%

---


# Hora de início (dimensão)

>[!BEGINSHADEBOX]

*Esta página aborda a dimensão **Hora de início**. O Adobe Analytics preenche automaticamente uma [Hora de início (métrica)](/help/reporting/metrics/time-to-start.md) emparelhada a partir da mesma variável de dados de contexto `a.media.qoe.timeToStart`. O Customer Journey Analytics expõe um único campo `xdm.mediaReporting.qoeDataDetails.timeToStart` que você pode usar como dimensão ou métrica. Consulte [Hora de início](/help/implementation/variables/quality/time-to-start.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Tempo para iniciar** relata o tempo decorrido entre o início da sessão e a renderização do primeiro quadro. Use a dimensão para dividir o envolvimento por classificação de tempo de inicialização. O Adobe armazena o valor em segundos e converte na assimilação a partir dos milissegundos relatados pelo reprodutor.

## Como essa dimensão é preenchida

O reprodutor define `timeToStart` no objeto de QoE antes do acionamento da sessão. O backend relata o valor na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.qoe.timeToStart` quando a [[!UICONTROL Qualidade de Mídia]](/help/reporting/media-reports-enable.md) está habilitada. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feeds de dados | `videoqoetimetostartevar`, `post_videoqoetimetostartevar` |
| Audience Manager | `c_contextdata.a.media.qoe.timeToStart` |

## Itens de dimensão

Cada item é o valor literal de tempo de inicialização relatado na chamada de fechamento.
