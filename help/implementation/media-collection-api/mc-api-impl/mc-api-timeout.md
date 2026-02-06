---
title: Condições de tempo-limite
description: Saiba mais sobre as condições de tempo limite da API Media Collection.
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
exl-id: 0b494b27-a4a6-4af7-84c1-c44b33b6da8f
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 60%

---

# Condições de tempo-limite{#timeout-conditions}

**Condições de tempo-limite da API Media Collection**

Como a API Media Collection não possui estado, ela não apresenta o mesmo mecanismo que o SDK do Media para emitir uma nova ID de sessão quando ocorrem condições de tempo-limite. Quando uma condição de tempo limite ocorre, o back-end encerra a sessão e todas as chamadas subsequentes feitas com essa ID de sessão são descartadas. A lógica que lida com um Tempo limite de sessão deve ser tratada no cliente. Ou seja, o reprodutor terá que monitorar as condições de tempo limite e obter uma nova ID de sessão se um tempo limite ocorrer.

* **10 minutos: Nenhum evento de API**

  Se o back-end não receber eventos de API, ele encerrará a sessão.
* **30 minutos: Sem alteração no indicador de reprodução**

  Se o indicador de reprodução não se mover por 30 minutos (por exemplo, o usuário clica em Pausar e sai), o back-end encerrará a sessão.

>[!NOTE]
>
>Você também pode forçar o fim de uma sessão, enviando uma solicitação `events` com o tipo de evento `sessionEnd`.
