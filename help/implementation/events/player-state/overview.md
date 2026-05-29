---
title: Rastrear estados do player
description: Saiba mais sobre os eventos de estado do player e como rastrear os estados de tela cheia, mudo, legendas ocultas, picture-in-picture e em foco.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 12%

---


# Rastrear estados do player

Os eventos de estado do player rastreiam como os visualizadores interagem com os controles do player em toda a sessão. Elas são opcionais e não são necessárias para implementações de rastreamento de mídia principal. Os cinco estados rastreáveis são: `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture` e `inFocus`.

Os eventos de estado do player são úteis para entender o uso do recurso de acessibilidade, como a frequência com que os visualizadores ativam as legendas ocultas ou a função mudo. Elas também revelam padrões de comportamento de visualização como tela cheia versus visualização em linha e multitarefa picture-in-picture.

## Eventos do player

| Evento do reprodutor | Ação |
| --- | --- |
| O reprodutor entra em um estado | Início do Estado da Chamada |
| O player sai de um estado | Fim do estado da chamada |

## Estados padrão e personalizados

Cinco estados padrão do player estão disponíveis e você pode adicionar seus próprios estados personalizados.

| Nome do estado padrão | Constante do SDK de mídia | Nome da API da coleção de mídia |
|----|----|----|
| Tela cheia | `ADB.Media.PlayerState.Fullscreen` | `fullScreen` |
| Legendas ocultas | `ADB.Media.PlayerState.ClosedCaptioning` | `closedCaptioning` |
| Mudo | `ADB.Media.PlayerState.Mute` | `mute` |
| Picture in picture | `ADB.Media.PlayerState.PictureInPicture` | `pictureInPicture` |
| Em foco | `ADB.Media.PlayerState.InFocus` | `inFocus` |

Consulte [Variáveis de estado do player](/help/implementation/variables/player-state/) para obter a referência completa da variável, incluindo caminhos XDM e definições de métricas.

**Estados personalizados:** você pode criar estados personalizados para capturar comportamentos de player adicionais específicos ao seu aplicativo. Consulte a [Referência da API de Mídia: `createStateObject`](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/) para obter detalhes sobre como criar objetos de estado personalizado.

## Etapas da implementação

1. **Chame [Início do estado](state-start.md)** quando o player entrar em qualquer um dos cinco estados rastreáveis. Vários estados podem estar ativos ao mesmo tempo e vários estados podem ser iniciados na mesma chamada de evento.
1. **Chame [Fim do estado](state-end.md)** quando o player sair de um estado. Vários estados podem ser encerrados na mesma chamada de evento e estados podem ser iniciados e encerrados juntos em uma única chamada.

## Diretrizes

* Uma sessão de vídeo é limitada a 10 estados do player.
* Qualquer combinação de estados é permitida.
* Se vários estados do player forem transmitidos, apenas os primeiros 10 serão retidos e encaminhados para o back-end de mídia.
* O máximo de 10 estados se aplica a todos os estados, independentemente de estarem abertos ou fechados.
* Um estado pode ser iniciado e finalizado várias vezes e contado como um único estado. Por exemplo, `closedCaptioning` pode ser iniciado e parado cinco vezes, mas conta como um estado.
* O estado do player é calculado em todos os estados de reprodução (sem divisão).
* Os estados do player são capturados para cada sessão de reprodução individual. O estado do player não é calculado entre as reproduções.
* O conhecimento do status do aplicativo não é mantido depois que um estado é interrompido. Após o término de um estado, ele deve ser iniciado novamente para continuar o rastreamento.

## Atualização de vários estados simultaneamente

Em plataformas baseadas em XDM, várias alterações de estado podem ser armazenadas em lote em uma única chamada `statesUpdate` usando matrizes em `statesStart` e `statesEnd`. Nos SDKs móveis, cada alteração de estado requer uma chamada separada.

Os exemplos a seguir começam juntos com mudo e picture-in-picture, depois fazem a transição para tela cheia.

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

```javascript
// t0 — start mute and picture-in-picture together
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "mute" }, { name: "pictureInPicture" }],
      sessionID: "{sid}",
      playhead: 0
    }
  }
});

// t1 — end mute and picture-in-picture; start full screen
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "mute" }, { name: "pictureInPicture" }],
      statesStart: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 0
    }
  }
});

// t2 — end full screen
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

O Mobile SDK não oferece suporte a agrupamento — envie uma chamada separada para cada alteração de estado.

```swift
// t0 — start mute and picture-in-picture
let muteState = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.MUTE)
let pipState = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.PICTURE_IN_PICTURE)
tracker.trackEvent(event: MediaEvent.StateStart, info: muteState, metadata: nil)
tracker.trackEvent(event: MediaEvent.StateStart, info: pipState, metadata: nil)

// t1 — end mute and picture-in-picture; start full screen
tracker.trackEvent(event: MediaEvent.StateEnd, info: muteState, metadata: nil)
tracker.trackEvent(event: MediaEvent.StateEnd, info: pipState, metadata: nil)
let fullscreenState = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)
tracker.trackEvent(event: MediaEvent.StateStart, info: fullscreenState, metadata: nil)

