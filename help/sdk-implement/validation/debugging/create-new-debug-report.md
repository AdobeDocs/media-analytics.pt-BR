---
seo-title: Criar um novo relatório de depuração
title: Criar um novo relatório de depuração
uuid: 438 fde 3 d -98 f 9-46 d 1-95 72-75 d 204361568
translation-type: tm+mt
source-git-commit: f2b08663a928e27625a9ff63f783c510f41e7a8c

---


# Criar um novo relatório de depuração{#create-a-new-debug-report}

Para criar um novo relatório de depuração:

1. In [!UICONTROL Create New Debug Report] select the following:

   ![](assets/create-new-debug-report.png)

1. Preencha os campos com as seguintes informações:

   * **Nome do relatório** - Insira o nome do reprodutor e a data para que você possa rastrear facilmente o reprodutor durante a certificação e manter as marcas e plataformas separadas.
   * **Adobe Analytics**

      * [!UICONTROL Nome de usuário] e [!UICONTROL Segredo compartilhado] - Esses campos são opcionais, mas você pode adicionar suas credenciais da API de serviços da Web ao Adobe Debug para exibir os nomes e as configurações das variáveis do conjunto de relatórios.

         Você pode acessar seguindo um dos seguintes procedimentos:

         * [!UICONTROL Analytics &gt; Administrador &gt; Configurações da empresa &gt; Serviços da Web]
         * [!UICONTROL Analytics &gt; Administrador &gt; Gerenciamento de usuários &gt; Usuários &gt; Configurações de usuário individual] Para criar uma credencial da API de serviços da Web para um novo usuário, no [!UICONTROL Gerenciamento de usuários], adicione o usuário ao grupo de usuários de **Acesso ao serviço da Web**.
      * [!UICONTROL Endpoint padrão] - os dados nesse campo são fornecidos pela Adobe e não podem ser alterados.
      * [!UICONTROL Endpoint extra] - Adicionar `CNAMES`, se você os usar, para o servidor de rastreamento como `metrics.companyname.com`
   * **Video Heartbeats (Media Analytics)**

      * [!UICONTROL Endpoint padrão] - os dados nesse campo são fornecidos pela Adobe e não podem ser alterados.
      * [!UICONTROL Endpoint extra] - Adicionar `CNAMES`, se você os usar, para o servidor de rastreamento, por exemplo `metrics.companyname.com`,



