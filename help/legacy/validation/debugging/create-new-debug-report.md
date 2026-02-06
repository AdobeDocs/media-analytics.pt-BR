---
title: Criar um novo relatório de depuração
description: Saiba como criar um novo relatório de depuração.
uuid: 438fde3d-98f9-46d1-9672-75d204361568
exl-id: 047acf35-8c1c-4493-9ee7-e2bad47c351e
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 44%

---

# Criar um novo relatório de depuração{#create-a-new-debug-report}

Para criar um novo relatório de depuração:

1. Em [!UICONTROL Criar novo relatório de depuração], selecione o seguinte:

   ![](assets/create-new-debug-report.png)

1. Preencha os campos com as seguintes informações:

   * **Nomear o relatório** - Insira o nome e a data do player para que você possa rastrear facilmente o player durante a certificação e manter as marcas e plataformas separadas.
   * **Adobe Analytics**

      * [!UICONTROL Nome de Usuário] e [!UICONTROL Segredo Compartilhado] - Esses campos são opcionais, mas você pode adicionar suas credenciais de API de serviços da Web ao Adobe Debug para exibir os nomes de variáveis e as configurações de variáveis do conjunto de relatórios.

        Você pode acessar o de uma das seguintes maneiras:

         * [!UICONTROL Analytics > Administrador > Configurações da empresa > Serviços da Web]
         * [!UICONTROL Analytics > Administrador > Gerenciamento de usuários > Usuários > Configurações de usuário individual] Para criar uma credencial da API de serviços da Web para um novo usuário, em [!UICONTROL Gerenciamento de usuários], adicione o usuário ao grupo de usuários **Acesso ao serviço da Web**.

      * [!UICONTROL Endpoint padrão] — Os dados nesse campo são fornecidos pela Adobe e não podem ser alterados.
      * [!UICONTROL Endpoint adicional] — Adicione `CNAMES`, se estiverem em uso, para rastrear um servidor como `metrics.companyname.com`

   * **Hearbeats de vídeo (Media Analytics)**

      * [!UICONTROL Endpoint padrão] — Os dados nesse campo são fornecidos pela Adobe e não podem ser alterados.
      * [!UICONTROL Endpoint adicional] — Adicione `CNAMES`, se estiverem em uso, para rastrear um servidor, por exemplo, `metrics.companyname.com`.
