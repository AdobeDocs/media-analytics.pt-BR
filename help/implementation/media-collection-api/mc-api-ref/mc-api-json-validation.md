---
title: Esquemas de validação JSON do complemento Coleção de mídia de transmissão
description: O que são esquemas de validação JSON de mídia de streaming e como eles são usados para determinar os parâmetros do corpo da solicitação corretos para cada tipo de evento.
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
exl-id: 2931715d-2e7d-4c15-8569-da63b43d6006
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 240fa48bdc738425e04cd29c27625c7dd612ff18
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 70%

---

# Esquemas de validação JSON{#json-validation-schemas}

O back-end do complemento Coleção de mídia de transmissão valida os parâmetros da solicitação para cada tipo de evento usando esquemas de validação JSON. Esses esquemas estão disponíveis para você e servem como a autoridade atual sobre os tipos de parâmetros usados na API do MA.

`GET https://{uri}/api/v1/schemas/{event-type}`

Para obter mais informações sobre como usar os esquemas de validação JSON, consulte [Validar solicitações de eventos.](../mc-api-impl/mc-api-validate-reqs.md)
