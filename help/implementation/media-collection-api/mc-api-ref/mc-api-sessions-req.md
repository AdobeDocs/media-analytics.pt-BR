---
title: API de serviços de mídia de transmissão — Ponto de extremidade de solicitação de sessões
description: O que são os parâmetros de ponto de extremidade de solicitação de sessões da API Media Collection e as respostas?
uuid: 9609192d-4f7f-4fb5-844f-ea89d47c4e30
exl-id: f55f5838-610f-4f82-b3c5-72165ea2c86b
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/q8PEJKM8tYAOT6UMrqvtzMHYjCtk4kjDWVhtl9pgc1s
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 133
ht-degree: 85%

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
   * `playhead` - Se o conteúdo estiver ao vivo, o indicador de reprodução deve ser o segundo atual do dia, 0 &lt;= indicador de reprodução &lt; 86400. Se o conteúdo for gravado, o indicador de reprodução deve ser o segundo atual do conteúdo, 0 &lt;= indicador de reprodução &lt; duração do conteúdo. O valor pode ser um número de ponto flutuante.
   * `ts` - Carimbo de data e hora; deve estar em milissegundos; Tempo Universal Coordenado (UTC).
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
