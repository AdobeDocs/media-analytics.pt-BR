---
seo-title: Rastrear o conteúdo baixado
title: Rastrear o conteúdo baixado
uuid: 0718689 d -9602-4 e 3 f -833 c -8297 aae 1 d 909
translation-type: tm+mt
source-git-commit: b9298de98eeb85c0e2ea0a456c98eac479f43b51

---


# Rastrear o conteúdo baixado{#track-downloaded-content}

## Visão geral {#section_hcy_3pk_cfb}

O recurso Conteúdo baixado fornece a capacidade de rastrear o consumo de mídia enquanto um usuário está offline. Por exemplo, um usuário baixa e instala um aplicativo em um dispositivo móvel. Em seguida, ele baixa o conteúdo usando o aplicativo no armazenamento local do dispositivo. Para rastrear esses dados baixados, a Adobe desenvolveu o recurso Conteúdo baixado. Com esse recurso, quando o usuário reproduz conteúdo a partir do armazenamento de um dispositivo, os dados são armazenados no dispositivo, independentemente da conectividade do dispositivo. Quando o usuário concluir a sessão de reprodução e o dispositivo retornar on-line, as informações de rastreamento armazenadas serão enviadas para o back-end da API da coleção de mídia dentro de uma única carga. Lá, o processamento e o relatório são executados como normal na API de coleta de mídia.

Contraste as duas abordagens:

* Online

   Com essa abordagem em tempo real, o player de mídia envia dados de rastreamento em cada evento do player e envia imagens a cada dez segundos (a cada um segundo para anúncios), um por um ao back-end.

* Offline (recurso Conteúdo baixado)

   Com essa abordagem de processamento em lote, os mesmos eventos de sessão precisam ser gerados, mas são armazenados no dispositivo até serem enviados para o back-end como uma única sessão (veja exemplo abaixo).

Cada abordagem tem suas vantagens e desvantagens:
* O cenário online acompanha em tempo real; isso requer uma verificação de conectividade antes de cada chamada de rede.
* O cenário offline (recurso Conteúdo baixado) precisa apenas de uma verificação de conectividade de rede, mas também exige um rastreamento de memória maior no dispositivo.

## Implementação {#section_jhp_jpk_cfb}

### Esquemas de evento

O recurso Conteúdo baixado é simplesmente a versão offline da On-line Collection Collection API (padrão), de modo que os dados do evento que seus lotes e envios enviam para o back-end devem usar os mesmos esquemas de evento usados quando você faz chamadas online. Para obter informações sobre esses esquemas, consulte:
* [Visão geral;](/help/media-collection-api/mc-api-overview.md)
* [Validar solicitações de evento](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### Ordem dos eventos

* O primeiro evento na carga em lote deve ser `sessionStart` como de costume com a API de coleta de mídia.
* **Você deve incluir`media.downloaded: true`** nos parâmetros padronizados de metadados (`params` chave) no `sessionStart` evento para indicar ao back-end que está enviando conteúdo baixado. Se esse parâmetro não estiver presente ou estiver definido como falso quando você enviar dados baixados, a API retornará um código de resposta 400 (Solicitação incorreta). Esse parâmetro faz a distinção entre conteúdo baixado e ativo para o back-end. (Note that if `media.downloaded: true` is set on a live session, this will likewise result in a 400 response from the API.)
* É da responsabilidade da implementação armazenar corretamente os eventos do reprodutor na ordem em que aparecem.

### Códigos de resposta

* 201 - Criado: solicitação bem-sucedida; os dados são válidos e a sessão foi criada e será processada.
* 400 - Solicitação inválida; a validação do esquema falhou, todos os dados são descartados, nenhum dado da sessão será processado.

## Integração com o Adobe Analytics {#section_cty_kpk_cfb}

Ao calcular chamadas de início/fechamento do Analytics para o cenário de conteúdo baixado, o back-end define um campo extra do Analytics chamado `ts.` Esses são carimbos de data e hora para o primeiro e último eventos recebidos (início e conclusão). Este mecanismo permite que uma sessão de mídia concluída seja colocada no ponto correto no tempo (ou seja, mesmo que o usuário não volte on-line por vários dias, a sessão de mídia deve ter ocorrido no momento em que o conteúdo realmente foi visualizado). Você deve ativar esse mecanismo no Adobe Analytics criando um _conjunto de relatórios opcionais de carimbo de data e hora._ Para ativar o conjunto de relatórios opcionais de carimbo de data e hora, consulte [Carimbos de data e hora opcionais.](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/timestamp-optional.html)

## Comparação de sessões de amostra {#section_qnk_lpk_cfb}

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

