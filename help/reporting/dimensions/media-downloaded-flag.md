---
title: Mídia baixada
description: Sinaliza as sessões que reproduziram o conteúdo baixado offline.
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
source-wordcount: '195'
ht-degree: 7%
---

# Mídia baixada

>[!BEGINSHADEBOX]

*Esta página abrange a dimensão de relatório **Mídia baixada**. Consulte [Sinalizador de mídia baixada](/help/implementation/variables/core/media-downloaded-flag.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Mídia baixada** sinaliza as sessões que reproduziram conteúdo offline baixado anteriormente em vez de um stream ao vivo da Internet. Use-a para separar a reprodução offline das sessões transmitidas ao comparar engajamento, conclusão ou qualidade.

## Como essa dimensão é preenchida

O sinalizador baixado é definido pelo reprodutor de uma das três formas a seguir. Inicialize o rastreador com o sinalizador (Mobile SDK), envie o `sessionStart` para a variante de ponto de extremidade `/downloaded` (API direta do Media Edge) ou inclua `media.downloaded: true` nos parâmetros `sessionStart` (API da coleção de mídia).

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Crie uma [Regra de processamento](https://experienceleague.adobe.com/pt-br/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.downloaded` para uma eVar. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isDownloaded`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `evar1`-`evar250`, `post_evar1`-`post_evar250` (a eVar para a qual sua regra de processamento mapeia `a.media.downloaded`) |
| Audience Manager | `c_contextdata.a.media.downloaded` |

## Itens de dimensão

| Valor | Descrição |
| --- | --- |
| `true` | A sessão reproduzida com o conteúdo baixado offline. |
| (vazio) | A sessão reproduzia um stream ao vivo. O campo foi omitido em vez de ser definido como `false`. |
