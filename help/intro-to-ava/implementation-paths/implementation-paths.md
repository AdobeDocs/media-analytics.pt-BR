---
seo-title: Caminhos de implementação
title: Caminhos de implementação
uuid: 8400 c 938-e 77 e -4 c 88-b 23 b -5 f 5977 a 5316 c
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Caminhos de implementação {#implementation-paths}

O Media Analytics (Heartbeats) é uma solução de vídeo padronizada da Adobe. Substituiu o modelo de marcos mais antigo da Adobe.

Para cada um desses caminhos de implementação, os clientes precisam entrar em contato com o representante de vendas/Gerente de contas para assinar uma nova Ordem de vendas, pois o Media Analytics tem uma SKU exclusiva e muda de um modelo de preços baseado em chamadas do servidor para um modelo com base em fluxos de vídeo:

* **Lado do cliente -** são integrações somente do Analytics. Você pode escolher o SDK do Video Heartbeat e/ou as integrações da API da coleção de mídia. Esse caminho pode ser usado em qualquer reprodutor de vídeo, incluindo reprodutores cliente e/ou OVP, como Brightcove, Ooyala, thePlatform, etc.

   If Media Analytics is your intended path, see the [Media SDK Implementation](/help/sdk-implement/setup/setup-overview.md) and the [Media Collection API.](/help/media-collection-api/mc-api-overview.md)

   >[!IMPORTANT]
   >
   >Para usar o Media Analytics, os clientes também precisam usar o Adobe Analytics.

* **Adobe Experience Platform Launch -** Adobe Experience Platform Launch, o produto subsequente ao Gerenciamento dinâmico de tags, apresenta uma Extensão de lançamento do Media Analytics que facilita a implementação do rastreamento de vídeo nos seus players.

   You can learn more about Experience Platform Launch here: [Adobe Media Analytics for Audio and Video Extension](https://docs.adobelaunch.com/extension-reference/web/adobe-media-analytics-for-audio-and-video-extension)
* **Adobe Primetime -** O Adobe Primetime é uma solução da Adobe Experience Cloud que ajuda os programadores e os distribuidores de conteúdo a monetizarem mídia em todas as tela conectadas.

   O Primetime elimina a complexidade de alcançar, monetizar e ativar públicos globais nos dispositivos, fornecendo uma plataforma modular para a publicação, a publicidade, a personalização e a análise de vídeos. Além disso, o Primetime oferece soluções e valor em relação ao seguinte:

   * Suporte para avaliar com precisão os tipos de conteúdo Linear e VOD.
   * Suporte para avaliar ad breaks com (ou sem) inserção dinâmica de anúncios.
   * O modelo perfeito de inserção de anúncios do TVSDK permite realizar análises que avaliam diretamente a reprodução do anúncio, o que aumenta a precisão.
   * Conjunto robusto de eventos e metadados para garantir a precisão entre o buffer de QoS ou problemas de interrupções de conectividade móvel e as interações do usuário final, como buscar, pausar e colocar em segundo plano em dispositivos móveis.
   * Suporte integrado ao DTVR (linear) da Nielsen com metadados ID3 e DCR com metadados CMS.
   O TVSDK já está integrado ao SDK de mídia analógica (Heartbeats), o que torna a implementação muito mais fácil e rápida em cada plataforma compatível. O Primetime também oferece suporte à parceria com a Nielsen. Para utilizar o Primetime, siga as mesmas diretrizes e pré-requisitos descritos em  [Lado do cliente](/help/intro-to-ava/implementation-paths/client-side-path.md), juntamente com os seguintes documentos para a(s) plataforma(s): [Guia do usuário do Primetime.](https://helpx.adobe.com/primetime/user-guide.html)

   Você também deve entrar em contato com o Representante de vendas/Gerente de conta para saber como adquirir o TVSDK.
