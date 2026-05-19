---
title: Atualização de vários estados do player de uma só vez
description: Este tópico descreve o recurso Rastreamento de vários estados do player.
feature: Streaming Media
role: User, Admin, Developer
exl-id: 7a512a81-a6d1-4d0c-a4fe-91e9b11419db
TQID: https://experienceleague.adobe.com/fKpr-TULVqDnK7j07e66gd-kiFLYzf7D2GmoGtP8Aqg
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 186
ht-degree: 80%

---

# Rastreamento de vários estados do player

Às vezes, dois estados do player começam e terminam ao mesmo tempo ou o fim de um estado também é o início de outro estado, como mostrado na imagem a seguir:

![Vários estados do player](assets/multiple-player-states.png)

A implementação atual permite ambos os cenários:
- `stateStart(pictureInPicture)` - t0
- `stateStart(mute)` - t0
- `stateEnd(mute)` - t1
- `stateEnd(pictureInPicture)` - t1
- `stateStart(fullScreen)` - t1
- `stateEnd(fullScreen)` - t2

No entanto, isso requer que você emita vários eventos `stateStart` e `stateEnd` para sinalizar várias alterações de estado simultâneas. Entrada
para otimizar esse comportamento comum, um novo tipo de evento `statesUpdate` foi implementado, que encerra uma lista de estados
e inicia uma lista de novos estados.

Ao utilizar o novo evento `statesUpdate`, a lista de eventos acima se torna:
- `statesUpdate(statesEnd=[], statesStart=[pictureInPicture, mute])` - t0
- `statesUpdate(statesEnd=[mute, pictureInPicture], statesStart=[fullScreen])` - t1
- `statesUpdate(statesEnd=[fullScreen], statesStart=[])` - t2

O número de chamadas de atualizações de estado foi reduzido de seis para três para o mesmo comportamento. O último evento
também poderia ter sido um simples `stateEnd(fullScreen)`.

## Implementação da API da coleção de mídia {#mpst-api}

Você pode usar a API de coleção de mídia para implementar o monitoramento de vários estados do player.

### Exemplo

A seguir, veja um exemplo de implementação da API de coleção de mídia para monitoramento de vários estados do player.

```
// statesUpdate (ex: mute and pictureInPicture are switched on)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "statesUpdate",
  "params": {
    "statesStart": [
      {
        "media.state.name": "mute"
      },
      {
        "media.state.name": "pictureInPicture"
      }
    ]
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

```
// statesUpdate (ex: mute and pictureInPicture are switched off, fullScreen is switched on)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [
      {
        "media.state.name": "mute"
      },
      {
        "media.state.name": "pictureInPicture"
      }
    ],
    "statesStart": [
      {
        "media.state.name": "fullScreen"
      }
    ]
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

```
// statesUpdate (ex: fullScreen is switched off)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [
      {
        "media.state.name": "fullScreen"
      }
    ]
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

## Implementação do SDK de mídia

Não há implementação do SDK de mídia.
