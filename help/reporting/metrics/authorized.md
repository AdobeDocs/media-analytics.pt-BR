---
title: Autorizado
description: Conta sessões cujo usuário foi autorizado por meio do Adobe Pass.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
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
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.authorized`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.pass.auth` |
