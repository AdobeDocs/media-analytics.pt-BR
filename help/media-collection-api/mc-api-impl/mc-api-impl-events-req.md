---
seo-title: Implementar uma solicitação de eventos
title: Implementar uma solicitação de eventos
uuid: 3 bfa 313 c-ff 74-4 e 2 e-bbde -6 f 4 a 6221 d 85 b
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Implementar uma solicitação de eventos{#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

Use the [Events request](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) for all subsequent tracking calls after you obtain a Session ID using the [Sessions request.](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) Especifique o local do indicador de reprodução e o carimbo de data e hora, o tipo de evento e quaisquer parâmetros opcionais que você deseja incluir no corpo JSON da solicitação.

The JSON request body for the [Events request](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) has the same structure as that of the Sessions request, however check the [JSON validation schemas](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) for parameter requirements and types.
