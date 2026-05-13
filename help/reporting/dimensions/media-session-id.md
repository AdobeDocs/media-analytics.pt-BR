---
title: ID da sessão de mídia
description: Identifica exclusivamente cada sessão de reprodução.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 5%

---


# ID da sessão de mídia

A dimensão **ID da sessão de mídia** identifica cada sessão de reprodução de forma exclusiva. Ele é gerado pelo back-end e carimbado em cada evento da sessão. Use-a para isolar os eventos de uma única sessão para depuração ou para desduplicar sessões em análises personalizadas.

## Como essa dimensão é preenchida

A ID da sessão é gerada automaticamente quando o back-end recebe um evento `media.sessionStart`. As implementações do Web SDK e do Mobile SDK capturam e persistem a ID para você; as implementações de API direta devem ler a ID da sessão da resposta `sessionStart` (o cabeçalho `Location` para a API Media Collection ou o identificador `media-analytics:new-session` para a API Media Edge) e incluí-la nos eventos subsequentes.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Crie uma [Regra de processamento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.vsid` para uma eVar. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.ID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videosessionid, post_videosessionid` |

## Itens de dimensão

Cada item é uma ID de sessão exclusiva gerada pelo back-end (normalmente uma sequência alfanumérica de 22 caracteres). Use o campo Filter ou Search para pesquisar uma sessão específica.
