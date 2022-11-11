---
title: Introdução
description: Introdução ao Adobe Analytics para mídia de streaming.
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 6%

---


# Introdução {#getting-started}

O Adobe Analytics for Streaming Media oferece dois métodos principais de implementação: os SDKs do Media e as APIs Media Collection.

![métodos](assets/getting-started2.png)

Uso da lógica integrada da variável **SDKs do Media**, você pode medir com precisão várias plataformas de mídia, incluindo sites, celulares, TVs conectadas, tablets, dispositivos OTT, decodificadores de sinais e consoles de jogos. Você pode até mesmo medir o conteúdo baixado. Os insights que você obtém são mais aprofundados no envolvimento de visualização do usuário, para que você possa entender por quanto tempo, quando e onde os visualizadores se envolvem. Os SDKs do Media usam o **APIs da coleção de mídia** para rastreamento. As APIs Media Collection são personalizáveis, se o aplicativo exigir recursos de rastreamento personalizados. Para dispositivos não compatíveis com os SDKs do Media, você pode usar as APIs Media Collection.

A solução Adobe Analytics Streaming Media é fornecida para as seguintes plataformas de mídia:

* Web
* Dispositivo móvel
* Sobre o topo
* Qualquer dispositivo conectado que possa ser usado para mídia de transmissão ou integração de servidor para servidor

Para obter mais informações, consulte [Dispositivos e plataformas compatíveis](#_Supported_devices_and).

>[!IMPORTANT]
>
>Para implementar o Adobe Analytics Streaming Media, entre em contato com o Representante de vendas do Adobe ou o Gerente de conta para garantir que o Streaming Media faça parte do seu portfólio de produtos.

## SDKs do Media para mídia de transmissão {#media-sdks}

Os SDKs do Media para mídia de transmissão estão disponíveis para plataformas JavaScript, Android, iOS, tvOS, Chromecast e Roku.

Para obter informações sobre como baixar e instalar SDKs do Media, consulte [Obter SDKs do Media, extensões usando tags e SDKs OTT](/help/getting-started/download-sdks.md).


## APIs da coleção de mídia {#media-collection-apis}

O **APIs da coleção de mídia** permite personalizar a implementação do media analytics. Use as APIs de coleção de mídia para chamar diretamente os servidores do Adobe e executar quase qualquer ação que você possa realizar usando os SDKs e muito mais. Personalize sua coleta de dados para criar relatórios que explorem, obtenham insights ou respondam perguntas importantes sobre seus dados de mídia de transmissão.

Para obter informações sobre como usar as APIs Media Collection, consulte [Documentação da API de mídia de streaming](/help/implementation/media-collection-api/mc-api-overview.md).

## Adobe Extensions {#adobe-extensions}

>[!NOTE]
>
>PRECISA DE INTRO PARA AS EXTENSÕES

* O [**Extensão Adobe Medium Analytics for Audio and Video**](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=en) (Extensão do Media Analytics), é necessário para implementações do iOS e tvOS. Ele fornece a funcionalidade necessária para adicionar a instância do rastreador a um site ou projeto de tag. A extensão do MA também requer a extensão do Analytics e a extensão Experience Cloud ID.

* [Extensão do Analytics versão 1.6 ou superior](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=en)—Essa extensão permite carregar a biblioteca JavaScript do SDK da Web da Adobe Experience Platform para enviar dados para soluções do Adobe.

* [Extensão Experience Cloud ID](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=en)—Essa extensão implementa o Serviço de ID do Experience Cloud que identifica visitantes em todas as soluções de Experience Cloud. O Serviço de Experience Cloud ID é uma extensão de personalização no Adobe Experience Platform.
