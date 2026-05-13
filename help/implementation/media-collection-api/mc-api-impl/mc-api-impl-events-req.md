---
title: Implementar uma solicitação de eventos
description: Saiba como usar o ponto de acesso de solicitação de eventos para todas as chamadas de rastreamento subsequentes após obter uma ID de sessão
uuid: 3bfa313c-ff74-4e2e-bbde-6f4a6221d85b
exl-id: af9a3470-85c7-498e-9bf4-6df3c6aafad9
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/xJntEcDm5sCGoCeuCjl9x51EOaYcOO2FzFAtK8mbt38
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 99
ht-degree: 56%

---

# Implementar uma solicitação de eventos{#implementing-an-events-request}

**`{uri}/api/v1/sessions/{sid}/events`**

Use a [Solicitação de eventos](../mc-api-ref/mc-api-events-req.md) para todas as chamadas de rastreamento subsequentes após obter uma ID de sessão usando a [Solicitação de sessões.](../mc-api-ref/mc-api-sessions-req.md) Especifique a localização do indicador de reprodução, o carimbo de data e hora e o tipo de evento, juntamente com quaisquer parâmetros opcionais que deseja incluir no corpo JSON da solicitação.

O corpo da solicitação JSON para a [Solicitação de eventos](../mc-api-ref/mc-api-events-req.md) tem a mesma estrutura que a solicitação de sessões. porém, verifique os [esquemas de validação JSON](../mc-api-ref/mc-api-json-validation.md) quanto aos requisitos e tipos de parâmetros.
