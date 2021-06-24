---
title: Suporte a metadados personalizados
description: '"Saiba como fornecer pares de chave:valor personalizados nos eventos sessionStart, chapterStart e adStart ."'
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 48%

---

# Suporte a metadados personalizados{#custom-metadata-support}

Você pode fornecer pares de chaves:valores personalizados nos eventos `sessionStart`, `chapterStart` e `adStart`. Essas informações devem ser fornecidas na chave JSON, `customMetadata`, posicionada com a chave `params`.

A chave JSON `customMetadata` deve conter um objeto de pares de chave:valor. A chave deve conter somente caracteres alfanuméricos, sublinhados e pontos.

[Eventos de API MA Collection](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

## Exemplo

Atualmente, você pode enviar um evento `sessionStart` com o seguinte par chave:valor :

```
params: { "media.channel": "channel-1" },
  customMetadata: { "a.media.channel": "channel-2" }
```

Para a configuração acima, os dados de relatório enviados para o analytics são os seguintes:

`c.a.media.channel=channel-2`

### Recomendação

Recomendamos usar um namespace separado para metadados personalizados. Por exemplo:

```
params: { "media.channel": "channel-1" },
  customMetadata: { "clientnamespace.media.channel": "channel-2" }
```

No exemplo recomendado, os dados de relatório para metadados personalizados enviados para o Analytics são:

`c.a.media.channel=channel-1`
`c.clientnamespace.media.channel=channel-2`
