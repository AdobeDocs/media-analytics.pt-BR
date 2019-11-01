---
title: Condições de tempo limite
description: null
uuid: 2a4ea13e-a561-4adf-b567-f980301b32c8
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Condições de tempo limite{#timeout-conditions}

**Condições de tempo limite da API da coleção de mídia**

A API de coleta de mídia, sem estado, não tem o mesmo mecanismo que o SDK de mídia para a emissão de uma nova ID de sessão quando ocorrem condições de tempo limite. Quando ocorre uma condição de tempo limite, o back-end encerra a sessão e todas as chamadas subsequentes feitas com essa ID de sessão são descartadas. A lógica que lida com o Tempo limite da sessão deve ser tratada no cliente. Ou seja, o reprodutor precisará monitorar as condições de tempo limite e obter uma nova ID de sessão se ocorrer um tempo limite.

* **10 minutos: Nenhum evento de API**

   Se o back-end não receber nenhum evento de API, a sessão será fechada.
* **30 minutos: Sem alteração no indicador de reprodução**

   Se o indicador de reprodução não se mover por 30 minutos (por exemplo, o usuário acessa Pausar e afasta-se), o back-end fechará a sessão.

>[!NOTE]
>
>You can also force a session end by sending an `events` request with the `sessionEnd` event type.

