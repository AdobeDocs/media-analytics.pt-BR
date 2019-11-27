---
title: Esquemas de validação JSON
description: null
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Esquemas de validação JSON {#json-validation-schemas}

O back-end do Media Analytics valida os parâmetros da solicitação para cada tipo de evento usando os esquemas de validação JSON. Esses esquemas estão disponíveis para você e servem como a autoridade atual sobre os tipos de parâmetros usados na API do MA.

```
POST
https://{uri}/api/v1/schemas/{event-type}
```

Para obter mais informações sobre como usar os esquemas de validação JSON, consulte [Validar solicitações de eventos.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
