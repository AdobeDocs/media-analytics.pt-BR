---
title: Rede
description: Reporta a rede de transmissão ou o nome do canal.
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
source-wordcount: '127'
ht-degree: 12%
---

# Rede

>[!BEGINSHADEBOX]

*Esta página cobre a dimensão de relatório **Rede**. Consulte [Rede](/help/implementation/variables/standard-metadata/network.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Rede** informa o nome da rede de difusão ou do canal (por exemplo, `"Fox"` ou `"ESPN"`). Use-a para comparar o engajamento em redes na mesma propriedade de streaming.

## Como essa dimensão é preenchida

A rede é definida pelo reprodutor no início da sessão.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.network` quando os [[!UICONTROL Metadados de vídeo]](/help/reporting/setup/analytics-reporting.md) estão habilitados. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.network`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videonetwork`, `post_videonetwork` |
| Audience Manager | `c_contextdata.a.media.network` |

## Itens de dimensão

Cada item é o valor de rede literal relatado no início da sessão. Use um nome estável e distinto por rede para que os dados não se fragmentem em variantes de ortografia.
