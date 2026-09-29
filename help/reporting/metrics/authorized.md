---
title: Autorizado
description: Conta sessões cujo usuário foi autorizado por meio do Adobe Pass.
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
source-wordcount: '137'
ht-degree: 12%
---

# Autorizado

>[!BEGINSHADEBOX]

*Esta página abrange a métrica de relatórios **Autorizada**. Consulte [Autorizado](/help/implementation/variables/standard-metadata/authorized.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A métrica **Autorizada** conta sessões cujo usuário foi autorizado por meio do Adobe Pass ou da TV-Everywhere. Emparelhe com a dimensão [MVPD](/help/reporting/dimensions/mvpd.md) para dividir o volume de autenticação por provedor.

## Como essa métrica é calculada

O back-end de mídia incrementa a contagem quando o reprodutor sinaliza a sessão como autorizada no início da sessão. A métrica é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.pass.auth` quando os [[!UICONTROL Metadados de vídeo]](/help/reporting/setup/analytics-reporting.md) estão habilitados. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.authorized`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.pass.auth` |
