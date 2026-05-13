---
title: Quais caminhos de implementação de transmissão de mídia estão disponíveis?
description: Saiba mais sobre os caminhos de implementação para o Streaming de Mídia da Adobe, incluindo a Coleção de dados da Adobe Experience Platform.
exl-id: eee70e62-ba45-440a-8ce1-e151b66d2c1f
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/U9PBQc7dHNmONZc06t1Xi7EITkveGUkzcst6Sakqqzo
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: eb9732ab-8232-4b21-bc4c-89de86dbe4d7id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: df312454-73c4-43f6-a90e-18f5043f074c
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 676
ht-degree: 87%

---

# Caminhos de implementação {#implementation-paths}

**ESTE CONTEÚDO FOI MOVIDO PARA O ARQUIVO DE CAMINHOS DE IMPLEMENTAÇÃO ATUAL**

Para cada caminho de implementação, os clientes precisam entrar em contato com o representante de vendas ou a equipe de conta da Adobe para assinar uma nova ordem de vendas, pois a coleção de streaming de mídia da Customer Journey Analytics e o Adobe Analytics para streaming de mídia têm uma SKU exclusiva e seus preços variam de acordo com o modelo, com base em chamadas de servidor e fluxos de vídeo.

## Coleção de dados da Adobe Experience Platform com a extensão do Adobe Media Analytics

>[!NOTE]
>A Adobe Experience Platform Launch está sendo reformulada como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=pt-BR) para obter uma referência consolidada das alterações de terminologia.


As tags no Adobe Experience Platform são a última palavra em gerenciamento de tags da Adobe. As tags oferecem aos clientes uma forma simples de implantar e gerenciar todas as tags de análise, de marketing e de anúncios necessárias para potencializar experiências relevantes do cliente. As tags são fornecidas aos clientes da Adobe Experience Cloud como um recurso incluso com valor agregado.

As tags capacitam qualquer pessoa a criar e manter suas próprias integrações, chamadas de extensões. Essas extensões estão disponíveis para os clientes da Adobe Experience Cloud numa experiência de loja de aplicativos, para que possam instalar, configurar e implantar tags com rapidez.

Uma extensão é um pacote de código (JavaScript, HTML e CSS) que estende a funcionalidade das tags. Crie, gerencie e atualize suas integrações usando uma interface de autoatendimento virtual. Pense nas extensões como aplicativos usados para realizar as tarefas.Para obter mais informações, consulte o artigo *Visão geral das tags* na [Documentação do Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR)

A extensão do Adobe Media Analytics (MA) adiciona o Media SDK JavaScript principal (Media SDK 2.x) para áudio e vídeo. Esta extensão fornece a funcionalidade de adicionar a instância do rastreador `MediaHeartbeat` a um site ou projeto de Coleção de dados.

A Coleção de dados da Adobe com a extensão do Media Analytics exige o seguinte:
* Você deve ser um cliente da Adobe Experience Cloud.
* Você deve implantar o código incorporado de Coleção de dados ou DTM nas páginas da Web.
* [Extensão do Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=pt-BR)
* [Extensão do Experience Cloud ID](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=pt-BR)


## Lado do cliente

Essas são integrações exclusivas do Media Analytics. Você pode escolher o SDK do Video Heartbeat e/ou as integrações da API da coleção do Media. Esse caminho pode ser usado em qualquer player de vídeo, incluindo players de clientes e/ou de OVP, como Brightcove, Ooyala, thePlatform e assim por diante.

Se o Media Analytics for o seu caminho pretendido, consulte a [Implementação de SDK do Media](/help/legacy/setup/legacy-setup-overview.md) e a [API da coleção do Media.](/help/implementation/media-collection-api/mc-api-overview.md)

>[!IMPORTANT]
>Para usar o Media Analytics, os clientes também precisam usar o Adobe Analytics.

## Adobe Primetime

O Adobe Primetime é uma solução da Adobe Experience Cloud que ajuda os programadores e distribuidores de conteúdo a monetizar mídia em cada tela conectada.

O Primetime elimina a complexidade de alcançar, monetizar e ativar públicos-alvo globais nos dispositivos, fornecendo uma plataforma modular para a publicação, a publicidade, a personalização e a análise de vídeo. Além disso, o Primetime oferece soluções e valor em torno do seguinte:

* Suporte para medir com precisão os tipos de conteúdo Linear e VOD.
* Suporte para medir quebras de anúncios com (ou sem) inserção dinâmica de anúncios.
* O modelo de inserção contínua de anúncios do TVSDK permite análises que avaliam diretamente a reprodução do anúncio, o que aumenta a precisão.
* Conjunto robusto de eventos e metadados para garantir a precisão em problemas de buffering de QoS ou interrupções de conectividade móvel e interações do usuário final, como busca, pausa e background em dispositivos móveis.
* Suporte integrado para DTVR Nielsen (linear) com metadados ID3 e DCR com metadados CMS.


O TVSDK já está integrado ao SDK do Media Analytics (Heartbeats), o que torna a implementação muito mais fácil e rápida em todas as plataformas compatíveis. Para aproveitar o Primetime, siga as mesmas diretrizes e pré-requisitos encontrados [no lado do cliente](/help/legacy/intro-to-ava/implementation-paths/client-side-path.md), juntamente com os seguintes documentos para sua(s) plataforma(s): [Guia do usuário do Primetime.](https://helpx.adobe.com/br/support/primetime.html)

Você também deve entrar em contato com um representante de vendas/gerente de conta para saber como adquirir o TVSDK.
