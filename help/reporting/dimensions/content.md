---
title: Conteúdo
description: Relata cada mídia executada, digitada pela ID de conteúdo.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 6%

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
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.name` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. Persiste durante a visita. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.name`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
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
