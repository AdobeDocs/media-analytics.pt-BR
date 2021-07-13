---
title: Endpoint de solicitação de sessões da API da coleção de mídia de streaming �
description: '"Quais são os parâmetros e as respostas do endpoint de solicitação das sessões da API da coleção de mídia?"'
uuid: 9609192d-4f7f-4fb5-844f-ea89d47c4e30
exl-id: f55f5838-610f-4f82-b3c5-72165ea2c86b
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 80%

---

# Solicitação de sessões{#sessions-request}

```
POST 
https://{uri}/api/v1/sessions
```

## Parâmetros de URI

Nenhum

## Corpo da solicitação

O corpo da solicitação deve ser JSON e deve ter a mesma estrutura que este exemplo de corpo da solicitação:

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

   **Valor válido:** `sessionStart`
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

`Location:` cabeçalho — A parte `/api/v1/` fornece a versão da API. A parte depois de `[…]sessions/` é a ID da sessão.

## Códigos de resposta

| Código de resposta HTTP | Descrição |
|---|---|
| 201 | Sessão criada |
| 400 | Solicitação inválida |
| 500 | Erro do servidor |
