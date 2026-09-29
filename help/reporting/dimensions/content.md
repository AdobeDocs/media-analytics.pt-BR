---
title: Conteúdo
description: Relata cada mídia executada, digitada pela ID de conteúdo.
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
source-wordcount: '251'
ht-degree: 7%
---

# Conteúdo

>[!BEGINSHADEBOX]

*Esta página cobre a dimensão de relatório **Conteúdo**. Consulte [ID de Conteúdo](/help/implementation/variables/core/content-id.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Conteúdo** relata cada parte exclusiva da mídia reproduzida, digitada pela ID de conteúdo definida no início da sessão. É o detalhamento principal para relatórios de mídia de transmissão e a chave de junção para dimensões de classificação, como Nome do vídeo, Duração do vídeo, ID do ativo, Data da primeira exibição e Classificação de conteúdo.

## Como essa dimensão é preenchida

O conteúdo é definido pelo reprodutor no início da sessão como um identificador estável para o ativo. A mesma ID de conteúdo é relatada em cada evento subsequente da sessão.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.name` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. Persiste durante a visita. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.name`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `video`, `post_video` |
| Audience Manager | `c_contextdata.a.media.name` |

>[!IMPORTANT]
>
>A ID de conteúdo é obrigatória. Se não estiver definida ou estiver vazia, a sessão será removida dos relatórios de streaming de mídia e não aparecerá em nenhum relatório de mídia ou no segmento [!UICONTROL Todas as mídias de streaming].

## Itens de dimensão

Cada item é uma ID de conteúdo exclusiva relatada no início da sessão. Use um identificador estável (por exemplo, uma CMS ID interna, uma ID do setor, como EIDR ou TMS/Gracenote, ou uma slug persistente) para que as sessões do mesmo ativo sejam acumuladas em um único item de linha ao longo do tempo.

## Segmentos recomendados

| Segmento | Regra |
| --- | --- |
| [!UICONTROL Todas as mídias de streaming] | O conteúdo (ID) existe |
