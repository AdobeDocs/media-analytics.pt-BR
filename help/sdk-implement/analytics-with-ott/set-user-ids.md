---
seo-title: Definir IDs de usuário
title: Definir IDs de usuário
uuid: fdd 54 fec -79 cd -4 bf 8-b 17 e -4 d 61 d 84 f 6310
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
