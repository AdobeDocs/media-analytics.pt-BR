---
seo-title: Definição do tipo de solicitação HTTP no seu reprodutor
title: Definição do tipo de solicitação HTTP no seu reprodutor
uuid: b 8 fa 7233-e 654-4 acf-a 9 d 7-14158 cded 13 e
translation-type: tm+mt
source-git-commit: 7f0a6a8d6def094bd669e5924ea76107a4ab3cc1

---


# Setting the HTTP request type {#setting-the-http-request-type}

O corpo da solicitação para todas as solicitações da API da coleção de mídia deve estar no formato JSON; portanto, você deve definir o tipo de solicitação de conteúdo no seu reprodutor. Por exemplo, em JavaScript, você define o cabeçalho da solicitação `Content-Type` como segue:

```
httpRequest.setRequestHeader('Content-Type', 'application/json'); 
```

