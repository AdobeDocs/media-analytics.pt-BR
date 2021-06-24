---
title: Esquemas de validação JSON do Streaming Media Analytics
description: O que são esquemas de validação JSON de mídia de fluxo contínuo e como eles são usados para determinar os parâmetros corretos do corpo da solicitação para cada tipo de evento.
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
exl-id: 2931715d-2e7d-4c15-8569-da63b43d6006
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 64%

---

# Esquemas de validação JSON{#json-validation-schemas}

O back-end do Media Analytics valida os parâmetros da solicitação para cada tipo de evento usando os esquemas de validação JSON. Esses esquemas estão disponíveis para você e servem como a autoridade atual sobre os tipos de parâmetros usados na API do MA.

```
GET
https://{uri}/api/v1/schemas/{event-type}
```

Para obter mais informações sobre como usar os esquemas de validação JSON, consulte [Validar solicitações de eventos.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
