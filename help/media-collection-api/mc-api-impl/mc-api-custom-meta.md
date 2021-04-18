---
title: Suporte a metadados personalizados
description: Suporte a metadados personalizados
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 100%

---

# Suporte a metadados personalizados {#custom-metadata-support}

Você pode fornecer pares de chaves:valores personalizados nos eventos `sessionStart`, `chapterStart` e `adStart`. Essas informações devem ser fornecidas na chave JSON, `customMetadata`, posicionada com a chave `params`.

A chave JSON `customMetadata` deve conter um objeto de pares de chave:valor. A chave deve conter somente caracteres alfanuméricos, sublinhados e pontos.

[Eventos de API MA Collection](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)
