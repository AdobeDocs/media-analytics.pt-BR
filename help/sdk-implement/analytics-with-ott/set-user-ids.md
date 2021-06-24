---
title: Definir IDs de usuário
description: APIs para definir IDs de usuário, que servidor é um identificador exclusivo do cliente.
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
exl-id: 6b451082-47f3-4e65-9fe0-cecb2d20dc2d
feature: '"Media Analytics, API"'
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 94%

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
