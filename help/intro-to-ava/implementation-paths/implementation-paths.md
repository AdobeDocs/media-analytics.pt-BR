---
title: Quais caminhos de implementação de transmissão de mídia estão disponíveis?
description: Saiba mais sobre os caminhos de implementação da Mídia de transmissão do Adobe, incluindo a Coleta de dados do Adobe Experience Platform.
exl-id: eee70e62-ba45-440a-8ce1-e151b66d2c1f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: f88e8b02bc9723793822fa7647a2ceab9ada45e6
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 79%

---

# Caminhos de implementação {#implementation-paths}

Para cada caminho de implementação, os clientes precisam entrar em contato com o representante de vendas/gerente de conta para assinar uma nova ordem de vendas, pois o Streaming Media Analytics tem uma SKU única e seus preços variam de acordo com o modelo, com base em chamadas de servidor e fluxos de vídeo.

## Coleta de dados do Adobe Experience Platform com a extensão do Adobe Medium Analytics

>[!NOTE]
>A Adobe Experience Platform Launch está sendo reformulada como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=pt-BR) para obter uma referência consolidada das alterações de terminologia.


As tags no Adobe Experience Platform são a última palavra em gerenciamento de tags da Adobe. As tags oferecem aos clientes uma forma simples de implantar e gerenciar todas as tags de análise, de marketing e de anúncios necessárias para potencializar experiências de cliente relevantes. Tags são oferecidas aos clientes da Adobe Experience Cloud como um recurso incluído de valor agregado.

As tags capacitam qualquer pessoa a criar e manter suas próprias integrações, chamadas de extensões. Essas extensões estão disponíveis aos clientes da Adobe Experience Cloud por uma experiência de loja de aplicativos, para que possam instalar, configurar e implantar tags com rapidez.

Uma extensão é um pacote de código (JavaScript, HTML e CSS) que estende a funcionalidade das tags. Crie, gerencie e atualize suas integrações usando uma interface de autoatendimento virtual. Pense nas extensões como aplicativos usados para realizar suas tarefas.Para obter mais informações, consulte o *Visão geral das tags* artigo na [Documentação do Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR)

A extensão do Adobe Media Analytics (MA) adiciona o principal SDK de mídia JavaScript (SDK do Media 2.x) para áudio e vídeo. Essa extensão fornece a funcionalidade necessária para adicionar a variável `MediaHeartbeat` instância do rastreador para um site ou projeto de Coleta de dados.

A coleta de dados do Adobe com a extensão do Media Analytics exige o seguinte:
* Você deve ser um cliente da Adobe Experience Cloud.
* Você deve implantar a Coleta de dados ou o código de inserção do DTM nas páginas da Web.
* [Extensão do Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=pt-BR)
* [Extensão do Experience Cloud ID](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=pt-BR)


## Lado do cliente

Essas são integrações exclusivas do Media Analytics. Você pode escolher o SDK do Video Heartbeat e/ou as integrações da API da coleção do Media. Esse caminho pode ser usado em qualquer player de vídeo, incluindo players de clientes e/ou de OVP, como Brightcove, Ooyala, thePlatform e assim por diante.

Se o Media Analytics for o seu caminho pretendido, consulte a [Implementação de SDK do Media](/help/sdk-implement/setup/setup-overview.md) e a [API da coleção do Media.](/help/media-collection-api/mc-api-overview.md)

>[!IMPORTANT]
>Para usar o Media Analytics, os clientes também precisam usar o Adobe Analytics.

## Adobe Primetime

O Adobe Primetime é uma solução da Adobe Experience Cloud que ajuda os programadores e distribuidores de conteúdo a monetizar mídia em cada tela conectada.

O Primetime elimina a complexidade de alcançar, monetizar e ativar públicos-alvo globais nos dispositivos, fornecendo uma plataforma modular para a publicação, a publicidade, a personalização e a análise de vídeo. Além disso, o Primetime oferece soluções e valor em torno do seguinte:

* Suporte para medir com precisão os tipos de conteúdo Linear e VOD.
* Suporte para medir quebras de anúncios com (ou sem) inserção dinâmica de anúncios.
* O modelo de inserção contínua de anúncios do TVSDK permite análises que avaliam diretamente a reprodução do anúncio, o que aumenta a precisão.
* Conjunto robusto de eventos e metadados para garantir a precisão em problemas de buffering de QoS ou interrupções de conectividade móvel e interações do usuário final, como busca, pausa e background em dispositivos móveis.
* Suporte integrado ao DTVR (linear) da Nielsen com metadados ID3 e DCR com metadados CMS.


O TVSDK já está integrado ao SDK do Media Analytics (Heartbeats), o que torna a implementação muito mais fácil e rápida em todas as plataformas compatíveis. Para aproveitar o Primetime, siga as mesmas diretrizes e pré-requisitos encontrados [no lado do cliente,](/help/intro-to-ava/implementation-paths/client-side-path.md) juntamente com os seguintes documentos para sua(s) plataforma(s): [Guia do usuário do Primetime.](https://helpx.adobe.com/br/support/primetime.html)

Você também deve entrar em contato com o Representante de vendas/Gerente de conta para saber como adquirir o TVSDK.
