---
title: Exemplos de rastreamento do estado do player
description: Este tópico inclui exemplos do recurso de Rastreamento do estado do player.
translation-type: tm+mt
source-git-commit: 1c2992d2a5992b07fa24823501d542c1878aa296
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 100%

---


# Exemplos de rastreamento do estado do player


## Exemplo de pausa longa

Quando uma sessão de vídeo tem uma duração de pausa superior a 30 minutos, a API exige uma nova sessão. Quando isso ocorrer, o cliente deverá gerar uma nova ID de sessão. Para ambas as sessões de vídeo, o cliente deve reter todos os estados em que um player está e enviar todas as informações como um evento `stateStart` evento logo após a chamada `sessionStart`.

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd
`

Depois que o `sessionEnd` for enviado, uma nova sessão de vídeo deverá ser iniciada e os primeiros eventos da API serão:

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

O exemplo de pausa longa mostra que o player também armazena seus estados para que possam ser enviados para a nova sessão de vídeo.
