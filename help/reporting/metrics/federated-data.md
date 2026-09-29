---
title: Dados federados
description: Conta sessões recebidas por meio de um compartilhamento de dados federado em vez da implementação de um cliente.
feature: Metrics
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 6%
---

# Dados federados

>[!AVAILABILITY]
>
>O serviço Federated Analytics está disponível apenas ao usar os recursos de mídia de transmissão com o Adobe Analytics. O Federated Analytics não está disponível no Customer Journey Analytics.

A métrica **Dados federados** conta sessões que foram recebidas por meio de um compartilhamento de dados federado, e não de sua própria implementação. Use-o para medir o volume de sessões compartilhadas com parceiros e comparar o envolvimento, a conclusão ou a qualidade em relação às sessões primárias.

Consulte o caso de uso [Federated Media](/help/use-cases/federated-media.md) para obter mais informações.

>[!TIP]
>
>Se quiser usar dados federados como uma dimensão, crie uma [Regra de processamento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie a variável de dados de contexto `a.media.federated` para uma eVar.

## Como essa métrica é calculada

O back-end de mídia define esse sinalizador quando a sessão é recebida por um canal federado. A métrica é incrementada uma vez por sessão qualificada e é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.federated` quando os [[!UICONTROL Metadados de vídeo]](/help/reporting/setup/analytics-reporting.md) estão habilitados. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isFederated`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.federated` |
