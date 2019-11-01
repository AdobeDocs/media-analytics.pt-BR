---
title: Suporte a metadados personalizados
description: null
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Suporte a metadados personalizados{#custom-metadata-support}

You can provide custom key:value pairs on the `sessionStart`, `chapterStart`, and `adStart` events. Essas informações devem ser fornecidas na chave JSON, `customMetadata`, posicionada com a chave `params`.

The `customMetadata` JSON key should contain an object of key:value pairs. A chave deve conter somente caracteres alfanuméricos, sublinhados e pontos.

[Eventos de API da coleção de MA](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

