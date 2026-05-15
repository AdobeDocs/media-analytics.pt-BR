---
title: Alterações na taxa de bits (dimensão)
description: Relata a contagem de eventos de alteração da taxa de bits por sessão.
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 5%

---


# Alterações na taxa de bits (dimensão)

>[!BEGINSHADEBOX]

*Esta página aborda a dimensão **Alterações na taxa de bits**. O Adobe Analytics preenche automaticamente um par de [alterações na taxa de bits (métrica)](/help/reporting/metrics/bitrate-changes.md) da mesma variável de dados de contexto `a.media.qoe.bitrateChangeCount`. O Customer Journey Analytics expõe um único campo `mediaReporting.qoeDataDetails.bitrateChangeCount` que você pode usar como dimensão ou métrica. Consulte [Alteração na taxa de bits](/help/implementation/variables/quality/bitrate-change.md) para saber como acionar eventos de alteração na taxa de bits.*

>[!ENDSHADEBOX]

A dimensão **Alterações na taxa de bits** informa a contagem de eventos de alteração na taxa de bits que ocorreram durante uma sessão. Use a dimensão para dividir o engajamento e a qualidade pelo valor exato da contagem de alterações (por exemplo, &quot;sessões com alterações de taxa de bits 3 versus sessões com 0&quot;).

## Como essa dimensão é preenchida

O back-end de mídia incrementa a contagem em cada evento de [alteração de taxa de bits](/help/implementation/events/playback/bitrate-change.md) recebido durante a sessão. O valor é relatado na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.qoe.bitrateChangeCount` quando a [[!UICONTROL Qualidade de Mídia]](/help/reporting/media-reports-enable.md) está habilitada. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bitrateChangeCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feeds de dados | `videoqoebitratechangecountevar`, `post_videoqoebitratechangecountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateChangeCount` |

## Itens de dimensão

Cada item é o valor literal de contagem de alterações relatado na chamada de fechamento. Para relatórios booleanos em nível de sessão (se a sessão sofreu alguma alteração na taxa de bits), use [Fluxos afetados pela alteração na taxa de bits](/help/reporting/metrics/bitrate-change-impacted-streams.md).