// t2 — end full screen
tracker.trackEvent(event: MediaEvent.StateEnd, info: fullscreenState, metadata: nil)
```

>[!TAB Android]

O Mobile SDK não oferece suporte a agrupamento — envie uma chamada separada para cada alteração de estado.

```kotlin
// t0 — start mute and picture-in-picture
val muteState = Media.createStateObject(MediaConstants.PlayerState.MUTE)
val pipState = Media.createStateObject(MediaConstants.PlayerState.PICTURE_IN_PICTURE)
tracker.trackEvent(Media.Event.StateStart, muteState, null)
tracker.trackEvent(Media.Event.StateStart, pipState, null)

// t1 — end mute and picture-in-picture; start full screen
tracker.trackEvent(Media.Event.StateEnd, muteState, null)
tracker.trackEvent(Media.Event.StateEnd, pipState, null)
val fullscreenState = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)
tracker.trackEvent(Media.Event.StateStart, fullscreenState, null)

// t2 — end full screen
tracker.trackEvent(Media.Event.StateEnd, fullscreenState, null)
```

>[!TAB Roku]

```brightscript
' t0 — start mute and picture-in-picture together
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesStart": [{"name": "mute"}, {"name": "pictureInPicture"}],
            "playhead": 0
        }
    }
})

' t1 — end mute and picture-in-picture; start full screen
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{"name": "mute"}, {"name": "pictureInPicture"}],
            "statesStart": [{"name": "fullscreen"}],
            "playhead": 0
        }
    }
})

' t2 — end full screen
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{"name": "fullscreen"}],
            "playhead": 0
        }
    }
})
```

>[!TAB API do Media Edge]

```sh
# t0 — start mute and picture-in-picture together
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{"name": "mute"}, {"name": "pictureInPicture"}],
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-01-01T00:00:00+00:00"
    }
  }]
}'

# t1 — end mute and picture-in-picture; start full screen
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesEnd": [{"name": "mute"}, {"name": "pictureInPicture"}],
        "statesStart": [{"name": "fullscreen"}],
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-01-01T00:01:00+00:00"
    }
  }]
}'

# t2 — end full screen
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesEnd": [{"name": "fullscreen"}],
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-01-01T00:02:00+00:00"
    }
  }]
}'
```

>[!ENDTABS]

## Tipos de implementação herdada (somente Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Alterações de vários estados exigem chamadas separadas.

```javascript
// t0 — start mute and picture-in-picture
var muteState = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
var pipState = ADB.Media.createStateObject(ADB.Media.PlayerState.PictureInPicture);
tracker.trackPlayerStateStart(muteState);
tracker.trackPlayerStateStart(pipState);

// t1 — end mute and picture-in-picture; start full screen
tracker.trackPlayerStateEnd(muteState);
tracker.trackPlayerStateEnd(pipState);
var fullscreenState = ADB.Media.createStateObject(ADB.Media.PlayerState.FullScreen);
tracker.trackPlayerStateStart(fullscreenState);

// t2 — end full screen
tracker.trackPlayerStateEnd(fullscreenState);
```

>[!TAB Chromecast]

Alterações de vários estados exigem chamadas separadas.

```javascript
// t0 — start mute and picture-in-picture
var muteState = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.Mute);
var pipState = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.PictureInPicture);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, muteState, null);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, pipState, null);

// t1 — end mute and picture-in-picture; start full screen
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, muteState, null);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, pipState, null);
var fullscreenState = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.FullScreen);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, fullscreenState, null);

// t2 — end full screen
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, fullscreenState, null);
```

>[!TAB API da coleção de mídia]

```json
// t0 — start mute and picture-in-picture together
{
  "eventType": "statesUpdate",
  "params": {
    "statesStart": [
      { "media.state.name": "mute" },
      { "media.state.name": "pictureInPicture" }
    ]
  },
  "playerTime": { "playhead": 0, "ts": 1569999130627 }
}

// t1 — end mute and picture-in-picture; start full screen
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [
      { "media.state.name": "mute" },
      { "media.state.name": "pictureInPicture" }
    ],
    "statesStart": [
      { "media.state.name": "fullScreen" }
    ]
  },
  "playerTime": { "playhead": 0, "ts": 1569999230627 }
}

// t2 — end full screen
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [{ "media.state.name": "fullScreen" }]
  },
  "playerTime": { "playhead": 0, "ts": 1569999330627 }
}
```

>[!ENDTABS]

## Pausa longa

Quando uma sessão de vídeo tem uma duração de pausa superior a 30 minutos, a API exige uma nova sessão. Gere uma nova ID de sessão e retenha todos os estados ativos para que eles possam ser restaurados com `stateStart` eventos logo após a nova chamada `sessionStart`.

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd`

Depois que `sessionEnd` for enviado, inicie uma nova sessão e reenvie imediatamente os estados ativos:

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

## Métricas de estado

Três métricas são computadas para cada estado rastreado e enviadas ao Adobe Analytics na chamada de fechamento de mídia:

| Métrica | Chave de dados de contexto | Descrição |
| --- | --- | --- |
| Estado definido | `a.media.states.[state.name].set = true` | `true` se o estado foi definido pelo menos uma vez durante a reprodução |
| Contagem de estados | `a.media.states.[state.name].count = 4` | Número de vezes que o estado ocorreu durante a reprodução |
| Hora do estado | `a.media.states.[state.name].time = 240` | Tempo total (segundos) gasto no estado durante a reprodução |
