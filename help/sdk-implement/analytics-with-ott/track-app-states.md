---
seo-title: Rastrear estados do aplicativo
title: Rastrear estados do aplicativo
uuid: 2f98fb43-c362-4a9b-8732-fa7e963da729
translation-type: tm+mt
source-git-commit: 9cdf69e30fa727aeb974213769a7ab61fb05b756

---


# Rastrear estados do aplicativo{#track-app-states}

Os estados são telas ou exibições diferentes do aplicativo. Sempre que um novo estado for exibido no aplicativo, você deverá enviar uma `trackState` chamada. Por exemplo, quando um usuário navega da página inicial para a tela de detalhes do vídeo, envia uma `trackState` chamada. Os estados geralmente são vistos usando um relatório de definição de caminho para que você possa ver como os usuários navegam no seu aplicativo e quais estados são exibidos mais comumente.

## Chamadas trackState

Normalmente, você liga `trackState` sempre que o aplicativo carrega uma nova tela.

### Roku

```js
ADBMobile().trackState("State Name", {})
```

### Chromecast

```js
ADBMobile.analytics.trackState("State Name",{});
```

The state name is reported in the "View State" variable in Adobe Mobile services, and a view is recorded for each `trackState` call. In other Analytics interfaces, "View State" is reported as "Page Name"; "State Views" is reported as "Page Views".

## Enviar dados de contexto

Além de "State Name", você pode enviar dados de contexto adicionais com cada chamada de rastreamento de estado.

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

