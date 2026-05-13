---
title: Rastrear ações do aplicativo
description: Ações dos aplicativos são eventos que ocorrem no aplicativo que você deseja avaliar.
uuid: 9cdc048a-419a-4725-bd61-6ca6d909cf10
exl-id: 88b7d540-67b7-4ec1-8273-02e34853bf60
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/ahqWp2yjs-zkd9dTRWTkE7b6KE-WpwVR0OH9vCqTPjI
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 132
ht-degree: 100%

---

# Rastrear ações do aplicativo{#track-app-actions}

Ações são os eventos que ocorrem em seu aplicativo que você deseja avaliar.

Cada ação tem uma ou mais métricas correspondentes que são incrementadas sempre que o evento ocorre. Por exemplo, você pode enviar uma chamada `trackAction` para cada nova assinatura sempre que o conteúdo é avaliado, ou sempre que um nível é concluído.

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
