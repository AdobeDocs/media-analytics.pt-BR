---
title: Suporte a metadados personalizados
description: Saiba como fornecer pares de chave:valor personalizados nos eventos sessionStart, chapterStart e adStart.
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: 3cebd16d47a0dceb66e7fe1faf312cef14638a3e
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 7%

---

# Suporte a metadados personalizados{#custom-metadata-support}

A API Media Collection permite enviar pares de valores chave personalizados juntamente com parâmetros padrão em eventos `sessionStart`, `adStart` e `chapterStart`. Os metadados personalizados são encaminhados ao **Adobe Analytics** com os respectivos eventos de fechamento de mídia.

Para disponibilizar esses dados no Analysis Workspace, os clientes devem definir eVars personalizadas e configurar regras de processamento para preenchê-las de acordo com seu caso de uso. Depois de mapeados para eVars ou props, os dados também ficam disponíveis no Adobe Experience Platform por meio dos caminhos do eVar correspondentes, desde que o [Conector de origem do Analytics](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sources/connectors/adobe-applications/analytics) esteja configurado.

Para implementações baseadas em XDM usando o Experience Edge, consulte [Suporte a metadados personalizados - formato XDM](/help/implementation/edge/implementation-edge-custom-metadata.md).

## Visão geral

Os metadados personalizados estão incluídos no corpo da solicitação como um objeto `customMetadata`, posicionado junto com a chave `params`. Ela se aplica a três tipos de evento:

| Evento | Os Metadados Se Aplicam A |
|-------|-------------------|
| `sessionStart` | Conteúdo principal (toda a sessão) |
| `adStart` | Anúncio individual |
| `chapterStart` | Capítulo ou segmento do conteúdo |

## Estrutura

Os metadados personalizados são um **objeto** simples (pares de valores chave) no nível do evento, ao lado da chave `params`:

```json
{
  "playerTime": {
    "playhead": 0,
    "ts": 1646938800000
  },
  "eventType": "sessionStart",
  "params": {
    "analytics.trackingServer": "example.sc.omtrdc.net",
    "analytics.reportSuite": "example-rsid",
    "visitor.marketingCloudOrgId": "0123456789@AdobeOrg",
    "media.id": "sample-video-id",
    "media.length": 3600,
    "media.contentType": "vod",
    "media.playerName": "HTML5 Player",
    "media.channel": "Sports"
  },
  "customMetadata": {
    "field": "value"
  }
}
```

### Parâmetros obrigatórios por tipo de evento

| Evento | Necessário `params` |
|-------|-------------------|
| `sessionStart` | `analytics.trackingServer`, `analytics.reportSuite`, `visitor.marketingCloudOrgId`, `media.id`, `media.length`, `media.contentType`, `media.playerName`, `media.channel` |
| `adStart` | `media.ad.id`, `media.ad.length`, `media.ad.podPosition`, `media.ad.playerName` |
| `chapterStart` | `media.chapter.length`, `media.chapter.offset`, `media.chapter.index` |

### Requisitos de nomenclatura de chave

- Evite usar o prefixo `media.` em chaves de metadados personalizadas, ele mapeia para campos de mídia padrão e pode substituí-los nos relatórios do Analytics
- O prefixo `a.` é reservado para metadados padrão do Adobe e não deve ser usado

## Metadados personalizados do conteúdo principal

Enviado com `sessionStart`. Aplica-se à mídia principal que está sendo rastreada e permanece disponível em chamadas de anúncio e capítulo. Quaisquer metadados personalizados definidos aqui serão mesclados automaticamente pelo back-end de mídia nas chamadas de fechamento correspondentes. Ele será incluído junto com quaisquer metadados personalizados específicos definidos para anúncios e capítulos.

```sh
curl -X POST "https://{uri}/api/v1/sessions" \
--header 'Content-Type: application/json' \
--data '{
  "playerTime": {
    "playhead": 0,
    "ts": 1646938800000
  },
  "eventType": "sessionStart",
  "params": {
    "analytics.trackingServer": "example.sc.omtrdc.net",
    "analytics.reportSuite": "example-rsid",
    "analytics.visitorId": "visitor123",
    "visitor.marketingCloudOrgId": "0123456789@AdobeOrg",
    "media.id": "sample-video-id",
    "media.name": "Sample Video",
    "media.length": 3600,
    "media.contentType": "vod",
    "media.playerName": "HTML5 Player",
    "media.channel": "Sports"
  },
  "customMetadata": {
    "contentCategory": "Live Sports",
    "leagueType": "Professional",
    "broadcastRights": "Premium"
  }
}'
```

## Adicionar metadados personalizados

Enviado com `adStart`. Específico para cada anúncio individual. Os metadados personalizados de `sessionStart` também são mesclados automaticamente pelo back-end de mídia na chamada de fechamento de anúncio ao lado de qualquer metadado personalizado específico do anúncio definido aqui.

```sh
curl -X POST "https://{uri}/api/v1/sessions/{sid}/events" \
--header 'Content-Type: application/json' \
--data '{
  "playerTime": {
    "playhead": 30,
    "ts": 1646938830000
  },
  "eventType": "adStart",
  "params": {
    "media.ad.id": "summer-sale-2026",
    "media.ad.name": "Summer Sale Ad",
    "media.ad.length": 30,
    "media.ad.playerName": "HTML5 Player",
    "media.ad.podPosition": 1
  },
  "customMetadata": {
    "campaignId": "SUMMER2026",
    "targetAudience": "18-34",
    "adFormat": "skippable"
  }
}'
```

## Metadados personalizados de capítulo

Enviado com `chapterStart`. Específico para cada capítulo ou segmento de conteúdo. Os metadados personalizados do `sessionStart` também são mesclados automaticamente pelo back-end de mídia na chamada de fechamento do capítulo ao lado de qualquer metadado personalizado específico do capítulo definido aqui.

```sh
curl -X POST "https://{uri}/api/v1/sessions/{sid}/events" \
--header 'Content-Type: application/json' \
--data '{
  "playerTime": {
    "playhead": 600,
    "ts": 1646938200000
  },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.friendlyName": "Introduction",
    "media.chapter.length": 300,
    "media.chapter.index": 1,
    "media.chapter.offset": 600
  },
  "customMetadata": {
    "chapterType": "tutorial",
    "difficulty": "beginner",
    "instructor": "Jane Smith"
  }
}'
```

## Comportamento

- Todos os valores de metadados personalizados devem ser **cadeias de caracteres**. Converta números e booleanos antes de enviar.
- Os metadados personalizados aparecem no Analytics com um prefixo `c.` (por exemplo, `contentCategory` → `c.contentCategory`)
- Mapear metadados personalizados para eVars, props ou variáveis de dados de contexto por meio de regras de processamento do Analytics
- `sessionStart` metadados persistem para a sessão inteira; as atualizações exigem uma nova sessão
- Cada evento do `adStart` e do `chapterStart` pode carregar diferentes metadados personalizados

## Documentação relacionada

- [Suporte a metadados personalizados - Formato XDM](/help/implementation/edge/implementation-edge-custom-metadata.md) — Enviar metadados personalizados via Experience Edge para o Analytics e o AEP
- [Conector de origem do Adobe Analytics para dados do conjunto de relatórios](https://experienceleague.adobe.com/pt-br/docs/experience-platform/sources/connectors/adobe-applications/analytics) — Trazer dados do Analytics para a Adobe Experience Platform

<!--
- [Session endpoints](sessions.md) — Session lifecycle management
- [Ad endpoints](ads.md) — Track advertising impressions
- [Chapter endpoints](chapters.md) — Segment content into chapters
-->
