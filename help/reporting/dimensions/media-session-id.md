---
title: ID da sessão de mídia
description: Identifica exclusivamente cada sessão de reprodução.
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
source-wordcount: '205'
ht-degree: 6%
---

# ID da sessão de mídia

A dimensão **ID da sessão de mídia** identifica cada sessão de reprodução de forma exclusiva. Ele é gerado pelo back-end e carimbado em cada evento da sessão. Use-a para isolar os eventos de uma única sessão para depuração ou para desduplicar sessões em análises personalizadas.

## Como essa dimensão é preenchida

A ID da sessão é gerada automaticamente quando o back-end recebe um evento [início de sessão](/help/implementation/events/session/session-start.md). As implementações do Web SDK e do Mobile SDK capturam e persistem a ID para você; as implementações de API direta devem ler a ID da sessão da resposta `sessionStart` (o cabeçalho `Location` para a API Media Collection ou o identificador `media-analytics:new-session` para a API Media Edge) e incluí-la nos eventos subsequentes.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Crie uma [Regra de processamento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.vsid` para uma eVar. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.ID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videosessionid`, `post_videosessionid` |
| Audience Manager | `c_contextdata.a.media.vsid` |

## Itens de dimensão

Cada item é uma ID de sessão exclusiva gerada pelo back-end (normalmente uma sequência alfanumérica de 22 caracteres). Use o campo Filter ou Search para pesquisar uma sessão específica.
