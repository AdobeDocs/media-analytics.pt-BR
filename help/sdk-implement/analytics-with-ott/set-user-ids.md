---
title: Definir IDs de usuário
description: APIs para definir IDs de usuário, que servidor é um identificador exclusivo do cliente.
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Definir IDs de usuário {#set-user-ids}

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
