---
title: Definir IDs de usuário
description: APIs para definição de IDs de usuário, que servem como um identificador exclusivo do cliente.
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
exl-id: 6b451082-47f3-4e65-9fe0-cecb2d20dc2d
feature: "Streaming Media, API"
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 45%

---

# Definir IDs de usuário{#set-user-ids}

A ID do usuário é um identificador de visitante personalizado exclusivo definido pelo aplicativo para um usuário.

Defina e obtenha o ID de usuário exclusivo no ADBMobile SDK da seguinte maneira:

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
