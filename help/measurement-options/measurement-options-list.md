---
title: Opções de medição
description: null
uuid: null
translation-type: tm+mt
source-git-commit: 967a126723ebbbe02097bd07edc2ed967cd35f4c
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 19%

---


# Opções de medição{#measurement-options}

Você pode ativar o rastreamento de áudio e vídeo usando o Adobe Launch com a extensão do Adobe Media Analytics, o SDK de mídia ou a API de coleção de mídia.

## Adobe Launch com a extensão do Adobe Media Analytics

O Adobe Launch é a próxima geração da solução de gerenciamento de tags da Adobe. O Launch fornece uma maneira simples de implantar e gerenciar todas as tags de análise, marketing e publicidade necessárias para potencializar as experiências relevantes do cliente. Para criar e manter suas próprias integrações com o Launch, use extensões. Uma extensão é um pacote JavaScript, HTML e CSS que estende a interface do usuário de inicialização e a funcionalidade do cliente. Para obter mais informações, consulte o Guia do Usuário do [Experience Platform Launch](https://docs.adobe.com/content/help/pt-BR/launch/using/overview.html)

A extensão do Adobe Media Analytics (MA) adiciona o principal SDK de mídia JavaScript (SDK do Media 2.x) para áudio e vídeo. Esta extensão fornece a funcionalidade necessária para adicionar a instância do rastreador `MediaHeartbeat` a um site ou projeto do Launch.

O Adobe Launch com a extensão do Media Analytics exige o seguinte:
* Você deve ser um cliente da Adobe Experience Cloud.
* Você deve implantar o código incorporado Launch ou DTM em suas páginas da Web.
* [Extensão do Analytics](https://docs.adobe.com/content/help/pt-BR/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html)
* [Extensão do Experience Cloud ID](https://docs.adobe.com/content/help/pt-BR/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)

## SDK do Media

O SDK de mídia é integrado aos players de mídia mais usados.

## API Media Collection (RESTful API)

Integra-se aos players sem suporte ao SDK ou quando a integração ao SDK não é necessária.<br>A partir da versão v2.2.0, os SDKs da Biblioteca do Video Heartbeat (VHL) são renomeados para SDKs do Media Analytics para oferecer suporte ao rastreamento de áudio e vídeo. O SDK do Media 2.2.0 é totalmente compatível com versões anteriores do SDK VHL 2.x. A alteração de nome é simplesmente uma alteração na convenção de nomenclatura e não representa alterações funcionais.
