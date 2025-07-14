---
title: Esquemas de validação JSON da coleção de mídia de transmissão
description: O que são esquemas de validação JSON de mídia de streaming e como eles são usados para determinar os parâmetros do corpo da solicitação corretos para cada tipo de evento.
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
exl-id: 2931715d-2e7d-4c15-8569-da63b43d6006
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 72%

---

# Esquemas de validação JSON{#json-validation-schemas}

O back-end da Coleção de mídia de transmissão valida os parâmetros da solicitação para cada tipo de evento usando esquemas de validação JSON. Esses esquemas estão disponíveis para você e servem como a autoridade atual sobre os tipos de parâmetros usados na API do MA.

`GET https://{uri}/api/v1/schemas/{event-type}`

Para obter mais informações sobre como usar os esquemas de validação JSON, consulte [Validar solicitações de eventos.](../mc-api-impl/mc-api-validate-reqs.md)
