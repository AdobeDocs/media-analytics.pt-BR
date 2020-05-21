---
title: Implementação e Relatórios
description: Este tópico descreve como implementar o recurso de rastreamento de estado do player, incluindo .
translation-type: tm+mt
source-git-commit: b0bfe74d1f6083e700dbf98f504a17518bd19ecb
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# Implementação e relatórios

Durante uma sessão de reprodução, cada ocorrência de estado (start para ponta) deve ser rastreada individualmente. O SDK de mídia e a API de coleta de mídia fornecem novos métodos de rastreamento para esse recurso.

O SDK de mídia inclui dois novos métodos para rastreamento de estado personalizado:

`trackStateStart("state_name")`

`trackStateClose("state_name")`


A API Media Collection inclui dois novos eventos que têm &quot;media.stateName&quot; como o parâmetro obrigatório:

`stateStart` e `stateEnd`

## Implementação do SDK de mídia

Start de estado do player

```
// StateStart (ex: Mute is switched on)
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
tracker.trackEvent(ADB.Media.Event.StateStart, stateObject);
```

O estado do player termina

```
// StateEnd (ex: Mute is switched off)
tracker.trackEvent(ADB.Media.Event.StateEnd, stateObject);
```


## Implementação da API do Media Collection

Start de estado do player

```
// StateStart (ex: Mute is switched on)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "stateStart",
  "params": {
    "media.state.name": "mute"
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

O estado do player termina

```
// StateEnd (ex: Mute is switched off)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events

{
  "eventType": "stateEnd",
  "params": {
    "media.state.name": "mute"
  },
  "playerTime": {
    "playhead": 600,
    "ts": 1569999730638
  }
}
```

## Métricas de estado

As métricas fornecidas para cada estado individual são computadas e enviadas para o Adobe Analytics como parâmetros de dados de contexto e armazenadas para fins de relatórios. Três métricas estão disponíveis para cada estado:

* `a.media.states.(media.state.name).set = true` — Definido como true se o estado foi definido pelo menos uma vez para cada reprodução específica de um fluxo.
* `a.media.states.(media.state.name).count = 4` — Identifica o número de ocorrências de um estado durante cada reprodução individual de um fluxo
* `a.media.states.(media.state.name).time = 240` — Identifica a duração total do estado em segundos para cada reprodução individual de um fluxo

## Relatórios

Todas as métricas de estado podem ser usadas para qualquer visualização ou componente do relatórios (segmento, métricas calculadas).
TBD - verificar fonte/wiki para obter informações atualizadas - para captura de tela do AW

## Importar métricas declaradas do player para a Adobe Experience Platform

Os dados armazenados no Analytics podem ser usados para qualquer finalidade e as métricas de estado do player podem ser importadas para a Adobe Experience Platform usando o XDM e usadas com o Customer Journey Analytics. As propriedades de estado padrão têm propriedades específicas, enquanto os estados personalizados são propriedades disponíveis por meio dos eventos personalizados. Para obter informações adicionais, consulte a lista de propriedades para identidades XDM na LISTA ?LINK TO METRIC?.
