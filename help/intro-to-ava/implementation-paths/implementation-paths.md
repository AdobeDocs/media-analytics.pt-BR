---
seo-title: Caminhos de implementação
title: Caminhos de implementação
uuid: 8400c938-e77e-4c88-b23b-5f5977a5316c
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Caminhos de implementação {#implementation-paths}

O Media Analytics (Heartbeats) é a solução de vídeo padronizada da Adobe. Substituiu o modelo de marcos mais antigo da Adobe.

Para cada um desses caminhos de implementação, os clientes precisam entrar em contato com o representante de vendas/gerente de conta para assinar uma nova Ordem de venda, já que o Media Analytics tem um SKU exclusivo e muda de um modelo de preços com base em chamadas de servidor para um modelo com base em streams de vídeo:

* **Cliente - São integrações somente do Media Analytics** . Você pode escolher o SDK do Video Heartbeat e/ou as integrações da API da coleção de mídia. Esse caminho pode ser usado em qualquer reprodutor de vídeo, incluindo reprodutores cliente e/ou OVP, como Brightcove, Ooyala, thePlatform, etc.

   If Media Analytics is your intended path, see the [Media SDK Implementation](/help/sdk-implement/setup/setup-overview.md) and the [Media Collection API.](/help/media-collection-api/mc-api-overview.md)

   >[!IMPORTANT]
   >
   >Para usar o Media Analytics, os clientes também devem usar o Adobe Analytics.

* **Adobe Experience Platform Launch - o Adobe Experience Platform Launch, o produto subsequente ao Gerenciamento dinâmico de tags, apresenta uma Extensão de lançamento do Media Analytics que facilita a implementação do rastreamento de vídeo nos players.**

   Saiba mais sobre o Experience Platform Launch aqui: Extensão de áudio e vídeo do [Adobe Media Analytics](https://docs.adobelaunch.com/extension-reference/web/adobe-media-analytics-for-audio-and-video-extension)
* **O Adobe Primetime -** Adobe Primetime é uma solução da Adobe Experience Cloud que ajuda os programadores e distribuidores de conteúdo a monetizar mídia em cada tela conectada.

   O Primetime elimina a complexidade de alcançar, monetizar e ativar públicos globais nos dispositivos, fornecendo uma plataforma modular para a publicação, a publicidade, a personalização e a análise de vídeos. Além disso, o Primetime oferece soluções e valor em relação ao seguinte:

   * Suporte para avaliar com precisão os tipos de conteúdo Linear e VOD.
   * Suporte para avaliar ad breaks com (ou sem) inserção dinâmica de anúncios.
   * O modelo perfeito de inserção de anúncios do TVSDK permite realizar análises que avaliam diretamente a reprodução do anúncio, o que aumenta a precisão.
   * Conjunto robusto de eventos e metadados para garantir a precisão entre o buffer de QoS ou problemas de interrupções de conectividade móvel e as interações do usuário final, como buscar, pausar e colocar em segundo plano em dispositivos móveis.
   * Suporte integrado ao DTVR (linear) da Nielsen com metadados ID3 e DCR com metadados CMS.
   O TVSDK já está integrado ao SDK do Media Analytics (Heartbeats), o que torna a implementação muito mais fácil e rápida em todas as plataformas suportadas. O Primetime também oferece suporte à parceria com a Nielsen. Para utilizar o Primetime, siga as mesmas diretrizes e pré-requisitos descritos em  [Lado do cliente](/help/intro-to-ava/implementation-paths/client-side-path.md), juntamente com os seguintes documentos para a(s) plataforma(s): Guia do usuário do [Primetime.](https://helpx.adobe.com/primetime/user-guide.html)

   Você também deve entrar em contato com o Representante de vendas/Gerente de conta para saber como adquirir o TVSDK.
