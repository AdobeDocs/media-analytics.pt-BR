---
title: Suporte a metadados personalizados - Formato XDM
description: Saiba como enviar metadados personalizados com eventos de rastreamento de mídia usando o formato XDM da Experience Edge.
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: da2fe856a32f9056752b9e2c2e339d43be20372a
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 2%

---


# Suporte a metadados personalizados - formato XDM

A API da Experience Edge permite enviar metadados personalizados de mídia juntamente com campos XDM padrão em eventos de API `sessionStart`, `adStart` e `chapterStart`. Os metadados personalizados de mídia enviados por meio do formato XDM podem ser encaminhados ao **Adobe Analytics** e ao **Adobe Experience Platform**.

Para implementações da API Media Collection, consulte [Suporte a metadados personalizados](/help/implementation/media-collection-api/mc-api-impl/mc-api-custom-meta.md).

## Visão geral

Os metadados personalizados de mídia podem ser enviados em dois locais em uma solicitação do Experience Edge, cada um com um comportamento de roteamento diferente:

| Localização | Enviado para o Adobe Analytics | Enviado para o Adobe Experience Platform | Caso de uso |
|----------|------------------------|-----------------------------------|----------|
| `xdm.mediaCollection.customMetadata` | ✅ Sim | ✅ Sim | Dados de negócios necessários em ambos os sistemas |
| `_data` | ✅ Sim | ❌ Não | Sinalizadores específicos do Analytics ou dicas de processamento |

Os metadados personalizados se aplicam a três tipos de evento:

| Evento | Os Metadados Se Aplicam A |
|-------|-------------------|
| `sessionStart` | Conteúdo principal (toda a sessão) |
| `adStart` | Anúncio individual |
| `chapterStart` | Capítulo ou segmento do conteúdo |

## Estrutura

### `xdm.mediaCollection.customMetadata` (Analytics + AEP)

Os metadados personalizados são uma **matriz de objetos de valor de nome** dentro do objeto `mediaCollection`:

```json
{
  "xdm": {
    "mediaCollection": {
      "customMetadata": [
        {
          "name": "_tenant.fieldName",
          "value": "fieldValue"
        }
      ]
    }
  }
}
```

<InlineAlert variant="warning" slots="text" />

`customMetadata` deve ser uma **matriz** dentro de `mediaCollection`, não no nível raiz `xdm`.

**Incorreto:**

```json
{
  "xdm": {
    "eventType": "media.sessionStart",
    "customMetadata": [...]  // ❌ Wrong location
  }
}
```

**Correto:**

```json
{
  "xdm": {
    "eventType": "media.sessionStart",
    "mediaCollection": {
      "customMetadata": [...]  // ✅ Inside mediaCollection
    }
  }
}
```

### `_data` (somente Analytics)

O objeto `_data` é uma construção especial do Experience Edge que envia dados exclusivamente para o Adobe Analytics, ignorando os conjuntos de dados do AEP. Os metadados personalizados devem ser colocados em `__adobe.analytics.contextData`.

Ao contrário de `xdm.mediaCollection.customMetadata` que usa uma **matriz de objetos de valor de nome**, o mapeamento `_data` usa um **objeto de valor de chave** simples diretamente em `contextData`:

| Abordagem | Estrutura | Destino |
|----------|-----------|-------------|
| `xdm.mediaCollection.customMetadata` | Matriz de `{"name": "...", "value": "..."}` objetos | Analytics + AEP |
| `_data.__adobe.analytics.contextData` | Objeto de valor de chave simples `{"key": "value"}` | Somente Analytics |

```json
{
  "xdm": { ... },
  "_data": {
    "__adobe": {
      "analytics": {
        "contextData": {
          "debugMode": "true",
          "internalTestFlag": "QA-Session"
        }
      }
    }
  }
}
```

### Nomeação de convenções

