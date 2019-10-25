---
seo-title: Rastrear o conteúdo baixado
title: Rastrear o conteúdo baixado
uuid: 0718689d-9602-4e3f-833c-8297aae1d909
translation-type: tm+mt
source-git-commit: ffb97a0162e0bb609ea427afab81e4d8b532f20b

---


# Rastrear o conteúdo baixado{#track-downloaded-content}

## Visão geral {#overview}

O recurso Conteúdo baixado fornece a capacidade de rastrear o consumo de mídia enquanto o usuário está offline. Por exemplo, um usuário baixa e instala um aplicativo em um dispositivo móvel. Em seguida, ele baixa o conteúdo usando o aplicativo no armazenamento local do dispositivo. Para rastrear esses dados baixados, a Adobe desenvolveu o recurso Conteúdo baixado. Com esse recurso, quando o usuário reproduz o conteúdo do armazenamento de um dispositivo, os dados de rastreamento são armazenados no dispositivo, independentemente da conectividade do dispositivo. Quando o usuário conclui a sessão de reprodução e o dispositivo retorna online, as informações de rastreamento armazenadas são enviadas para o back-end da API de coleta de mídia em uma única carga. A partir daí, o processamento e o relatório continuam normalmente na API Media Collection.

Compare as duas abordagens:

* Online

   Com essa abordagem em tempo real, o player de mídia envia dados de rastreamento sobre cada evento do player e envia ping de rede a cada dez segundos (a cada segundo para anúncios), um por um para o back-end.

* Offline (recurso Conteúdo baixado)

   Com essa abordagem de processamento em lote, os mesmos eventos de sessão precisam ser gerados, mas são armazenados no dispositivo até que sejam enviados para o back-end como uma única sessão (consulte o exemplo abaixo).

Cada abordagem tem suas vantagens e desvantagens:
* O cenário online é rastreado em tempo real; isso requer uma verificação de conectividade antes de cada chamada de rede.
* O cenário offline (recurso Conteúdo baixado) precisa apenas de uma verificação de conectividade de rede, mas também requer um espaço maior de memória no dispositivo.

## Implementação {#implementation}

### Esquemas de eventos

O recurso Conteúdo baixado é simplesmente a versão offline da API (padrão) de coleta de mídia online, de modo que os dados de evento que seu player acumula e envia para o back-end devem usar os mesmos esquemas de evento que você usa quando faz chamadas online. Para obter informações sobre esses esquemas, consulte:
* [Visão geral;](/help/media-collection-api/mc-api-overview.md)
* [Validar solicitações de evento](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### Ordem dos eventos

* O primeiro evento na carga do lote deve ser `sessionStart` como de costume com a API Media Collection.
* **Você deve incluir`media.downloaded: true`** os parâmetros de metadados padrão (`params` chave) no `sessionStart` evento para indicar ao back-end que você está enviando o conteúdo baixado. Se esse parâmetro não estiver presente ou estiver definido como falso quando você enviar dados baixados, a API retornará um código de resposta 400 (solicitação incorreta). Esse parâmetro distingue o conteúdo baixado do conteúdo em tempo real do back-end. (Note that if `media.downloaded: true` is set on a live session, this will likewise result in a 400 response from the API.)
* É da responsabilidade da implementação armazenar corretamente os eventos do reprodutor na ordem em que aparecem.

### Códigos de resposta

* 201 - Criado: solicitação bem-sucedida; os dados são válidos e a sessão foi criada e será processada.
* 400 - Solicitação inválida; a validação do esquema falhou, todos os dados são descartados, nenhum dado da sessão será processado.

## Integração com o Adobe Analytics {#integration-with-adobe-analtyics}

Ao calcular as chamadas de início/fechamento do Analytics para o cenário de conteúdo baixado, o back-end define um campo adicional do Analytics chamado `ts.` Estes são carimbos de data e hora para o primeiro e o último evento recebido (início e conclusão). Esse mecanismo permite que uma sessão de mídia concluída seja colocada no ponto no tempo correto (isto é, mesmo se o usuário não voltar online por vários dias, a sessão de mídia é reportada como ocorrida no momento em que o conteúdo foi realmente exibido). Você deve ativar esse mecanismo no Adobe Analytics criando um _conjunto de relatórios opcionais de carimbo de data e hora._ Para ativar o conjunto de relatórios opcionais de carimbo de data e hora, consulte [Carimbos de data e hora opcionais.](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/timestamp-optional.html)

## Comparação de sessões de amostra {#sample-session-comparison}

```
[url]/api/v1/sessions
```

### Conteúdo online

```
{ 
  eventType: "sessionStart", 
  playerTime: { 
    playhead: 0,  
    ts: 1529997923478},  
  params: { /* Standard metadata parameters as documented */ },  
  customMetadata: { /* Custom metadata parameters as documented */ },  
  qoeData: { /* QoE parameters as documented */ } 
}
```

### Conteúdo baixado

```
[{ 
    eventType: "sessionStart", 
    playerTime:{
      playhead: 0, 
      ts: 1529997923478},  
    params:{
        "media.downloaded": true
        ...
    }, 
    customMetadata:{},  
    qoeData:{} 
}, 
    {eventType: "play", playerTime:
        {playhead: 0,  ts: 1529997928174}}, 
    {eventType: "ping", playerTime:
        {playhead: 10, ts: 1529997937503}}, 
    {eventType: "ping", playerTime:
        {playhead: 20, ts: 1529997947533}}, 
    {eventType: "ping", playerTime:
        {playhead: 30, ts: 1529997957545},}, 
    {eventType: "sessionComplete", playerTime:
        {playhead: 35, ts: 1529997960559} 
}]
```

