---
seo-title: Condições de tempo limite
title: Condições de tempo limite
uuid: 2 a 4 ea 13 e-a 561-4 adf-b 567-f 980301 b 32 c 8
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# Condições de tempo limite{#timeout-conditions}

**Condições de tempo limite da API da coleção de mídia**

A API de coleta de mídia, sem estado, não tem o mesmo mecanismo que o Media SDK para emitir uma nova ID da sessão quando as condições de tempo limite ocorrem. Quando ocorre uma condição de tempo limite, o back-end encerra a sessão e todas as chamadas subsequentes feitas com essa ID de sessão são descartadas. A lógica que lida com o Tempo limite da sessão deve ser tratada no cliente. Ou seja, o reprodutor precisará monitorar as condições de tempo limite e obter uma nova ID de sessão se ocorrer um tempo limite.

* **10 minutos: Sem eventos de API**

   Se o back end não receber nenhum evento API, ele fechará a sessão.
* **30 minutos: Nenhuma alteração no playhead**

   Se o indicador de reprodução não for movido por 30 minutos (por exemplo, o usuário acessar Pausar e sair), o back end fechará a sessão.

>[!NOTE]
>
>You can also force a session end by sending an `events` request with the `sessionEnd` event type.

