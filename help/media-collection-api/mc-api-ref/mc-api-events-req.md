---
seo-title: Solicitação de eventos
title: Solicitação de eventos
uuid: b237f0a0-dc29-418b-89ee-04c596a27f39
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Solicitação de eventos{#events-request}

```
POST 
https://{uri}/api/v1/sessions/{sid}/events 
```

## Parâmetro URI

`sid`: A ID da sessão retornada de uma solicitação de [Sessões.](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)

## Corpo da solicitação

O corpo da solicitação deve ser JSON e ter a mesma estrutura que este corpo de solicitação de amostra:

```
{ 
    "playerTime": { 
        "playhead": 0, 
        "ts": 1509045324153 
    }, 
    "eventType": "{event-type}", 
    "params": {}, 
    "qoeData": {}, 
    "customMetadata": {} 
}
```

* `playerTime` (Obrigatório)
   * `playhead` - Deve ser expresso em segundos, mas pode ser um float.
   * `ts` - carimbo de data e hora; deve estar em milissegundos.
* `eventType` (Obrigatório)
* `params` (Opcional)
* `customMetadata` (Opcional; enviar somente com tipos `adStart` e `chapterStart` eventos)
* `qoeData` (Opcional)

Para obter uma lista de tipos de eventos válidos para esta versão, consulte [Tipos e descrições de eventos.](/help/media-collection-api/mc-api-ref/mc-api-event-types.md)

>[!IMPORTANT]
>
>***Rastreamento de anúncios - Você só pode rastrear anúncios dentro de um**`adBreak`*.
>
>Na ausência de `adBreakStart` e "finalizações" `adBreakComplete` nos anúncios, os eventos `adStart` e `adComplete` simplesmente serão ignorados e a duração do anúncio correspondente será rastreada como a duração do conteúdo principal. Isso pode ter um impacto significativo nos dados agregados que estarão disponíveis no Adobe Analytics.

## Resposta

```
HTTP/1.1 204 No Content 
Server nginx/1.13.5 
Date Thu, 26 Oct 2017 19:15:24 GMT 
Connection keep-alive 
Access-Control-Allow-Origin * 
Access-Control-Allow-Methods OPTIONS,POST,PUT 
Access-Control-Allow-Headers Content-Type 
Access-Control-Expose-Headers Location
```

## Códigos de resposta HTTP

| Código de resposta HTTP | Descrição | Itens de ação do cliente |
|---|---|---|
| **204** | **Sem conteúdo.** <br/><br/>O Heartbeat foi salvo com sucesso. | N/A |
| **400** | **Solicitação inválida.** <br/><br/>Solicitação com formato inapropriado. | Verifique o tipo de solicitação dos [esquemas de validação de JSON](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md). |
| **404** | **Não encontrada.** <br/><br/>A ID da sessão da sessão de mídia não foi encontrada no serviço back-end. | O aplicativo do cliente deve usar a [API de solicitação de sessões](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para criar outra sessão de mídia e relatar o rastreamento nela. |
| **410** | **Gone.** <br/><br/>A sessão de mídia foi encontrada no serviço back-end, mas o cliente não pode mais relatar a atividade nela. | O aplicativo do cliente deve usar a [API de solicitação de sessões](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para criar outra sessão de mídia e relatar o rastreamento nela. |
| **500** | **Erro do servidor** | N/A |

