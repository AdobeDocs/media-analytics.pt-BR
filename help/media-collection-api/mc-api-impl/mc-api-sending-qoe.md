---
title: Enviar dados de QoE
description: Enviar dados de QoE
uuid: 52a02d92-195d-4ce8-8ce3-585ed68969f9
exl-id: 41a20410-78e6-481d-bd5c-0febadb290d8
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '49'
ht-degree: 100%

---

# Enviar dados de QoE {#sending-qoe-data}

Cada evento pode ser decorado com uma chave JSON adicional chamada `qoeData`, que é posicionada juntamente com a chave `params` no corpo da solicitação JSON.

>[!NOTE]
>
>Você deve verificar os [esquemas de validação JSON](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md) para verificar os tipos de parâmetros e se são obrigatórios ou opcionais.
