---
seo-title: Solicitação de sessões
title: Solicitação de sessões
uuid: 9609192 d -4 f 7 f -4 fb 5-844 f-ea 89 d 47 c 4 e 30
translation-type: tm+mt
source-git-commit: f1c9f5f4cbcd4c043e1c7b4a5037c134b2bdd380

---


# Solicitação de sessões{#sessions-request}

```
POST 
https://{uri}/api/v1/sessions
```

## Parâmetros de URI

Nenhum

## Corpo da solicitação

O corpo da solicitação deve ser JSON e deve ter a mesma estrutura desse corpo de solicitação de amostra:

```
{ 
    "playerTime": { 
        "playhead": 0, 
        "ts": 1509045324153 
    }, 
    "eventType": "sessionStart", 
    "params": { 
        "media.playerName": "sample-html5-api-player", 
        "analytics.trackingServer": "<your-aa-tracking-server>", 
        "analytics.reportSuite": "<your-aa-rsid>", 
        "analytics.visitorId": "<your-userId>", 
        "media.contentType": "VOD", 
        "media.length": 60.39333333333333, 
        "media.id": "MA API Sample Player", 
        "visitor.marketingCloudOrgId": "<your-org-id>", 
        "media.name": "ClickMe", 
        "media.channel": "sample-channel", 
        "media.sdkVersion": "va-api-0.0.0", 
        "analytics.enableSSL": false 
    }, 
    "customMetadata": { 
        "myCustomData": "<your metadata>", 
        "myCustomData2": "<your metadata>", 
        ... 
    }, 
    "qoeData": { 
        "param1": "<your param-value>", 
        "param2": "<your param-value>", 
        ... 
    } 
}
```

* `playerTime` (Obrigatório)
   * `playhead` - Deve ser expresso em segundos, mas pode ser um float.
   * `ts` - carimbo de data e hora; deve estar em milissegundos.
* `eventType` (Obrigatório)

   **Valor válido:**`sessionStart`
* `params` (Obrigatório)
* `customMetadata` (Opcional)
* `qoeData` (Opcional)

## Resposta

```
HTTP/1.1 201 Created 
Server: nginx/1.13.5 
Date: Wed, 06 Dec 2017 19:14:51 GMT 
Content-Type: application/octet-stream 
Content-Length: 0 
Location: /api/v1/sessions/bfcca2ca597a3c71bc03b4ce357833ad02b3570d262ecd0c595fcf8f2ae4df58 
Access-Control-Allow-Origin: * 
Access-Control-Allow-Methods: OPTIONS,POST,PUT 
Access-Control-Allow-Headers: Content-Type 
Access-Control-Expose-Headers: Location 
Age: 0 
Via: 1.1 wsg.sanjose08
```

`Location:` cabeçalho - A `/api/v1/` parte fornece a versão da API. The part after `[…]sessions/` is the Session ID.

## Códigos de resposta

| Código de resposta HTTP | Descrição |
|---|---|
| 201 | Sessão criada |
| 400 | Solicitação inválida |
| 500 | Erro do servidor |

