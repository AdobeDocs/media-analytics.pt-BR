---
title: Enviar dados de QoE
description: Saiba como enviar eventos com uma chave JSON de dados de QoE.
uuid: 52a02d92-195d-4ce8-8ce3-585ed68969f9
exl-id: 41a20410-78e6-481d-bd5c-0febadb290d8
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '55'
ht-degree: 100%

---

# Enviar dados de QoE{#sending-qoe-data}

Cada evento pode ser decorado com uma chave JSON adicional chamada `qoeData`, que é posicionada juntamente com a chave `params` no corpo da solicitação JSON.

>[!NOTE]
>
>Você deve verificar os [esquemas de validação JSON](mc-api-validate-reqs.md) para verificar os tipos de parâmetros e se são obrigatórios ou opcionais.
