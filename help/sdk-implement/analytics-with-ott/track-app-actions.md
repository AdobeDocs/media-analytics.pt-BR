---
seo-title: Rastrear ações do aplicativo
title: Rastrear ações do aplicativo
uuid: 9cdc048a-419a-4725-bd61-6ca6d909cf10
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# Rastrear ações do aplicativo{#track-app-actions}

As ações são eventos que ocorrem no aplicativo que você deseja avaliar.

Cada ação tem uma ou mais métricas correspondentes, que são incrementadas sempre que o evento ocorre. For example, you might send a `trackAction` call for each new subscription, or each time content is rated, or each time a level is completed.

As ações não são rastreadas automaticamente, por isso, chame `trackAction` quando ocorrer um evento que você deseja rastrear e mapeie a ação para um evento personalizado.

1. When an event that you want to track occurs, call `trackAction`.

   * **Roku:**

      ```js
      ADBMobile().trackAction("myapp.ActionName", {})
      ```

   * **Chromecast:**

      ```js
      ADBMobile.analytics.trackAction("myapp.ActionName", {});
      ```

1. Mapeie a ação a um evento personalizado.

   * **Roku:**

      ```js
      dictionary = {} 
      dictionary["myapp.social.SocialSource"] = "Twitter"  
      ADBMobile().trackAction("myapp.SocialShare", dictionary)
      ```

   * **Chromecast:**

      ```js
      var dictionary = {}; 
      dictionary["myapp.social.SocialSource"] = "Twitter"; 
      ADBMobile.analytics.trackAction("myapp.SocialShare", dictionary);
      ```

Você também pode enviar dados de contexto adicionais com cada chamada de ação de rastreamento.

