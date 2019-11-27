---
title: Criar um novo relatório de depuração
description: Este tópico descreve como criar um novo relatório de Depuração.
uuid: 438fde3d-98f9-46d1-9672-75d204361568
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Criar um novo relatório de depuração {#create-a-new-debug-report}

Para criar um novo relatório de depuração:

1. Em [!UICONTROL Criar novo relatório de depuração], selecione o seguinte:

   ![](assets/create-new-debug-report.png)

1. Preencha os campos com as seguintes informações:

   * **Nome do relatório** - Insira o nome do reprodutor e a data para que você possa rastrear facilmente o reprodutor durante a certificação e manter as marcas e plataformas separadas.
   * **Adobe Analytics**

      * [!UICONTROL Nome de usuário] e [!UICONTROL Segredo compartilhado] - Esses campos são opcionais, mas você pode adicionar suas credenciais da API de serviços da Web ao Adobe Debug para exibir os nomes e as configurações das variáveis do conjunto de relatórios.

         Você pode acessar seguindo um dos seguintes procedimentos:

         * [!UICONTROL Analytics &gt; Administrador &gt; Configurações da empresa &gt; Serviços da Web]
         * [!UICONTROL Analytics &gt; Administrador &gt; Gerenciamento de usuários &gt; Usuários &gt; Configurações de usuário individual] Para criar uma credencial da API de serviços da Web para um novo usuário, no [!UICONTROL Gerenciamento de usuários], adicione o usuário ao grupo de usuários de **Acesso ao serviço da Web**.
      * [!UICONTROL Endpoint padrão] — Os dados nesse campo são fornecidos pela Adobe e não podem ser alterados.
      * [!UICONTROL Endpoint adicional] — Adicione `CNAMES`, se estiverem em uso, para rastrear um servidor como `metrics.companyname.com`
   * **Hearbeats de vídeo (Media Analytics)**

      * [!UICONTROL Endpoint padrão] — Os dados nesse campo são fornecidos pela Adobe e não podem ser alterados.
      * [!UICONTROL Endpoint adicional] — Adicione `CNAMES`, se estiverem em uso, para rastrear um servidor, por exemplo, `metrics.companyname.com`.



