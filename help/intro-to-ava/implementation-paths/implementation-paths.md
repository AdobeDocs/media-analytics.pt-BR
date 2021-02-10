---
title: Quais caminhos de implementação de transmissão de mídia estão disponíveis?
description: Saiba mais sobre os caminhos de implementação de transmissão de mídia da Adobe, incluindo o Adobe Launch.
translation-type: ht
source-git-commit: 901539a2095b23f9108a934eb61d182b14ccd9e8
workflow-type: ht
source-wordcount: '505'
ht-degree: 100%

---


# Caminhos de implementação {#implementation-paths}

Para cada caminho de implementação, os clientes precisam entrar em contato com o representante de vendas/gerente de conta para assinar uma nova ordem de vendas, pois o Streaming Media Analytics tem uma SKU única e seus preços variam de acordo com o modelo, com base em chamadas de servidor e fluxos de vídeo.

* **Adobe Launch com a extensão do Adobe Media Analytics**

   O Adobe Launch é a solução de gerenciamento de tags de última geração da Adobe. O Launch oferece uma forma simples de implantar e gerenciar todas as tags de análise, marketing e anúncios necessárias para enriquecer as experiências de clientes relevantes. Para criar e manter suas próprias integrações com o Launch, use extensões. Uma extensão é um pacote de JavaScript, HTML e CSS que estende a funcionalidade do cliente e da interface do usuário do Launch. Para obter mais informações, consulte o [Guia do usuário da Experience Platform Launch](https://docs.adobe.com/content/help/pt-BR/launch/using/overview.html)

   A extensão do Adobe Media Analytics (MA) adiciona o principal SDK de mídia JavaScript (SDK do Media 2.x) para áudio e vídeo. Esta extensão fornece a funcionalidade necessária para adicionar a instância do rastreador `MediaHeartbeat` a um site ou projeto do Launch.

   O Adobe Launch com a extensão do Media Analytics exige o seguinte:
   * Você deve ser um cliente da Adobe Experience Cloud.
   * Você deve implantar o código de incorporação do Launch ou DTM nas páginas da Web.
   * [Extensão do Analytics](https://docs.adobe.com/content/help/pt-BR/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html)
   * [Extensão do Experience Cloud ID](https://docs.adobe.com/content/help/pt-BR/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)


* **Lado do cliente -** Estas são integrações exclusivas do Media Analytics. Você pode escolher o SDK do Video Heartbeat e/ou as integrações da API da coleção do Media. Esse caminho pode ser usado em qualquer player de vídeo, incluindo players de clientes e/ou de OVP, como Brightcove, Ooyala, thePlatform e assim por diante.

   Se o Media Analytics for o seu caminho pretendido, consulte a [Implementação de SDK do Media](/help/sdk-implement/setup/setup-overview.md) e a [API da coleção do Media.](/help/media-collection-api/mc-api-overview.md)

   >[!IMPORTANT]
   >
   >Para usar o Media Analytics, os clientes também precisam usar o Adobe Analytics.

* **Adobe Primetime -** O Adobe Primetime é uma solução da Adobe Experience Cloud que ajuda os programadores e distribuidores de conteúdo a monetizar mídia em cada tela conectada.

   O Primetime elimina a complexidade de alcançar, monetizar e ativar públicos-alvo globais nos dispositivos, fornecendo uma plataforma modular para a publicação, a publicidade, a personalização e a análise de vídeo. Além disso, o Primetime oferece soluções e valor em torno do seguinte:

   * Suporte para medir com precisão os tipos de conteúdo Linear e VOD.
   * Suporte para medir quebras de anúncios com (ou sem) inserção dinâmica de anúncios.
   * O modelo de inserção contínua de anúncios do TVSDK permite análises que avaliam diretamente a reprodução do anúncio, o que aumenta a precisão.
   * Conjunto robusto de eventos e metadados para garantir a precisão em problemas de buffering de QoS ou interrupções de conectividade móvel e interações do usuário final, como busca, pausa e background em dispositivos móveis.

<!--
   * Integrated support for Nielsen DTVR (linear) with ID3 metadata and DCR with CMS metadata.
-->

O TVSDK já está integrado ao SDK do Media Analytics (Heartbeats), o que torna a implementação muito mais fácil e rápida em todas as plataformas compatíveis. <!--Primetime also supports the partnership with Nielsen.--> Para aproveitar o Primetime, siga as mesmas diretrizes e pré-requisitos encontrados [no lado do cliente,](/help/intro-to-ava/implementation-paths/client-side-path.md) juntamente com os seguintes documentos para sua(s) plataforma(s): [Guia do usuário do Primetime.](https://helpx.adobe.com/br/support/primetime.html)

Você também deve entrar em contato com o Representante de vendas/Gerente de conta para saber como adquirir o TVSDK.
