---
title: Visão geral do complemento Coleção de mídia de transmissão do Adobe
description: Use o complemento Coleção de mídia de streaming para obter insights avançados de conteúdo, áudio e anúncios.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 64%

---

# Visão geral do complemento Coleção de mídia de transmissão do Adobe

![Banner](./assets/media_analytics_banner.png)

O complemento Adobe Streaming Media Collection fornece ferramentas eficientes de coleção, medição e personalização para streaming de conteúdo de mídia, como áudio, vídeo e anúncio para provedores de streaming de mídia. Você pode combinar métricas de transmissão de mídia com recursos como Audience Analytics, Mobile ou Cross-Device Analytics.

Os dados de mídia de transmissão se integram facilmente aos seguintes produtos da Adobe Experience Platform:

* Adobe Analytics

* Customer Journey Analytics

* Adobe Journey Optimizer

* Real-Time Customer Data Platform

>[!IMPORTANT]
>
>Para implementar a coleção de mídia de transmissão, entre em contato com o representante de vendas da Adobe ou com a equipe de conta da Adobe para garantir que o complemento Coleção de mídia de transmissão faça parte do seu portfólio de produtos.

## Recursos principais

Os benefícios do complemento de coleção de mídia de transmissão incluem monitoramento em tempo real, análise detalhada, insights acionáveis, oportunidades de monetização e muito mais.

* **Análise em tempo real**: tome decisões acionáveis em tempo real, utilizando as principais métricas de desempenho, como inicializações de mídia, em vários canais.

  Com o complemento Coleção de mídia de streaming, você obtém detalhes precisos sobre duração, interrupções e inicializações quase em tempo real, que permitem avaliar e combinar métricas de vídeo e áudio. Esses insights permitem entender os hábitos de visualização e acompanhamento de seus clientes e aumentar o engajamento com recomendações altamente personalizadas.

* **Promover o engajamento**: envolva totalmente os usuários com menos eventos de buffer e entenda onde e quando os anúncios devem ser exibidos no conteúdo para fornecer uma experiência fluida e menos intrusiva, o que resulta no retorno de usuários.

* **Visão integral**: combine vários pontos de dados em todos os distribuidores de conteúdo para obter uma visão completa de todas as atividades de mídia. Além disso, meça o engajamento e as visualizações/acompanhamentos em todos os canais possíveis.

  O complemento Coleção de mídia de transmissão permite rastrear a jornada completa do cliente em seu site e aplicativos de transmissão para visualizar o caminho e os interesses do cliente, além de fornecer recomendações aprimoradas e personalizar as experiências do cliente.  A medição de mídia permite categorizar seus dados em várias dimensões e segmentos, capturando todos os metadados necessários para fazer uma análise completa e detalhada. Em seguida, você pode analisar dados e atribuir critérios de sucesso a mídias totalmente consumidas, tempo médio gasto e anúncios concluídos.

* **Métricas essenciais**: meça as métricas essenciais de entrega relacionadas à Qualidade da experiência (QoE), como quadros ignorados, tempo gasto no buffering e taxa média de bits.

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


Para obter informações detalhadas sobre os vários métodos de implementação, consulte [Implementar o Complemento de Coleção de Mídia de Streaming para Adobe Analytics ou Customer Journey Analytics](/help/implementation/overview.md).
