---
seo-title: Rastrear estados do aplicativo
title: Rastrear estados do aplicativo
uuid: 2 f 98 fb 43-c 362-4 a 9 b -8732-fa 7 e 963 da 729
translation-type: tm+mt
source-git-commit: 9cdf69e30fa727aeb974213769a7ab61fb05b756

---


# Rastrear estados do aplicativo{#track-app-states}

Os estados são telas ou exibições diferentes do aplicativo. Each time a new state is displayed in your application, you should send a `trackState` call. For example, when a user navigates from the home page to the video details screen, send a `trackState` call. Os estados geralmente são vistos usando um relatório de definição de caminho para que você possa ver como os usuários navegam no seu aplicativo e quais estados são exibidos mais comumente.

## Chamadas trackState

You typically call `trackState` each time the app loads a new screen.

### Roku

```js
ADBMobile().trackState("State Name", {})
```

### Chromecast

```js
ADBMobile.analytics.trackState("State Name",{});
```

The state name is reported in the "View State" variable in Adobe Mobile services, and a view is recorded for each `trackState` call. Em outras interfaces do Analytics, "Visualizar estado" é relatado como "Nome da página"; " Exibições de estado "é relatado como" Exibições de página ".

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

