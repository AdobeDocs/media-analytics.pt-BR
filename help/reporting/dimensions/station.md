---
title: Estação
description: Reporta o nome ou ID da estação de rádio para o conteúdo de difusão de áudio.
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
source-wordcount: '138'
ht-degree: 10%
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
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.station` quando os [[!UICONTROL Metadados de áudio]](/help/reporting/setup/analytics-reporting.md) estão habilitados. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.station`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videoaudiostation` |
| Audience Manager | `c_contextdata.a.media.station` |

## Itens de dimensão

Cada item é o nome literal da estação ou ID reportada no início da sessão. Use um único identificador canônico por estação para que o engajamento não se fragmente entre as variantes de sinal de chamada.
