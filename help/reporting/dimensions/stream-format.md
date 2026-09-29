---
title: Formato do fluxo
description: Relata o nível de qualidade de cada sessão (normalmente HD ou SD).
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
source-wordcount: '168'
ht-degree: 7%
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
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.streamFormat`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `evar1`-`evar250`, `post_evar1`-`post_evar250` (a eVar para a qual sua regra de processamento mapeia `a.media.format`) |
| Audience Manager | `c_contextdata.a.media.format` |

## Itens de dimensão

Cada item é o valor de formato literal relatado no início da sessão. Use um conjunto estável de valores (`HD`, `SD`, `4K`, `UHD`) para que os itens de linha não se fragmentem em variações de ortografia.
