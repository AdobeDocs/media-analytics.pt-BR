---
title: Implementação de metadados padrão usando o JavaScript 3.x
description: Descreve a configuração de metadados de vídeo e anúncios padrão a serem enviados com chamadas de rastreamento em aplicativos do navegador (JS).
translation-type: tm+mt
source-git-commit: 318bb60d9835d9a07fb7aa0a0a02162248410d09
workflow-type: tm+mt
source-wordcount: '43'
ht-degree: 46%

---


# Implementação de metadados padrão usando o JavaScript 3.x{#implement-standard-metadata-on-javascript}

## Implementação

Instancie um objeto de dados de contexto e preencha as variáveis de metadados padronizadas desejadas. Por exemplo:

```js
_onVideoLoad = function () {
    //Create the Media Object
    var mediaObject =
      ADB.Media.createMediaObject(<MEDIA_NAME>,
                                       <MEDIA_ID,
                                       <MEDIA_LENGTH>,
                                       <STREAM_TYPE>,
                                       <MEDIA_TYPE>);

    //Set standard Video Metadata
    var contextData = {};
    contextData = "Sample Show";
    contextData = "Sample Season";
    contextData = "Sample Episode";

    //Set standard Audio Metadata
    var contextData = {};
    contextData = "Sample Artist";
    contextData = "Sample Album";
    contextData = "Sample Label";

    this.tracker.trackSessionStart(mediaObject, contextData);
};
```
