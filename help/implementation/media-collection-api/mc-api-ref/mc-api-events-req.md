---
title: Ponto de acesso da solicitação de eventos ‐ da API da coleção de mídia de transmissão
description: Quais são os parâmetros e as respostas do ponto de extremidade de solicitação de eventos da API Media Collection?
uuid: b237f0a0-dc29-418b-89ee-04c596a27f39
exl-id: ee0dd8a6-1529-4258-af12-0e2f5948ec38
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/yFHQhj33PM209WycWdPZsV-Yi8qN1DN-DC0KyyqFK1I
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: 263
ht-degree: 70%

---

# Solicitação de eventos{#events-request}

`POST https://{uri}/api/v1/sessions/{sid}/events`

## Parâmetro URI

`sid`: A ID da sessão retornada de uma [Solicitação de sessões](mc-api-sessions-req.md).

## Corpo da solicitação

O corpo da solicitação deve ser JSON e deve ter a mesma estrutura que este exemplo de corpo da solicitação:

```json
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
* `customMetadata` (Opcional; enviar somente com tipos de evento `adStart` e `chapterStart`)
* `qoeData` (Opcional)

Para obter uma lista de tipos de eventos válidos e exemplos de implementação por SDK, consulte [Visão geral dos eventos](/help/implementation/events/overview.md).

>[!IMPORTANT]
>
>***Rastreamento de anúncios -** Você somente pode rastrear anúncios dentro de um`adBreak`*.
>
>Na ausência de `adBreakStart` e &quot;finalizações&quot; `adBreakComplete` nos anúncios, os eventos `adStart` e `adComplete` simplesmente serão ignorados e a duração do anúncio correspondente será rastreada como a duração do conteúdo principal. Isso pode ter um impacto significativo nos dados agregados que estarão disponíveis no Adobe Analytics.

## Resposta

```text
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
| **204** | **Nenhum conteúdo.** <br/><br/>A chamada do Heartbeat foi bem-sucedida. | N/D |
| **400** | **Solicitação inválida.** <br/><br/>Solicitação com formato inapropriado. | Verifique os [esquemas de validação JSON](mc-api-json-validation.md) para o tipo de solicitação. |
| **404** | **Não encontrado.** <br/><br/>A ID da sessão para a sessão de mídia não foi encontrada no serviço de back-end. | O aplicativo cliente deve usar a API [Solicitação de sessões](mc-api-sessions-req.md) para criar outra sessão de mídia e o rastreamento de relatórios nela. |
| **410** | **Não existe mais.** <br/><br/>A sessão de mídia foi encontrada no serviço de back-end, mas o cliente não pode mais relatar atividade nela. | O aplicativo cliente deve usar a API [Solicitação de sessões](mc-api-sessions-req.md) para criar outra sessão de mídia e o rastreamento de relatórios nela. |
| **500** | **Erro do servidor** | N/D |
