---
title: Definir IDs de usuário
description: APIs para definição de IDs de usuário, que servem como um identificador exclusivo do cliente.
uuid: fdd54fec-79cd-4bf8-b17e-4d61d84f6310
exl-id: 6b451082-47f3-4e65-9fe0-cecb2d20dc2d
feature: "Streaming Media, API"
role: User, Admin, Data Engineer
source-git-commit: 70900e305c3ed7a2be4069c6f296d56f1f6e0966
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
