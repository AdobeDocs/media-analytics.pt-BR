---
title: Rótulo
description: Relata a gravadora que liberou o conteúdo de áudio.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 10%

---


# Rótulo

>[!BEGINSHADEBOX]

*Esta página cobre a dimensão de relatório **Rótulo**. Consulte [Rótulo](/help/implementation/variables/standard-metadata/label.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Rótulo** informa o rótulo de registro que liberou o conteúdo de áudio (por exemplo, `"Capitol Records"`). Use-o para comparar o engajamento entre rótulos em um catálogo de música ou podcast.

## Como essa dimensão é preenchida

O rótulo é definido pelo reprodutor no início da sessão para o conteúdo de áudio.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.label` quando os [[!UICONTROL Metadados de áudio]](/help/reporting/media-reports-enable.md) estão habilitados. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.label`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videoaudiolabel` |
| Audience Manager | `c_contextdata.a.media.label` |

## Itens de dimensão

Cada item é o nome do rótulo literal relatado no início da sessão. Use um nome estável e canônico por rótulo para que o engajamento não se fragmente pelas variantes de ortografia ou impressão.
