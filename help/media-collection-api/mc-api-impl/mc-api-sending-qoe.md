---
title: Enviar dados de QoE
description: Saiba mais sobre como enviar eventos com uma chave qoeData JSON.
uuid: 52a02d92-195d-4ce8-8ce3-585ed68969f9
exl-id: 41a20410-78e6-481d-bd5c-0febadb290d8
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '57'
ht-degree: 84%

---

# Enviar dados de QoE{#sending-qoe-data}

Cada evento pode ser decorado com uma chave JSON adicional chamada `qoeData`, que é posicionada juntamente com a chave `params` no corpo da solicitação JSON.

>[!NOTE]
>
>Você deve verificar os [esquemas de validação JSON](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md) para verificar os tipos de parâmetros e se são obrigatórios ou opcionais.
