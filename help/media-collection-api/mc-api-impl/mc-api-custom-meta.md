---
title: Suporte a metadados personalizados
description: null
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Suporte a metadados personalizados {#custom-metadata-support}

Você pode fornecer pares de chaves:valores personalizados nos eventos `sessionStart`, `chapterStart` e `adStart`. Essas informações devem ser fornecidas na chave JSON, `customMetadata`, posicionada com a chave `params`.

A chave JSON `customMetadata` deve conter um objeto de pares de chave:valor. A chave deve conter somente caracteres alfanuméricos, sublinhados e pontos.

[Eventos de API MA Collection](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

