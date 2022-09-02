---
title: Atualização de vários estados do player de uma só vez
description: Este tópico descreve o recurso Rastreamento de vários estados do player.
exl-id: a77bc882-ac03-40b4-ac64-87f26a09707b
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 7a28674024739593431a942d5e0a498294bbe793
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 10%

---

# Rastreamento de vários estados do player

Há situações em que dois estados do player começam e terminam ao mesmo tempo ou quando o fim de um estado também é o início de outro estado. Observando o exemplo a seguir:

![Vários estados do player](assets/multiple-player-states.svg)

A implementação atual permite ambos os cenários:
- `stateStart(pictureInPicture)` - t0
- `stateStart(mute)` - t0
- `stateEnd(mute)` - t1
- `stateEnd(pictureInPicture)` - t1
- `stateStart(fullScreen)` - t1
- `stateEnd(fullScreen)` - t2

No entanto, o cliente precisa emitir muitas `stateStart` e `stateEnd` para sinalizar várias alterações de estado simultâneas. Para otimizar esse comportamento comum, um novo `statesUpdate` O tipo de evento foi implementado, o que encerra uma lista de estados e inicia uma lista de novos estados.

Uso da nova `statesUpdate` , a lista acima de eventos se torna:
- `statesUpdate(statesEnd=[], statesStart=[pictureInPicture, mute])` - t0
- `statesUpdate(statesEnd=[mute, pictureInPicture], statesStart=[fullScreen])` - t1
- `statesUpdate(statesEnd=[fullScreen], statesStart=[])` - t2

O número de chamadas de atualizações de estado foi reduzido de 6 para 3 para o mesmo comportamento. O último evento também poderia ter sido simples `stateEnd(fullScreen)`.

## Implementação da API da coleção de mídia

Exemplos:

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

Não há implementação do SDK do Media.
