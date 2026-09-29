---
title: MVPD
description: Informa o cabo, satélite ou provedor virtual pelo qual o usuário se autenticou.
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
source-wordcount: '150'
ht-degree: 10%
---

# MVPD

>[!BEGINSHADEBOX]

*Esta página cobre a dimensão de relatório **MVPD**. Consulte [MVPD](/help/implementation/variables/standard-metadata/mvpd.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **MVPD** (distribuidor de programação de vídeo multicanal) informa o provedor pelo qual o usuário se autenticou por meio do Adobe Pass (por exemplo, `"Comcast"` ou `"DirecTV"`). Use-o para romper o engajamento do provedor de autenticação.

## Como essa dimensão é preenchida

O MVPD é definido pelo reprodutor no início da sessão quando o conteúdo é bloqueado por trás do Adobe Pass.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.pass.mvpd` quando os [[!UICONTROL Metadados de vídeo]](/help/reporting/setup/analytics-reporting.md) estão habilitados. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.mvpd`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videomvpd`, `post_videomvpd` |
| Audience Manager | `c_contextdata.a.media.pass.mvpd` |

## Itens de dimensão

Cada item é o nome literal do MVPD relatado no início da sessão. Use o identificador MVPD canônico do Adobe Pass por provedor para que os dados sejam acumulados até um único item de linha por provedor.
