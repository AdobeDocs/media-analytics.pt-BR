---
title: 'Implementar uma solicitação de eventos '
description: Saiba como usar o ponto de acesso de solicitação de eventos para todas as chamadas de rastreamento subsequentes após obter uma ID de sessão
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
exl-id: af9a3470-85c7-498e-9bf4-6df3c6aafad9
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 100%

---

# Implementar uma solicitação de eventos{#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

Use a [Solicitação de eventos](../mc-api-ref/mc-api-events-req.md) para todas as chamadas de rastreamento subsequentes após obter uma ID de sessão usando a [Solicitação de sessões.](../mc-api-ref/mc-api-sessions-req.md) Especifique a localização do indicador de reprodução, o carimbo de data e hora e o tipo de evento, juntamente com quaisquer parâmetros opcionais que deseja incluir no corpo JSON da solicitação.

O corpo da solicitação JSON para a [Solicitação de eventos](../mc-api-ref/mc-api-events-req.md) tem a mesma estrutura que a solicitação de sessões. porém, verifique os [esquemas de validação JSON](../mc-api-ref/mc-api-json-validation.md) quanto aos requisitos e tipos de parâmetros.
