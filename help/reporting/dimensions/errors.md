---
title: Erros
description: Relata a contagem de eventos de erro por sessão.
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
source-wordcount: '235'
ht-degree: 6%
---

# Erros

>[!BEGINSHADEBOX]

*Esta página abrange a dimensão **Erros**. O Adobe Analytics preenche automaticamente uma [métrica de eventos de erro](/help/reporting/metrics/error-events.md) emparelhada a partir da mesma variável de dados de contexto `a.media.qoe.errorCount`. O Customer Journey Analytics expõe um único campo `xdm.mediaReporting.qoeDataDetails.errorCount` que você pode usar como dimensão ou métrica.*

>[!ENDSHADEBOX]

A dimensão **Erros** relata a contagem de eventos de erro recebidos durante uma sessão. Use a dimensão para dividir o engajamento por contagem exata de erros.

## Como essa dimensão é preenchida

O back-end de mídia incrementa a contagem em cada erro relatado pelo reprodutor. O valor é relatado na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.qoe.errorCount` quando a [[!UICONTROL Qualidade de Mídia]](/help/reporting/setup/analytics-reporting.md) está habilitada. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.errorCount`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feeds de dados | `videoqoeerrorcountevar`, `post_videoqoeerrorcountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.errorCount` |

## Itens de dimensão

Cada item é o valor literal de contagem de erros relatado na chamada de fechamento. Para relatórios booleanos em nível de sessão (se algum erro ocorreu), use [Fluxos afetados por erros](/help/reporting/metrics/error-impacted-streams.md). Para identificadores de erro exclusivos, use as [Identificações de erro externo](external-error-ids.md) e as [Identificações de erro do Player SDK](player-sdk-error-ids.md).

>[!NOTE]
>
>Se você usa o Heartbeat SDK herdado (Media SDK 1.5.x-2.x), as IDs de erro geradas internamente pelo SDK são automaticamente coletadas na chave de dados de contexto `a.media.qoe.mediaSdkErrors` e acessíveis no Adobe Analytics por meio de uma regra de processamento personalizada. A característica do Audience Manager é `c_contextdata.a.media.qoe.mediaSdkErrors`. Esse campo não se aplica às implementações da API Media Collection ou da API Media Edge.
