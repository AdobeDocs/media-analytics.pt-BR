---
seo-title: Rastrear o conteúdo baixado
title: Rastrear o conteúdo baixado
uuid: 0718689 d -9602-4 e 3 f -833 c -8297 aae 1 d 909
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Rastrear o conteúdo baixado{#track-downloaded-content}

## Visão geral {#section_hcy_3pk_cfb}

A API do conteúdo baixado tem a capacidade de rastrear o consumo de mídia enquanto o usuário está offline. Por exemplo, um usuário baixa e instala um aplicativo em um dispositivo móvel. Em seguida, ele baixa o conteúdo usando o aplicativo no armazenamento local do dispositivo. Para rastrear esses dados baixados, a Adobe desenvolveu a API do conteúdo baixado. Com essa API, quando o usuário reproduz o conteúdo do armazenamento de um dispositivo, os dados de rastreamento são armazenados no dispositivo, independentemente da conectividade dele. Quando o usuário concluir a sessão de reprodução e o dispositivo estiver online, as informações de rastreamento armazenadas serão enviadas para o back-end da API da coleção de mídia dentro de uma única carga. A partir daí, o processamento e os relatórios continuam normalmente na API da coleção de mídia, na qual essa API é baseada.

Contraste as duas abordagens:

* API da coleção de mídia

   Com essa abordagem em tempo real, o player de mídia envia dados de rastreamento em cada evento do player e envia imagens a cada dez segundos (a cada um segundo para anúncios), um por um ao back-end.

* API do conteúdo baixado

   Com essa abordagem de processamento em lote, os mesmos eventos de sessão precisam ser gerados, mas armazenados no dispositivo até serem enviados para o back-end como uma única sessão (consulte exemplo abaixo).

Cada abordagem tem suas vantagens e desvantagens: a API da coleção de mídia rastreia em tempo real, mas isso requer uma verificação de conectividade antes de cada chamada de rede; a API do conteúdo baixado só precisa de uma verificação de conectividade de rede, mas também exige um espaço maior de memória no dispositivo.

## Implementação {#section_jhp_jpk_cfb}

### Esquemas de evento

A API de conteúdo baixado baseia-se na API de coleta de mídia, de modo que os dados do evento que seus lotes e enviados são enviados exigem que os mesmos esquemas de eventos sejam usados como na API de coleta de mídia. For information on these schemas, see: [Overview;](/help/media-collection-api/mc-api-overview.md) and [Validating event requests.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### Ordem dos eventos

* O primeiro evento na carga em lote deve ser `sessionStart`.
* You must include `media.downloaded: true` in the standard metadata parameters ( `params` key) on the `sessionStart` event. Se este parâmetro não estiver presente ou for definido como false, a API do conteúdo baixado retornará um código de resposta 400 (solicitação inválida). Isso é para que o back-end possa distinguir entre o conteúdo baixado e ao vivo, e processá-lo de acordo. (Observe que se `media.downloaded: true` for configurado em uma sessão em tempo real, isso também resultará em uma resposta 400 da API da coleção de mídia.)

* É da responsabilidade da implementação armazenar corretamente os eventos do reprodutor na ordem em que aparecem.

### Códigos de resposta

* 201 - Criado: solicitação bem-sucedida; os dados são válidos e a sessão foi criada e será processada.
* 400 - Solicitação inválida; a validação do esquema falhou, todos os dados são descartados, nenhum dado da sessão será processado.

## Integração com o Adobe Analytics {#section_cty_kpk_cfb}

When computing the Analytics start/close calls for the downloaded content scenario, the back-end sets an extra Analytics field called `ts`. Esses são carimbos de data e hora para o primeiro e último eventos recebidos (início e conclusão). Este mecanismo permite que uma sessão de mídia concluída seja colocada no ponto correto no tempo (ou seja, mesmo que o usuário não volte on-line por vários dias, a sessão de mídia deve ter ocorrido no momento em que o conteúdo realmente foi visualizado). Você deve ativar esse mecanismo no Adobe Analytics criando um *conjunto de relatórios opcionais de carimbo de data e hora*. Para ativar o conjunto de relatórios opcionais de carimbo de data e hora, consulte [Carimbos de data e hora opcionais.](https://marketing.adobe.com/resources/help/en_US/reference/timestamp-optional.html)

## Comparação de sessões de amostra {#section_qnk_lpk_cfb}

```
[url]/api/v1/sessions
```

### API da coleção de mídia

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

### API do conteúdo baixado

```
[{ 
    eventType: "sessionStart", 
    playerTime:{playhead: 0, ts: 1529997923478},  
    params:{
        "media.downloaded": true
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

