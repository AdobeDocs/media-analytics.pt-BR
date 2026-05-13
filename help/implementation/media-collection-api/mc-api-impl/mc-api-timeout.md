---
title: Condições de tempo-limite
description: Saiba mais sobre as condições de tempo limite da API Media Collection.
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
exl-id: 0b494b27-a4a6-4af7-84c1-c44b33b6da8f
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/13vwFrp3NF-e-odFn3eXIuhHusl14ovkwhTpPYbJC0U
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 165
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
