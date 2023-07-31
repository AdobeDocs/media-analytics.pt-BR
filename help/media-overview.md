---
title: Visão geral do Adobe Analytics para mídia de streaming
description: Use o Analytics para mídia de streaming e obtenha insights avançados de conteúdo, áudio e anúncios.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b12e6547ef32bfad7e8d6787a26d6467bcfeb23c
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 71%

---

# Visão geral do Adobe Analytics para mídia de streaming

![Banner](./assets/media_analytics_banner.png)

O Adobe Analytics para mídia de streaming fornece ferramentas eficientes de medição para áudio, vídeo e anúncios. Você pode combinar métricas de mídia de streaming com outros recursos do Adobe Analytics, como o Analytics para dispositivos móveis, Audience Analytics ou Cross-Device Analytics.

A mídia de transmissão pode ser adquirida como um complemento do Adobe Analytics<!-- update this when SKUs are available for other AEP products -->, e as métricas de mídia de transmissão se integram facilmente aos seguintes produtos da Adobe Experience Platform:

* Adobe Analytics

* Customer Journey Analytics

* Adobe Journey Optimizer

* Real-Time Customer Data Platform

>[!IMPORTANT]
>
>Para implementar a mídia de streaming do Adobe Analytics, entre em contato com o representante de vendas da Adobe ou com a equipe de contas da Adobe e garanta que a Mídia de streaming faça parte do seu portfólio de produtos.

## Recursos principais

Os benefícios do Adobe Analytics para mídia de streaming incluem monitoramento em tempo real, análise detalhada, insights acionáveis, oportunidades de monetização e muito mais.

* **Análise em tempo real**: tome decisões acionáveis em tempo real, utilizando as principais métricas de desempenho, como inicializações de mídia, em vários canais.

  Com o Analytics para Mídia de streaming, você obtém detalhes precisos sobre duração, interrupções e inicializações quase em tempo real, o que permite avaliar e combinar métricas de vídeo e áudio. Esses insights permitem entender os hábitos de visualização e acompanhamento de seus clientes e aumentar o engajamento com recomendações altamente personalizadas.

* **Promover o engajamento**: envolva totalmente os usuários com menos eventos de buffer e entenda onde e quando os anúncios devem ser exibidos no conteúdo para fornecer uma experiência fluida e menos intrusiva, o que resulta no retorno de usuários.

* **Imagem holística**: combine vários pontos de dados em todos os distribuidores de conteúdo para obter uma visão completa de todas as atividades de mídia. Meça o engajamento e as visualizações/escutas em todos os canais possíveis.

  O Adobe Analytics para mídia de streaming permite rastrear a jornada completa do cliente em seu site e aplicativos de transmissão para visualizar o caminho e os interesses do cliente, além de fornecer recomendações aprimoradas e personalizar as experiências do cliente.  A medição de mídia permite categorizar seus dados em várias dimensões e segmentos, capturando todos os metadados necessários para fazer uma análise completa e detalhada. Em seguida, você pode analisar dados e atribuir critérios de sucesso a mídias totalmente consumidas, tempo médio gasto e anúncios concluídos.

* **Métricas vitais**: meça as métricas essenciais de entrega relacionadas à Qualidade de experiência (QoE), como quadros ignorados, tempo gasto no buffering e taxa média de bits.

* **Mais granularidade**: avalie o comportamento de visualização em mais detalhes, incluindo a hora de visita do visitante individual, os visualizadores/ouvintes simultâneos por minuto e a duração média do conteúdo consumido.

* **Medição precisa**: meça os vários dispositivos usados para o consumo de mídia, incluindo OTT, smartphones, tablets, dispositivos de desktop e muito mais, permitindo monitorar os padrões e hábitos de engajamento do usuário.

* **Segmentação**: aplique classificações a seus players, dispositivos, gêneros, capítulos e séries para observar o impacto de cada um em suas visualizações/acompanhamentos gerais e no engajamento do cliente com o conteúdo, áudio, anúncios e combinações.


## Como funciona

Os dados de rastreamento de mídia de streaming são coletados de um player usando o SDK/Extensão Mídia para rede de borda, a Extensão de mídia com tags, os SDKs de mídia, a API de borda de mídia ou a API da coleção de mídia.

Todos os dados granulares (até 10 segundos) são enviados para o Media Analytics Service ou para o Experience Edge (dependendo do [método de implementação](/help/implementation/overview.md) de sua escolha), que coletam e processam os dados para cada sessão de reprodução individual.

Após o término de uma sessão de reprodução, os dados de rastreamento calculados são enviados ao Adobe Analytics ou ao Customer Journey Analytics para armazenamento e produção de relatórios.

>[!NOTE]
>
>Com as implementações do Customer Journey Analytics, os dados podem ser enviados para o Customer Journey Analytics usando o Experience Edge ou o Conector de dados do Analytics (ADC).


Para obter informações detalhadas sobre os vários métodos de implementação, consulte [Implementar mídia de transmissão para Adobe Analytics ou Customer Journey Analytics](/help/implementation/overview.md).
