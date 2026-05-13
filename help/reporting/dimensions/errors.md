---
title: Erros
description: Relata a contagem de eventos de erro por sessão.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 6%

---


# Erros

>[!BEGINSHADEBOX]

*Esta página abrange a dimensão **Erros**. O Adobe Analytics preenche automaticamente uma [métrica de eventos de erro](/help/reporting/metrics/error-events.md) emparelhada a partir da mesma variável de dados de contexto `a.media.qoe.errorCount`. O Customer Journey Analytics expõe um único campo `mediaReporting.qoeDataDetails.errorCount` que você pode usar como dimensão ou métrica.*

>[!ENDSHADEBOX]

A dimensão **Erros** relata a contagem de eventos de erro recebidos durante uma sessão. Use a dimensão para dividir o engajamento por contagem exata de erros.

## Como essa dimensão é preenchida

O back-end de mídia incrementa a contagem em cada erro relatado pelo reprodutor. O valor é relatado na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.qoe.errorCount` quando a [[!UICONTROL Qualidade de Mídia]](/help/reporting/media-reports-enable.md) está habilitada. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.errorCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feeds de dados | `videoqoeerrorcountevar, post_videoqoeerrorcountevar` |

## Itens de dimensão

Cada item é o valor literal de contagem de erros relatado na chamada de fechamento. Para relatórios booleanos em nível de sessão (se algum erro ocorreu), use [Fluxos afetados por erros](/help/reporting/metrics/error-impacted-streams.md). Para identificadores de erro exclusivos, use as [Identificações de erro externo](external-error-ids.md) e as [Identificações de erro do Player SDK](player-sdk-error-ids.md).
