---
title: Rastrear estados do aplicativo
description: Os estados de aplicativos são as diferentes telas ou visualizações no aplicativo. Saiba como rastrear o estado do aplicativo usando a chamada trackState.
uuid: 2f98fb43-c362-4a9b-8732-fa7e963da729
exl-id: bb1e0eee-7c59-40b4-9359-a7441b9686b8
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 100%

---

# Rastrear estados do aplicativo{#track-app-states}

Os estados são telas ou exibições diferentes do aplicativo. Sempre que um novo estado for exibido no aplicativo, você deverá enviar uma chamada `trackState`. Por exemplo, quando um usuário navega da página inicial para a tela de detalhes do vídeo, envie uma chamada `trackState`. Os estados geralmente são vistos usando um relatório de definição de caminho para que você possa ver como os usuários navegam no seu aplicativo e quais estados são exibidos mais comumente.

## Chamadas trackState

Normalmente, você chama `trackState` sempre que o aplicativo carrega uma nova tela.

### Roku

```js
ADBMobile().trackState("State Name", {})
```

### Chromecast

```js
ADBMobile.analytics.trackState("State Name",{});
```

O nome do estado é relatado na variável “Exibir estado” no Adobe Mobile Services e uma exibição é gravada para cada `trackState` chamada. Em outras interfaces do Analytics, o “Exibir estado” é reportado como “Nome de página” e as “Exibições de estado” como “Exibições de páginas”.

## Enviar dados de contexto

Além do &quot;Nome do estado&quot;, é possível enviar dados de contexto adicionais com cada chamada de rastreamento de estado.

### Roku

```js
dictionary = { } 
dictionary["myapp.login.LoginStatus"] = "logged in"  
ADBMobile().trackState("Home Screen", dictionary)
```

### Chromecast

```js
var dictionary = { }; 
dictionary["myapp.login.LoginStatus"] = "logged in"; 
ADBMobile.analytics.trackState("Home Screen", dictionary); 
```

>[!NOTE]
>
>Os valores de dados de contexto devem ser mapeados para variáveis personalizadas nos Adobe Mobile Services.
