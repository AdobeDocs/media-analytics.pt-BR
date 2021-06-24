---
title: Rastrear ações do aplicativo
description: Ações dos aplicativos são eventos que ocorrem no aplicativo que você deseja avaliar.
uuid: 9cdc048a-419a-4725-bd61-6ca6d909cf10
exl-id: 88b7d540-67b7-4ec1-8273-02e34853bf60
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 100%

---

# Rastrear ações do aplicativo{#track-app-actions}

Ações são os eventos que ocorrem em seu aplicativo que você deseja medir.

Cada ação tem uma ou mais métricas correspondentes, que são incrementadas sempre que o evento ocorre. Por exemplo, você pode enviar uma chamada `trackAction` para cada nova assinatura sempre que o conteúdo é avaliado, ou sempre que um nível é concluído.

As ações não são rastreadas automaticamente, por isso, chame `trackAction` quando ocorrer um evento que você deseja rastrear e mapeie a ação para um evento personalizado.

1. Quando ocorrer um evento que você deseja rastrear, chame `trackAction`.

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
