---
title: Álbum
description: Relata o álbum ao qual a faixa de áudio pertence.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
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
