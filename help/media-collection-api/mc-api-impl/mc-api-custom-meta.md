---
seo-title: Suporte a metadados personalizados
title: Suporte a metadados personalizados
uuid: df 4109 dd -9 fca -4 c 33-a 7 d 5-8 e 6 eec 257527
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# Suporte a metadados personalizados{#custom-metadata-support}

You can provide custom key:value pairs on the `sessionStart`, `chapterStart`, and `adStart` events. Essas informações devem ser fornecidas na chave JSON, `customMetadata`, posicionada com a chave `params`.

The `customMetadata` JSON key should contain an object of key:value pairs. A chave deve conter somente caracteres alfanuméricos, sublinhados e pontos.

[Eventos de API da coleção MA](../mc-api-ref/mc-api-events-req.md)

