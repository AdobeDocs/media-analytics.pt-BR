---
title: Introdução
description: Introdução ao Adobe Analytics para mídia de transmissão.
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: 660aa29a-2a3d-4a4f-acd6-471551d1047b
source-git-commit: 8b939da2374acb5d573a553c848ba880345e64b5
workflow-type: ht
source-wordcount: '439'
ht-degree: 100%

---

# Introdução {#getting-started}

O Adobe Analytics para mídia de transmissão oferece dois métodos principais de implementação, os SDKs de mídia e as APIs da Coleção de mídia.

![Métodos ](assets/getting-started2.png)

Usando a lógica integrada dos **SDKs de Mídia**, você pode medir com precisão várias plataformas de mídia, incluindo sites, celulares, TVs conectadas, tablets, dispositivos OTT, decodificadores de sinais e consoles de jogos. Você pode até mesmo medir o conteúdo baixado. Os insights que você obtém são mais aprofundados no envolvimento de visualização do usuário, para que você possa entender por quanto tempo, quando e onde os visualizadores se envolvem. Os SDKs de Mídia usam as **APIs do Media Collection** para rastreamento. As APIs do Media Collection são personalizáveis, se o aplicativo exigir recursos de rastreamento personalizados. Para dispositivos não compatíveis com os SDKs de Mídia, você pode usar as APIs do Media Collection.

A solução Adobe Analytics para mídia de transmissão é fornecida para as seguintes plataformas de mídia:

* Web
* Dispositivo móvel
* Over-the-top
* Qualquer dispositivo conectado que possa ser usado para mídia de transmissão ou integração de servidor para servidor

Para obter mais informações, consulte [Dispositivos e plataformas compatíveis](#_Supported_devices_and).

>[!IMPORTANT]
>
>Para implementar a Mídia de Streaming do Adobe Analytics, entre em contato com o Representante de vendas da Adobe ou com o gerente de conta para garantir que a Mídia de transmissão faça parte do seu portfólio de produtos.

## SDKs de mídia para mídia de transmissão {#media-sdks}

Os SDKs de mídia para mídia de transmissão estão disponíveis para plataformas JavaScript, Android, iOS, tvOS, Chromecast e Roku.

Para obter informações sobre como baixar e instalar SDKs de mídia, consulte [Obter SDKs de mídia, extensões usando tags e SDKs OTT](/help/getting-started/download-sdks.md).


## APIs da Coleção de mídia {#media-collection-apis}

As **APIs da Coleção de mídia** permitem personalizar a implementação de análise de mídia. Use as APIs da Coleção de mídia para chamar diretamente os servidores da Adobe e executar, praticamente, qualquer ação que você possa realizar usando os SDKs e muito mais. Personalize sua coleção de dados para criar relatórios que explorem, obtenham insights ou respondam a perguntas importantes sobre seus dados de mídia de transmissão.

Para obter informações sobre como usar as APIs da Coleção de mídia, consulte [Documentação da API de mídia de streaming](/help/implementation/media-collection-api/mc-api-overview.md).

## Extensões da Adobe {#adobe-extensions}

* A [**extensão do Adobe Media Analytics para Áudio e Vídeo**](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=pt-BR) (Extensão do Media Analytics), é necessária para implementações do iOS e tvOS. Essa extensão fornece a funcionalidade para adicionar a instância do rastreador a um site ou projeto de tag. A extensão do MA também requer a extensão do Analytics e a extensão da ID da Experience Cloud.

* [Extensão do Analytics versão 1.6 ou superior](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=pt-BR) — Essa extensão permite carregar a biblioteca JavaScript do SDK da Web da Adobe Experience Platform para enviar dados para soluções da Adobe.

* [Extensão da ID da Experience Cloud](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=pt-BR) — Essa extensão implementa o Serviço de ID da Experience Cloud, que identifica visitantes em todas as soluções da Experience Cloud. O serviço do Experience Cloud ID é uma extensão de personalização na Adobe Experience Platform.
