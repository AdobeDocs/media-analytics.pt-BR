---
title: Definição do tipo de solicitação HTTP no seu reprodutor
description: 'O corpo da solicitação para todas as solicitações da API da coleção de mídia de transmissão deve estar no formato JSON. Saiba como definir o tipo de solicitação de conteúdo no seu reprodutor. '
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
exl-id: 9ab3eb07-8f0d-4f9a-8feb-db20c4de3db4
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 66%

---

# Definição do tipo de solicitação HTTP {#setting-the-http-request-type}

O corpo da solicitação para todas as solicitações da API Media Collection deve estar no formato JSON; portanto, você deve definir o tipo de solicitação de conteúdo no seu reprodutor. Por exemplo, em JavaScript, você define o cabeçalho da solicitação `Content-Type` como segue:

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```
