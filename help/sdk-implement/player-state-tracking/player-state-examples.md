---
title: Exemplos de rastreamento de estado do player
description: Este tópico inclui exemplos do recurso de Rastreamento de estado do player.
translation-type: tm+mt
source-git-commit: 1cf11a6b8971f5be490998bbd855a27bfe366e48
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# Exemplos de rastreamento de estado do player

Adicionar exemplos


## Exemplo de pausa longa

Quando uma sessão de vídeo tem uma duração de pausa superior a 30 minutos, a API requer uma nova sessão. Quando isso ocorrer, o cliente deverá gerar uma nova ID de sessão. Para ambas as sessões de vídeo, o cliente deve reter todos os estados em que um player está e enviar todas as informações como um `stateStart` evento logo após a `sessionStart` chamada.

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd
`

Depois que o `sessionEnd` for enviado, uma nova sessão de vídeo deverá ser iniciada e os primeiros eventos da API serão:

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

O exemplo de pausa longa mostra que o player também armazena seus estados, para que possam ser enviados para a nova sessão de vídeo.