- **Formato XDM:** prefixo com namespace de locatário usando um sublinhado. Você também pode criar estruturas no grupo de campos personalizados do locatário, como `_<tenant>.<struct_name>.<field_name>`.
- Formato **`_data`:** campos estão posicionados em `_data.__adobe.analytics.contextData` — nenhum prefixo de sublinhado é necessário no nome do campo (por exemplo, `debugFlag`)

## Metadados personalizados do conteúdo principal

Enviado com `sessionStart`. Aplica-se à mídia principal que está sendo rastreada e permanece disponível em chamadas de anúncio e capítulo. Quaisquer metadados personalizados definidos aqui serão mesclados automaticamente pelo back-end de mídia nas chamadas de fechamento correspondentes. Ele será incluído junto com quaisquer metadados personalizados específicos definidos para anúncios e capítulos.

<CodeBlock slots="heading, code" repeat="1" languages="CURL"/>

### Solicitação

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId={datastreamId}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
          "sessionDetails": {
            "name": "Sample Video",
            "playerName": "HTML5 Player",
            "contentType": "VOD",
            "length": 3600,
            "channel": "Sports"
          },
          "playhead": 0,
          "customMetadata": [
            {
              "name": "_mycompany.contentCategory",
              "value": "Live Sports"
            },
            {
              "name": "_mycompany.leagueType",
              "value": "Professional"
            }
          ]
        },
        "timestamp": "2026-03-10T18:00:00Z"
      }
    }
  ]
}'
```

## Adicionar metadados personalizados

Enviado com `adStart`. Específico para cada anúncio individual. Os metadados personalizados de `sessionStart` também são mesclados automaticamente pelo back-end de mídia na chamada de fechamento de anúncio ao lado de qualquer metadado personalizado específico do anúncio definido aqui.

<CodeBlock slots="heading, code" repeat="1" languages="CURL"/>

### Solicitação

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adStart?configId={datastreamId}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [
    {
      "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
          "sessionID": "your-session-id",
          "playhead": 30,
          "advertisingDetails": {
            "name": "Summer Sale Ad",
            "playerName": "HTML5 Player",
            "length": 30,
            "podPosition": 1
          },
          "customMetadata": [
            {
              "name": "_mycompany.campaignId",
              "value": "SUMMER2026"
            },
            {
              "name": "_mycompany.targetAudience",
              "value": "18-34"
            },
            {
              "name": "_mycompany.adFormat",
              "value": "skippable"
            }
          ]
        },
        "timestamp": "2026-03-10T18:05:30Z"
      }
    }
  ]
}'
```

## Metadados personalizados de capítulo

Enviado com `chapterStart`. Específico para cada capítulo ou segmento de conteúdo. Os metadados personalizados do `sessionStart` também são mesclados automaticamente pelo back-end de mídia na chamada de fechamento do capítulo ao lado de qualquer metadado personalizado específico do capítulo definido aqui.

<CodeBlock slots="heading, code" repeat="1" languages="CURL"/>

### Solicitação

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/chapterStart?configId={datastreamId}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [
    {
      "xdm": {
        "eventType": "media.chapterStart",
        "mediaCollection": {
          "sessionID": "your-session-id",
          "playhead": 600,
          "chapterDetails": {
            "friendlyName": "Introduction",
            "length": 300,
            "index": 1,
            "offset": 600
          },
          "customMetadata": [
            {
              "name": "_mycompany.chapterType",
              "value": "tutorial"
            },
            {
              "name": "_mycompany.difficulty",
              "value": "beginner"
            }
          ]
        },
        "timestamp": "2026-03-10T18:10:00Z"
      }
    }
  ]
}'
```

## Usando o objeto `_data` (metadados somente Analytics)

Use o objeto `_data` quando precisar de metadados no Adobe Analytics que devem **não** ser armazenados em conjuntos de dados do AEP — por exemplo, sinalizadores temporários, variáveis de depuração ou dicas de processamento específicas do Analytics.

<InlineAlert variant="warning" slots="text" />

Os dados enviados via `_data` não são armazenados no Adobe Experience Platform e não estão disponíveis para o Real-Time CDP, Journey Orchestration ou outros serviços da AEP.

<CodeBlock slots="heading, code" repeat="1" languages="CURL"/>

### Solicitação

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId={datastreamId}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
          "sessionDetails": {
            "name": "Sample Video",
            "playerName": "HTML5 Player",
            "contentType": "VOD",
            "length": 3600
          },
          "playhead": 0,
          "customMetadata": [
            {
              "name": "_mycompany.league",
              "value": "Action"
            }
          ]
        },
        "timestamp": "2026-03-10T18:00:00Z"
      },
      "_data": {
        "__adobe": {
          "analytics": {
            "contextData": {
              "debugMode": "true",
              "testFlag": "QA-Session"
            }
          }
        }
      }
    }
  ]
}'
```

