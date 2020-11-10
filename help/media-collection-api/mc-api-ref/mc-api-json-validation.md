---
title: Esquemas de validação JSON
description: null
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
translation-type: tm+mt
source-git-commit: 9b2f8b14ddb5b814f57c752665b78409e31173e8
workflow-type: tm+mt
source-wordcount: '55'
ht-degree: 100%

---


# Esquemas de validação JSON {#json-validation-schemas}

O back-end do Media Analytics valida os parâmetros da solicitação para cada tipo de evento usando os esquemas de validação JSON. Esses esquemas estão disponíveis para você e servem como a autoridade atual sobre os tipos de parâmetros usados na API do MA.

```
GET
https://{uri}/api/v1/schemas/{event-type}
```

Para obter mais informações sobre como usar os esquemas de validação JSON, consulte [Validar solicitações de eventos.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
