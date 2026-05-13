---
title: Estação
description: Reporta o nome ou ID da estação de rádio para o conteúdo de difusão de áudio.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 8%

---


# Estação

>[!BEGINSHADEBOX]

*Esta página cobre a dimensão de relatório **Estação**. Consulte [Estação](/help/implementation/variables/standard-metadata/station.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Estação** informa o nome ou a ID da estação de rádio que está transmitindo o conteúdo de áudio (por exemplo, `"NPR"` ou `"WXYZ-FM"`). Use-o para comparar o engajamento entre estações em uma rede sindicalizada.

## Como essa dimensão é preenchida

A estação é definida pelo reprodutor no início da sessão para conteúdo de áudio.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.station` quando os [[!UICONTROL Metadados de áudio]](/help/reporting/media-reports-enable.md) estão habilitados. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.station`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videoaudiostation` |

## Itens de dimensão

Cada item é o nome literal da estação ou ID reportada no início da sessão. Use um único identificador canônico por estação para que o engajamento não se fragmente entre as variantes de sinal de chamada.
