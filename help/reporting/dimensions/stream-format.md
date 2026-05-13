---
title: Formato do fluxo
description: Relata o nível de qualidade de cada sessão (normalmente HD ou SD).
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 6%

---


# Formato do fluxo

>[!BEGINSHADEBOX]

*Esta página abrange a **Dimensão de relatório do formato de fluxo**. Consulte [Formato do fluxo](/help/implementation/variables/standard-metadata/stream-format.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Formato do fluxo** informa o nível de qualidade de cada sessão (normalmente `"HD"` ou `"SD"`, mas qualquer cadeia de caracteres é aceita). Use-a para comparar o envolvimento, a conclusão e a qualidade entre os níveis de qualidade da entrega.

## Como essa dimensão é preenchida

O formato do fluxo é definido pelo reprodutor no início da sessão.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Crie uma [Regra de processamento](https://experienceleague.adobe.com/pt-br/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.format` para uma eVar. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.streamFormat`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `evar1`-`evar250`, `post_evar1`-`post_evar250` (a eVar para a qual sua regra de processamento mapeia `a.media.format`) |

## Itens de dimensão

Cada item é o valor de formato literal relatado no início da sessão. Use um conjunto estável de valores (`HD`, `SD`, `4K`, `UHD`) para que os itens de linha não se fragmentem em variações de ortografia.
