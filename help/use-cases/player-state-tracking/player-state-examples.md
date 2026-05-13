---
title: Exemplos de rastreamento do estado do player
description: Este tópico inclui exemplos do recurso de Rastreamento do estado do player.
exl-id: a77bc882-ac03-40b4-ac64-87f26a09707b
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/eJ9Pb4tWQy0lRhkNXmexUyflt3qT0105FM--jAsGldQ
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 120
ht-degree: 100%

---

# Exemplos de rastreamento do estado do player


## Exemplo de pausa longa

Quando uma sessão de vídeo tem uma duração de pausa superior a 30 minutos, a API exige uma nova sessão. Quando isso ocorrer, o cliente deverá gerar uma nova ID de sessão. Para ambas as sessões de vídeo, o cliente deve reter todos os estados em que um player está e enviar todas as informações como um evento `stateStart` evento logo após a chamada `sessionStart`.

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd`

Depois que o `sessionEnd` for enviado, uma nova sessão de vídeo deverá ser iniciada e os primeiros eventos da API serão:

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

O exemplo de pausa longa mostra que o player também armazena seus estados para que possam ser enviados para a nova sessão de vídeo.
