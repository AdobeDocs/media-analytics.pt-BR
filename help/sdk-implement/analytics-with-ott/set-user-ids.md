---
seo-title: Definir IDs de usuário
title: Definir IDs de usuário
uuid: fdd54ª-79cd-4bf8-b17e-4d61d84f6310
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# Definir IDs de usuário{#set-user-ids}

O ID de usuário é um identificador de visitante personalizado e exclusivo, definido pelo aplicativo para um usuário.

Defina e obtenha a ID de usuário exclusiva no SDK do ADBMobile da seguinte maneira:

* **Defina:**

   * **Roku:**

      ```
      ADBMobile().setUserIdentifer("app-generated-unique-id")
      ```

   * **Chromecast:**

      ```
      ADBMobile().config.setUserIdentifer("app-generated-unique-id");
      ```

* **Obtenha:**

   * **Roku:**

      ```
      vid = ADBMobile().userIdentifer()
      ```

   * **Chromecast:**

      ```
      vid = ADBMobile().config.getUserIdentifer();
      ```
