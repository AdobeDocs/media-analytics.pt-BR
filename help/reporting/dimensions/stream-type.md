---
title: Tipo de transmissão
description: Registra se cada sessão de mídia era conteúdo de áudio ou vídeo.
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
source-wordcount: '322'
ht-degree: 6%
---

# Tipo de transmissão

>[!BEGINSHADEBOX]

*Esta página abrange a **Tipo de fluxo**&#x200B;dimensão de relatório. Consulte [Tipo de fluxo](/help/implementation/variables/core/stream-type.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Tipo de fluxo** captura se cada sessão de mídia foi conteúdo de áudio ou vídeo. Ele fica disponível na Adobe Analytics uma vez que o [Media Core é habilitado](/help/reporting/setup/analytics-reporting.md) para o conjunto de relatórios e no Customer Journey Analytics para qualquer conjunto de dados que inclua dados de mídia de streaming.

## Como essa dimensão é preenchida

O tipo de fluxo é definido pelo reprodutor no início da sessão e transportado até a chamada de fechamento da sessão. Não é calculado nem derivado. O valor relatado corresponde exatamente ao que foi enviado durante a coleta.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.streamType` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.streamType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videostreamtype` |
| Audience Manager | `c_contextdata.a.media.streamType` |

>[!IMPORTANT]
>
>Se o tipo de fluxo não estiver definido, a dimensão não será preenchida para essa sessão. Essas sessões são excluídas dos segmentos integrados Somente áudio e Somente vídeo, e o segmento Todas as mídias de transmissão será subcontabilizado se usado em conjunto com detalhamentos do tipo de fluxo.

## Itens de dimensão

| Valor | Descrição |
| --- | --- |
| `video` | A sessão era conteúdo em vídeo. |
| `audio` | A sessão era conteúdo de áudio, como um podcast, audiobook ou fluxo de música. |

Tecnicamente, valores personalizados são aceitos pelas APIs de coleção, mas não são recomendados. Eles não corresponderão aos segmentos integrados descritos abaixo e podem causar relatórios inconsistentes em implementações.

## Segmentos recomendados

O tipo de fluxo é a base para os segmentos [!UICONTROL Tipo de Fluxo de Mídia] internos do Adobe Analytics. Use estes segmentos para determinar o escopo de qualquer relatório de mídia de transmissão para um tipo de conteúdo específico:

| Segmento | Regra |
| --- | --- |
| [!UICONTROL Todas as mídias de streaming] | O conteúdo (ID) existe |
| [!UICONTROL Somente áudio] | Conteúdo (ID) existe E Tipo de Fluxo = `audio` |
| [!UICONTROL Somente vídeo] | Existe conteúdo (ID) E tipo de fluxo != `audio` |

>[!TIP]
>
>O segmento [!UICONTROL Somente vídeo] usa uma regra `!=` em vez de `= video` para capturar corretamente as sessões em que o tipo de fluxo pode ter sido definido como um valor personalizado que não é `audio`.
