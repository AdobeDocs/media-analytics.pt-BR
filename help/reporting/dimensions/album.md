---
title: Álbum
description: Relata o álbum ao qual a faixa de áudio pertence.
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
source-wordcount: '136'
ht-degree: 10%
---

# Álbum

>[!BEGINSHADEBOX]

*Esta página cobre a dimensão de relatório **Álbum**. Consulte [Álbum](/help/implementation/variables/standard-metadata/album.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Álbum** informa o álbum ao qual a faixa de áudio pertence (por exemplo, `"Pinegrove"`). Use-o para acumular engajamento entre faixas do mesmo álbum.

## Como essa dimensão é preenchida

O álbum é definido pelo reprodutor no início da sessão para o conteúdo de áudio.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.album` quando os [[!UICONTROL Metadados de áudio]](/help/reporting/setup/analytics-reporting.md) estão habilitados. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.album`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videoaudioalbum` |
| Audience Manager | `c_contextdata.a.media.album` |

## Itens de dimensão

Cada item é o título literal do álbum relatado no início da sessão. Dois álbuns com o mesmo título de artistas diferentes são recolhidos para um único item de linha. Emparelhe com a dimensão [Artista](artist.md) para desfazer a ambiguidade.
