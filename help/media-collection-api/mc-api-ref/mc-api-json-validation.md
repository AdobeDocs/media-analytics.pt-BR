---
title: Esquemas de validação JSON
description: null
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
translation-type: tm+mt
source-git-commit: 72fd9b359d778c912ae6439aa0438ed467ebeef1
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Esquemas de validação JSON {#json-validation-schemas}

O back-end do Media Analytics valida os parâmetros da solicitação para cada tipo de evento usando os esquemas de validação JSON. Esses esquemas estão disponíveis para você e servem como a autoridade atual sobre os tipos de parâmetros usados na API do MA.

```
GET
https://{uri}/api/v1/schemas/{event-type}
```

Para obter mais informações sobre como usar os esquemas de validação JSON, consulte [Validar solicitações de eventos.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
