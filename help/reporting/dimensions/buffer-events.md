---
title: Eventos de buffer (dimensão)
description: Relata a contagem de eventos de buffer por sessão.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 6%

---


# Eventos de buffer (dimensão)

>[!BEGINSHADEBOX]

*Esta página abrange a dimensão **Eventos de buffer**. O Adobe Analytics preenche automaticamente um par de [Eventos de buffer (métrica)](/help/reporting/metrics/buffer-events.md) da mesma variável de dados de contexto `a.media.qoe.bufferCount`. O Customer Journey Analytics expõe um único campo `xdm.mediaReporting.qoeDataDetails.bufferCount` que você pode usar como dimensão ou métrica.*

>[!ENDSHADEBOX]

A dimensão **Eventos de buffer** relata a contagem de eventos de buffer que ocorreram durante uma sessão. Use a dimensão para dividir o engajamento por contagem exata de buffer.

## Como essa dimensão é preenchida

O back-end de mídia incrementa a contagem toda vez que o player entra em um estado `buffer`. O valor é relatado na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.qoe.bufferCount` quando a [[!UICONTROL Qualidade de Mídia]](/help/reporting/media-reports-enable.md) está habilitada. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bufferCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feeds de dados | `videoqoebuffercountevar`, `post_videoqoebuffercountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bufferCount` |

## Itens de dimensão

Cada item é o valor literal de contagem de buffer relatado na chamada de fechamento. Para relatórios booleanos em nível de sessão (se a sessão passou por algum buffer), use [Fluxos afetados pelo buffer](/help/reporting/metrics/buffer-impacted-streams.md).
