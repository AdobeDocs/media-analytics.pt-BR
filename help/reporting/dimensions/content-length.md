---
title: Extensão do conteúdo
description: Informa a duração total em segundos de cada sessão de mídia conforme definido no início da sessão.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 6%

---


# Extensão do conteúdo

>[!BEGINSHADEBOX]

*Esta página abrange a **Duração do conteúdo**dimensão de relatório. Consulte [Duração do conteúdo](/help/implementation/variables/core/content-length.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Duração do conteúdo** informa a duração total em segundos de cada sessão de mídia conforme definido no início da sessão. Ela habilita métricas de back-end, incluindo [marcadores de progresso](/help/reporting/metrics/progress-markers.md) e [Público-alvo médio por minuto](/help/reporting/metrics/average-minute-audience.md).

## Como essa dimensão é preenchida

A duração do conteúdo é definida pelo reprodutor no início da sessão. O valor relatado é a duração total do ativo em segundos, não o indicador de reprodução decorrido.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.length` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.length`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videolength`, `post_videolength` |
| Audience Manager | `c_contextdata.a.media.length` |

>[!NOTE]
>
>No Adobe Analytics, esse valor também corresponde a uma classificação de **Duração do vídeo** na dimensão [Conteúdo](content.md). Você é responsável por preencher e manter essa classificação separadamente. O Customer Journey Analytics usa essa dimensão diretamente. Você pode usar a [Classificação de valores](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/value-bucketing), se desejar.

>[!IMPORTANT]
>
>Se a duração do conteúdo não for definida ou não for maior que zero, os marcadores de progresso e o Público médio por minuto não serão produzidos para essa sessão. Para fluxos ao vivo com duração desconhecida, defina `86400`.

## Itens de dimensão

Cada item é o valor de comprimento literal, em segundos, relatado no início da sessão.
