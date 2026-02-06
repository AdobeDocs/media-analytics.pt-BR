---
title: Suporte a metadados personalizados
description: Saiba como fornecer pares de chave:valor personalizados nos eventos sessionStart, chapterStart e adStart.
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 62%

---

# Suporte a metadados personalizados{#custom-metadata-support}

Você pode fornecer pares de chaves :value personalizados nos eventos `sessionStart`, `chapterStart` e `adStart`. Essas informações devem ser fornecidas na chave JSON, `customMetadata`, posicionada com a chave `params`.

A chave JSON `customMetadata` deve conter um objeto de pares de chaves:value. A chave deve conter somente caracteres alfanuméricos, sublinhados e pontos.

[Eventos de API MA Collection](../mc-api-ref/mc-api-events-req.md)

## Exemplo

Atualmente você pode enviar um evento `sessionStart` com o seguinte par de chaves :value:

```
params: { "media.channel": "channel-1" },
  customMetadata: { "a.media.channel": "channel-2" }
```

Para a configuração acima, os dados de relatório enviados para análise são:

`c.a.media.channel=channel-2`

### Recomendação

Recomendamos usar um namespace separado para metadados personalizados. Por exemplo:

```
params: { "media.channel": "channel-1" },
  customMetadata: { "clientnamespace.media.channel": "channel-2" }
```

No exemplo recomendado, os dados de relatório para metadados personalizados enviados para análise são:

`c.a.media.channel=channel-1`
`c.clientnamespace.media.channel=channel-2`
