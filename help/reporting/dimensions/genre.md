---
title: Gênero
description: Gênero de conteúdo de relatórios. O conteúdo multigênero é dividido em itens de linha, cada um recebendo peso de métrica igual.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 7%

---


# Gênero

>[!BEGINSHADEBOX]

*Esta página cobre a dimensão de relatório **Gênero**. Consulte [Gênero](/help/implementation/variables/standard-metadata/genre.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Gênero** informa o gênero do conteúdo. O gênero é coletado como uma string delimitada por vírgulas e armazenado como uma dimensão de lista. O conteúdo multigênero é dividido em itens de linha separados, cada um recebendo peso de métrica igual. Use-o para comparar o engajamento entre gêneros sem contar duas vezes o tempo gasto em um único ativo de vários gêneros.

## Como essa dimensão é preenchida

O gênero é definido pelo reprodutor no início da sessão.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.genre` (armazenado como uma variável de lista) quando os [[!UICONTROL Metadados de vídeo]](/help/reporting/media-reports-enable.md) estão habilitados. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.genreList`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) ou [`xdm.mediaReporting.sessionDetails.genre`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) (Herdado) |
| Feeds de dados | `videogenre`, `post_videogenre` |
| Audience Manager | `c_contextdata.a.media.genre` |

## Itens de dimensão

Cada item é um valor de gênero. Sessões multigênero (por exemplo, `"Drama,Action"`) aparecem como dois itens de linha separados (`Drama` e `Action`), com cada item recebendo crédito total pela sessão.
