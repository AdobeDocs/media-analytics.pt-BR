---
seo-title: Definição do tipo de solicitação HTTP no seu reprodutor
title: Definição do tipo de solicitação HTTP no seu reprodutor
uuid: b8fa7233-e654-4acf-a9d7-14158cded13e
translation-type: tm+mt
source-git-commit: 7f0a6a8d6def094bd669e5924ea76107a4ab3cc1

---


# Definição do tipo de solicitação HTTP {#setting-the-http-request-type}

O corpo da solicitação para todas as solicitações da API da coleção de mídia deve estar no formato JSON; portanto, você deve definir o tipo de solicitação de conteúdo no seu reprodutor. Por exemplo, em JavaScript, você define o cabeçalho da solicitação `Content-Type` como segue:

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```

