---
title: Opções de medição
description: null
uuid: null
source-git-commit: 0d5edcae0a80357247ada7f61daece9840d5c4b5
workflow-type: ht
source-wordcount: '287'
ht-degree: 100%

---


# Opções de medição {#measurement-options}

Você pode ativar o rastreamento de áudio e vídeo usando o Adobe Launch com a extensão do Adobe Media Analytics, o SDK de mídia ou a API de coleção de mídia.

## Adobe Launch com a extensão do Adobe Media Analytics

O Adobe Launch é a solução de gerenciamento de tags de última geração da Adobe. O Launch oferece uma forma simples de implantar e gerenciar todas as tags de análise, marketing e anúncios necessárias para enriquecer as experiências de clientes relevantes. Para criar e manter suas próprias integrações com o Launch, use extensões. Uma extensão é um pacote de JavaScript, HTML e CSS que estende a funcionalidade do cliente e da interface do usuário do Launch. Para obter mais informações, consulte o [Guia do usuário da Experience Platform Launch](https://experienceleague.adobe.com/docs/launch/using/overview.html)

A extensão do Adobe Media Analytics (MA) adiciona o principal SDK de mídia JavaScript (SDK do Media 2.x) para áudio e vídeo. Esta extensão fornece a funcionalidade necessária para adicionar a instância do rastreador `MediaHeartbeat` a um site ou projeto do Launch.

O Adobe Launch com a extensão do Media Analytics exige o seguinte:
* Você deve ser um cliente da Adobe Experience Cloud.
* Você deve implantar o código de incorporação do Launch ou DTM nas páginas da Web.
* [Extensão do Analytics](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html?lang=pt-BR)
* [Extensão do Experience Cloud ID](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html?lang=pt-BR)

## SDK do Media

O SDK de mídia integra-se aos players de mídia mais usados.

## API Media Collection (RESTful API)

Integra-se aos players sem suporte ao SDK ou quando a integração ao SDK não é necessária.<br>A partir da versão v2.2.0, os SDKs da Biblioteca do Video Heartbeat (VHL) são renomeados para SDKs do Media Analytics para oferecer suporte ao rastreamento de áudio e vídeo. O Media 2.2.0 SDK tem compatibilidade reversa com a série de SDK VHL 2.X. A alteração de nome é simplesmente uma alteração na convenção de nomenclatura e não representa mudanças funcionais.
