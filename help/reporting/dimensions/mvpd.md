---
title: MVPD
description: Informa o cabo, satélite ou provedor virtual pelo qual o usuário se autenticou.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 9%

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
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.pass.mvpd` quando os [[!UICONTROL Metadados de vídeo]](/help/reporting/media-reports-enable.md) estão habilitados. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.mvpd`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videomvpd`, `post_videomvpd` |
| Audience Manager | `c_contextdata.a.media.pass.mvpd` |

## Itens de dimensão

Cada item é o nome literal do MVPD relatado no início da sessão. Use o identificador MVPD canônico do Adobe Pass por provedor para que os dados sejam acumulados até um único item de linha por provedor.
