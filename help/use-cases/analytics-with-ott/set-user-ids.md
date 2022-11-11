---
title: Definir IDs de usuário
description: APIs para definir IDs de usuário, que servidor é um identificador exclusivo do cliente.
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
exl-id: 6b451082-47f3-4e65-9fe0-cecb2d20dc2d
feature: "Media Analytics, API"
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 100%

---

# Definir IDs de usuário{#set-user-ids}

O ID de usuário é um identificador de visitante personalizado e único, definido pelo aplicativo para um usuário.

Defina e obtenha a ID de usuário única no SDK do ADBMobile da seguinte maneira:

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
