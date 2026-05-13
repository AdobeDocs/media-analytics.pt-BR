---
title: MVPD
description: Informa o cabo, satélite ou provedor virtual pelo qual o usuário se autenticou.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 8%

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
| Customer Journey Analytics | [`mediaReporting.sessionDetails.mvpd`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videomvpd, post_videomvpd` |

## Itens de dimensão

Cada item é o nome literal do MVPD relatado no início da sessão. Use o identificador MVPD canônico do Adobe Pass por provedor para que os dados sejam acumulados até um único item de linha por provedor.
