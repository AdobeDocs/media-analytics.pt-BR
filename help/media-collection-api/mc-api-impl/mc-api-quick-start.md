---
title: '"API da coleção de mídia de streaming - Início rápido"'
description: Introdução à API da mídia de transmissão. Saiba como verificar rapidamente seus dados de solicitação.
uuid: ca20bad4-2c8f-406b-833e-b4883a9aa534
exl-id: 08bb5873-f69a-4fdd-8f27-69649b4acb17
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 92%

---

# Início rápido{#quick-start}

>[!TIP]
>
>Obtenha os dados de solicitação necessários para concluir uma [Solicitação de sessão](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) bem-sucedida no servidor do back-end da API da coleção do Media Analytics (MA). Você pode verificar rapidamente seus dados de solicitação enviando solicitações manualmente (com `curl`, Postman, etc.). Você terá feedback imediato se você tiver algum problema com tipos de dados incorretos ou informações incorretas em sua solicitação. Use os [esquemas de validação JSON](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) para verificar se você está fornecendo dados de solicitação adequados.

1. Obtenha os dados padrão e necessários do Adobe Analytics e do visitante que você deve fornecer para executar qualquer um dos aplicativos da Experience Cloud:

   * ID da organização da Experience Cloud do visitante
   * ID do usuário da Experience Cloud do visitante
   * ID de conjunto de relatórios do Analytics
   * URL do servidor de rastreamento do Analytics

1. Crie um objeto JSON para o corpo da solicitação `sessions` contendo os dados mínimos necessários para uma chamada bem-sucedida. Por exemplo:

   ```
   { 
       "playerTime": { 
           "playhead": 0, 
           "ts": 1234560890123 
       }, 
       "eventType": "sessionStart", 
       "params": { 
           "media.playerName": "sample-html5-api-player", 
           "analytics.trackingServer": "[YOUR_TS]", 
           "analytics.reportSuite": "[YOUR_RSID]", 
           "media.contentType": "VOD", 
           "media.length": 60.39333333333333, 
           "media.id": "MA Collection API Sample Player", 
           "visitor.marketingCloudOrgId": "[YOUR_ORG_ID]", 
           "visitor.marketingCloudUserId": "[YOUR_ECID]",
           "media.name": "ClickMe", 
           "media.channel": "sample-channel", 
           "media.sdkVersion": "va-api-0.0.0", 
           "analytics.enableSSL": false 
       } 
   }
   ```

   >[!NOTE]
   >
   >Você deve usar os tipos de dados corretos no corpo da solicitação JSON. Por exemplo, `analytics.enableSSL` exige um booleano, `media.length` é numérico, etc. Você pode verificar os tipos de parâmetros e requisitos de obrigatoriedade nos [esquemas de validação JSON.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

1. Envie Solicitações de sessões para o endpoint da API da coleção do MA. Se a carga da sua solicitação for inválida, identifique o problema e tente novamente até obter uma resposta `201 Created`. Neste exemplo `curl`, o corpo da solicitação JSON está em um arquivo denominado `sample_data_session`:

   ```
   $ curl -i -d \ 
     @sample_data_session https://{uri}/api/v1/sessions \ 
     > curl.sessions.out 
   
   $ cat curl.sessions.out 
   HTTP/1.1 201 Created 
   Server: nginx/1.13.5 
   Date: Mon, 18 Dec 2017 22:34:12 GMT 
   Content-Type: application/octet-stream 
   Content-Length: 0 
   Connection: keep-alive 
   Location: /api/v1/sessions/a39c037641f[...]  # <== Session ID  
   Access-Control-Allow-Origin: * 
   Access-Control-Allow-Methods: OPTIONS,POST,PUT 
   Access-Control-Allow-Headers: Content-Type 
   Access-Control-Expose-Headers: Location
   ```

Se a [Solicitação de sessões](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) tiver êxito, você receberá uma resposta `201 Created` semelhante à mostrada acima. A resposta inclui uma ID de sessão no cabeçalho Local. A ID de sessão é uma parte essencial das informações na resposta, pois é necessária para todas as chamadas de rastreamento subsequentes. Depois de um retorno bem-sucedido de uma [Solicitação de sessões](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md), você pode prosseguir com a implementação do rastreamento de vídeo usando a API do MA no reprodutor de vídeo.
