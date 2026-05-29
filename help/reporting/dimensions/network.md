---
title: Rede
description: Reporta a rede de transmissão ou o nome do canal.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 11%

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
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.network` quando os [[!UICONTROL Metadados de vídeo]](/help/reporting/media-reports-enable.md) estão habilitados. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.network`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videonetwork`, `post_videonetwork` |
| Audience Manager | `c_contextdata.a.media.network` |

## Itens de dimensão

Cada item é o valor de rede literal relatado no início da sessão. Use um nome estável e distinto por rede para que os dados não se fragmentem em variantes de ortografia.
