---
title: Rastrear estados do aplicativo
description: 'Os estados do aplicativo são telas ou exibições diferentes no aplicativo, que quando exibidas devem resultar em uma chamada trackState. '
uuid: 2f98fb43-c362-4a9b-8732-fa7e963da729
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Rastrear estados do aplicativo {#track-app-states}

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

O nome do estado é relatado na variável “Exibir estado” no Adobe Mobile Services e uma exibição é gravada para cada chamada de `trackState`. Em outras interfaces do Analytics, o “Exibir estado” é reportado como “Nome de página” e as “Exibições de estado” como “Exibições de páginas”.

## Enviar dados de contexto

Além do "Nome do estado", é possível enviar dados de contexto adicionais com cada chamada de rastreamento de estado.

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

