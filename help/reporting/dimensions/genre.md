---
title: Gênero
description: Gênero de conteúdo de relatórios. O conteúdo multigênero é dividido em itens de linha, cada um recebendo peso de métrica igual.
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
source-wordcount: '181'
ht-degree: 8%
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
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.genre` (armazenado como uma variável de lista) quando os [[!UICONTROL Metadados de vídeo]](/help/reporting/setup/analytics-reporting.md) estão habilitados. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.genreList`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) ou [`xdm.mediaReporting.sessionDetails.genre`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) (Herdado) |
| Feeds de dados | `videogenre`, `post_videogenre` |
| Audience Manager | `c_contextdata.a.media.genre` |

## Itens de dimensão

Cada item é um valor de gênero. Sessões multigênero (por exemplo, `"Drama,Action"`) aparecem como dois itens de linha separados (`Drama` e `Action`), com cada item recebendo crédito total pela sessão.
