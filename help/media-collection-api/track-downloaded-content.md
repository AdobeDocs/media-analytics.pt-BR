---
title: Rastrear o conteúdo baixado
description: null
uuid: 0718689d-9602-4e3f-833c-8297aae1d909
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Rastrear o conteúdo baixado {#track-downloaded-content}

## Visão geral {#overview}

O recurso Conteúdo baixado tem a capacidade de rastrear o consumo de mídia enquanto o usuário está offline. Por exemplo, um usuário baixa e instala um aplicativo em um dispositivo móvel. O usuário então baixa o conteúdo usando o aplicativo no armazenamento local do dispositivo. Para rastrear esses dados baixados, a Adobe desenvolveu o recurso Conteúdo baixado. Com esse recurso, quando o usuário reproduz o conteúdo do armazenamento de um dispositivo, os dados de rastreamento são armazenados no dispositivo, independentemente da conectividade dele. Quando o usuário finaliza a sessão de reprodução e o dispositivo volta ao modo online, as informações de rastreamento armazenadas são enviadas ao back-end da API Media Collection, dentro de uma única carga. A partir daí, o processamento e o relatório continuam normalmente na API Media Collection.

Compare as duas abordagens:

* Online

   Com esta abordagem em tempo real, o reprodutor de mídia envia dados de rastreamento sobre cada evento do reprodutor e envia pings de rede a cada dez segundos (a cada segundo para anúncios), um por um, para o back-end.

* Offline (recurso Conteúdo baixado)

   Com essa abordagem de processamento em lote, os mesmos eventos de sessão precisam ser gerados, mas são armazenados no dispositivo até que sejam enviados para o back-end como uma única sessão (consulte o exemplo abaixo).

Cada abordagem tem suas vantagens e desvantagens:
* O cenário online é rastreado em tempo real; isso requer uma verificação de conectividade antes de cada chamada de rede.
* O cenário offline (recurso Conteúdo baixado) precisa apenas de uma verificação de conectividade de rede, mas também requer um espaço maior de memória no dispositivo.

## Implementação {#implementation}

### Esquemas de eventos

O recurso Conteúdo baixado é simplesmente a versão offline (padrão) da API Media Collection online, de modo que os dados de evento que seu reprodutor acumula e envia para o back-end devem usar os mesmos esquemas de evento que você usa quando faz chamadas online. Para obter informações sobre esses esquemas, consulte:
* [Visão geral;](/help/media-collection-api/mc-api-overview.md)
* [Validar solicitações de evento](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### Ordem dos eventos

* O primeiro evento na carga do lote deve ser `sessionStart` como de costume com a API Media Collection.
* **Você deve incluir`media.downloaded: true`** nos parâmetros de metadados padrão (`params`chave) no evento`sessionStart`para indicar ao back-end que você está enviando o conteúdo baixado. Se este parâmetro não estiver presente ou for definido como &quot;false&quot; quando você enviar o conteúdo baixado, a API retornará um código de resposta 400 (Solicitação inválida). Esse parâmetro distingue o conteúdo baixado do conteúdo em tempo real para o back-end. (Observe que se`media.downloaded: true`estiver configurado em uma sessão em tempo real, isso também resultará em uma resposta 400 da API.)
* É da responsabilidade da implementação armazenar corretamente os eventos do reprodutor na ordem em que aparecem.

### Códigos de resposta

* 201 - Criado: Solicitação bem-sucedida; os dados são válidos e a sessão foi criada e será processada.
* 400 - Solicitação incorreta; falha na validação do schema, todos os dados são descartados, nenhum dado de sessão será processado.

## Integração com o Adobe Analytics {#integration-with-adobe-analtyics}

Ao calcular as chamadas de início/fechamento do Analytics para o cenário de conteúdo baixado, o back-end define um campo adicional do Analytics chamado `ts.` Estes são carimbos de data e hora para o primeiro e o último evento recebido (início e conclusão). Esse mecanismo permite que uma sessão de mídia concluída seja colocada no momento correto (ou seja, mesmo que o usuário não volte a ficar online por vários dias, a sessão de mídia informa que ocorreu no momento em que o conteúdo foi realmente visualizado). Você deve ativar esse mecanismo no Adobe Analytics criando um _conjunto de relatórios opcionais de carimbo de data e hora._ Para ativar o conjunto de relatórios opcionais de carimbo de data e hora, consulte [Carimbos de data e hora opcionais.](https://docs.adobe.com/content/help/pt-BR/analytics/admin/admin-tools/timestamp-optional.html)

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

