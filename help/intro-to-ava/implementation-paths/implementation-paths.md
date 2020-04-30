---
title: Caminhos de implementação
description: null
uuid: 8400c938-e77e-4c88-b23b-5f5977a5316c
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Caminhos de implementação {#implementation-paths}

O Media Analytics (Heartbeats) é a solução de vídeo padronizada da Adobe. Substituiu o modelo de marcos mais antigo da Adobe.

Para cada um desses caminhos de implementação, os clientes precisam entrar em contato com o representante de vendas/gerente de conta para assinar uma nova ordem de vendas, pois o Media Analytics tem uma SKU exclusiva e seus preços variam de acordo com o modelo, com base em chamadas de servidor e fluxos de vídeo:

* **Lado do cliente -** Estas são integrações exclusivas do Media Analytics. Você pode escolher o SDK do Video Heartbeat e/ou as integrações da API da coleção do Media. Esse caminho pode ser usado em qualquer player de vídeo, incluindo players de clientes e/ou de OVP, como Brightcove, Ooyala, thePlatform e assim por diante.

   Se o Media Analytics for o seu caminho pretendido, consulte a [Implementação de SDK do Media](/help/sdk-implement/setup/setup-overview.md) e a [API da coleção do Media.](/help/media-collection-api/mc-api-overview.md)

   >[!IMPORTANT]
   >
   >Para usar o Media Analytics, os clientes também precisam usar o Adobe Analytics.

* **Adobe Experience Platform Launch -** O Adobe Experience Platform Launch, o produto complementar ao Dynamic Tag Management, apresenta uma extensão de inicialização do Media Analytics que facilita a implementação do rastreamento de vídeo em seus reprodutores.

   Saiba mais sobre o Experience Platform Launch aqui: [Extensão de áudio e vídeo do Adobe Media Analytics](https://docs.adobe.com/content/help/pt-BR/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)
* **Adobe Primetime -** O Adobe Primetime é uma solução da Adobe Experience Cloud que ajuda os programadores e distribuidores de conteúdo a monetizar mídia em cada tela conectada.

   O Primetime elimina a complexidade de alcançar, monetizar e ativar públicos-alvo globais nos dispositivos, fornecendo uma plataforma modular para a publicação, a publicidade, a personalização e a análise de vídeo. Além disso, o Primetime oferece soluções e valor em torno do seguinte:

   * Suporte para medir com precisão os tipos de conteúdo Linear e VOD.
   * Suporte para medir quebras de anúncios com (ou sem) inserção dinâmica de anúncios.
   * O modelo de inserção contínua de anúncios do TVSDK permite análises que avaliam diretamente a reprodução do anúncio, o que aumenta a precisão.
   * Conjunto robusto de eventos e metadados para garantir a precisão em problemas de buffering de QoS ou interrupções de conectividade móvel e interações do usuário final, como busca, pausa e background em dispositivos móveis.
<!--
   * Integrated support for Nielsen DTVR (linear) with ID3 metadata and DCR with CMS metadata.
-->

O TVSDK já está integrado ao SDK do Media Analytics (Heartbeats), o que torna a implementação muito mais fácil e rápida em todas as plataformas compatíveis. <!--Primetime also supports the partnership with Nielsen.--> Para aproveitar o Primetime, siga as mesmas diretrizes e pré-requisitos encontrados [no lado do cliente,](/help/intro-to-ava/implementation-paths/client-side-path.md) juntamente com os seguintes documentos para sua(s) plataforma(s): [Guia do usuário do Primetime.](https://helpx.adobe.com/br/primetime/user-guide.html)

Você também deve entrar em contato com o Representante de vendas/Gerente de conta para saber como adquirir o TVSDK.
