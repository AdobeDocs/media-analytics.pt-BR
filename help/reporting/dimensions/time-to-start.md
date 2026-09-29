---
title: Hora de início (dimensão)
description: Relata o tempo decorrido antes da renderização do primeiro quadro.
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 7%
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
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.qoe.timeToStart` quando a [[!UICONTROL Qualidade de Mídia]](/help/reporting/setup/analytics-reporting.md) está habilitada. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feeds de dados | `videoqoetimetostartevar`, `post_videoqoetimetostartevar` |
| Audience Manager | `c_contextdata.a.media.qoe.timeToStart` |

## Itens de dimensão

Cada item é o valor literal de tempo de inicialização relatado na chamada de fechamento.
