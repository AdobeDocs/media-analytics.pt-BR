---
seo-title: Condições de tempo limite
title: Condições de tempo limite
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# Condições de tempo limite{#timeout-conditions}

**Condições de tempo limite da API da coleção de mídia**

The Media Collection API, being stateless, does not have the same mechanism as the Media SDK for issuing a new Session ID when timeout conditions occur. Quando ocorre uma condição de tempo limite, o back-end encerra a sessão e todas as chamadas subsequentes feitas com essa ID de sessão são descartadas. A lógica que lida com o Tempo limite da sessão deve ser tratada no cliente. Ou seja, o reprodutor precisará monitorar as condições de tempo limite e obter uma nova ID de sessão se ocorrer um tempo limite.

* **10 minutos: Nenhum evento de API**

   Se o back-end não receber nenhum evento de API, a sessão será fechada.
* **30 minutos: Sem alteração no indicador de reprodução**

   Se o indicador de reprodução não se mover por 30 minutos (por exemplo, o usuário acessa Pausar e afasta-se), o back-end fechará a sessão.

>[!NOTE]
>
>You can also force a session end by sending an `events` request with the `sessionEnd` event type.

