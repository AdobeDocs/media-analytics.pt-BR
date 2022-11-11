---
title: Ponto de extremidade da solicitação de eventos da API da coleção de mídia de streaming �
description: "Quais são os parâmetros de ponto de extremidade e as respostas da solicitação dos eventos da API da coleção de mídia?"
uuid: b237f0a0-dc29-418b-89ee-04c596a27f39
exl-id: ee0dd8a6-1529-4258-af12-0e2f5948ec38
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 92%

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

Para obter uma lista de tipos de eventos válidos para esta versão, consulte [Tipos e descrições de eventos.](mc-api-event-types.md)

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
| **204** | **Sem conteúdo.** <br/><br/>O Heartbeat foi salvo com sucesso. | N/D |
| **400** | **Solicitação inválida.** <br/><br/>Solicitação com formato inapropriado. | Verifique os [esquemas de validação JSON](mc-api-json-validation.md) para o tipo de solicitação. |
| **404** | **Não encontrado.** <br/><br/>A ID da sessão para a sessão de mídia não foi encontrada no serviço de back-end. | O aplicativo cliente deve usar a API [Solicitação de sessões](mc-api-sessions-req.md) para criar outra sessão de mídia e o rastreamento de relatórios nela. |
| **410** | **Excluído.** <br/><br/>A sessão de mídia foi encontrada no serviço de back-end, mas o cliente não pode mais relatar atividade nela. | O aplicativo cliente deve usar a API [Solicitação de sessões](mc-api-sessions-req.md) para criar outra sessão de mídia e o rastreamento de relatórios nela. |
| **500** | **Erro do servidor** | N/D |
