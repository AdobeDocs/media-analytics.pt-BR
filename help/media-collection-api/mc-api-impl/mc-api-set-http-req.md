---
title: Definição do tipo de solicitação HTTP no seu reprodutor
description: Definição do tipo de solicitação HTTP no seu reprodutor
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
exl-id: 9ab3eb07-8f0d-4f9a-8feb-db20c4de3db4
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '58'
ht-degree: 100%

---

# Definição do tipo de solicitação HTTP {#setting-the-http-request-type}

O corpo da solicitação para todas as solicitações da API Media Collection deve estar no formato JSON; portanto, você deve definir o tipo de solicitação de conteúdo no seu reprodutor. Por exemplo, em JavaScript, você define o cabeçalho da solicitação `Content-Type` como segue:

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```