Neste exemplo:
- `_mycompany.league` → enviado ao Analytics e ao AEP
- `debugMode` e `testFlag` (em `_data.__adobe.analytics.contextData`) → enviado somente para o Analytics


## Local dos dados downstream

<InlineAlert variant="info" slots="text" />

`xdm.mediaCollection.customMetadata` é o **caminho de API de entrada** usado para enviar metadados personalizados com eventos. Após o processamento, os dados são encaminhados ao Adobe Analytics como variáveis de dados de contexto e armazenados no Adobe Experience Platform em `mediaReporting.customMetadata` e como campos nivelados de nível superior.

**Adobe Analytics:**
- Após o processamento, os metadados personalizados são encaminhados para o Adobe Analytics como variáveis de dados de contexto. O prefixo `_tenant` é removido automaticamente, portanto, as regras de processamento referenciam somente o caminho do campo após `_tenant` (por exemplo, `_mycompany.contentCategory` torna-se `contentCategory`)
- Os dados enviados via `_data` também são encaminhados ao Adobe Analytics e disponibilizados pelas regras de processamento
- Use as regras de processamento para mapear variáveis de dados de contexto para eVars, props ou outras variáveis do Analytics. Consulte [Mapeamento de variável de dados para o Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/data-var-mapping) para obter detalhes.

**Adobe Experience Platform:**
- Os campos de metadados personalizados devem ser definidos como campos personalizados no esquema XDM (por exemplo, `_mycompany`) e podem ser armazenados e consultados no AEP como campos nivelados

  ![Definição de campo personalizado no esquema XDM](assets/custom_metadata.png)
- Para relatórios e consultas, os metadados personalizados estão disponíveis em `mediaReporting.customMetadata` e também como campos nivelados de nível superior. Use o que for mais adequado para seu caso de uso.
- Acessível para segmentação, Journey Orchestration e ativação do Real-Time CDP

## Comportamento

- Todos os valores de metadados personalizados devem ser **cadeias de caracteres**. Converta números e booleanos antes de enviar.
- `sessionStart` metadados persistem para a sessão inteira; as atualizações exigem uma nova sessão
- Cada evento do `adStart` e do `chapterStart` pode carregar diferentes metadados personalizados
- Preferir campos XDM padrão (`sessionDetails`, `advertisingDetails`, `chapterDetails`) aos metadados personalizados quando existir um campo padrão


## Documentação relacionada

- [Suporte a metadados personalizados](/help/implementation/media-collection-api/mc-api-impl/mc-api-custom-meta.md). — API MC (formato JSON)
- [Tipo de dados de Detalhes da Coleção de Mídia](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) — Referência de esquema XDM
- [Mapeamento de variável de dados para o Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/data-var-mapping) — Mapeamento de dados de contexto do Analytics para campos XDM
<!--
- [Session endpoints](sessions.md) — Session lifecycle management
- [Ad endpoints](ads.md) — Track advertising impressions
- [Chapter endpoints](chapters.md) — Segment content into chapters
-->
