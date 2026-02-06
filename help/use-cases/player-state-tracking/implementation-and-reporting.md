---
title: Implementação e Relatórios
description: 'Saiba como implementar o recurso de rastreamento do estado do player, incluindo:'
exl-id: 19a97c9b-14d1-4f11-bb0a-3a1ad6f949da
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 78%

---

# Implementação e relatórios

Durante uma sessão de reprodução, cada ocorrência de estado (início ao fim) deve ser rastreada individualmente. O Media SDK e a API de coleção de mídia fornecem métodos de rastreamento para esse recurso.

O Media SDK inclui dois métodos para rastreamento de estado personalizado:

`trackStateStart("state_name")`

`trackStateClose("state_name")`


A API da coleção de mídia inclui dois eventos que têm `media.stateName` como o parâmetro obrigatório:

`stateStart` e `stateEnd`

## Implementação do SDK de mídia

Início do estado do player

```
// StateStart (ex: Mute is switched on)
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
tracker.trackEvent(ADB.Media.Event.StateStart, stateObject);
```

Encerramento do estado do player

```
// StateEnd (ex: Mute is switched off)
tracker.trackEvent(ADB.Media.Event.StateEnd, stateObject);
```


## Implementação da API da coleção de mídia

Início do estado do player

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

Encerramento do estado do player

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

* `a.media.states.[state.name].set = true` — Definido como true se o estado foi definido pelo menos uma vez para cada reprodução específica de um fluxo.
* `a.media.states.[state.name].count = 4` — Identifica o número de ocorrências de um estado durante cada reprodução individual de um fluxo
* `a.media.states.[state.name].time = 240` — Identifica a duração total do estado em segundos para cada reprodução individual de um fluxo

## Geração de relatórios

Todas as métricas do estado do player podem ser usadas para qualquer visualização de relatórios disponível no Analysis Workspace ou em um componente (segmento, métricas calculadas) assim que um conjunto de relatórios é habilitado para o rastreamento do estado do player. Essas métricas podem ser ativadas no Admin Console para cada relatório individual usando a Configuração do relatórios de mídia (Editar configurações > Gerenciamento de mídia > Relatórios de mídia).

![](assets/report-setup.png)

No Analysis Workspace, todas as novas propriedades estão localizadas no painel de métricas. Por exemplo, você pode pesquisar por `full screen` para visualizar os dados do estado de tela cheia no painel de métricas.

![](assets/full-screen-report.png)

## Importar métricas declaradas do player para a Adobe Experience Platform

Os dados armazenados no Analytics podem ser usados para qualquer finalidade e as métricas do estado do player podem ser importadas para a Adobe Experience Platform usando o XDM e usadas com o Customer Journey Analytics. As propriedades de estado padrão têm propriedades específicas, enquanto os estados personalizados são propriedades disponíveis por meio dos eventos personalizados. Para obter mais informações sobre as propriedades de estado padrão, consulte a seção *Lista de propriedades para identidades XDM* na página [Parâmetros do estado do player](/help/implementation/variables/player-state-parameters.md).
