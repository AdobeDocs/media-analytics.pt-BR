---
title: Visão geral da mídia de transmissão do Adobe
description: Use as soluções Adobe para mídia de transmissão para obter insight avançados para conteúdo, áudio e anúncios.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/EJ6osO9PkXBubSF7a7HebRJhpSTamNnghofASOs7E-E
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: c8add8f2-4250-4fd9-9cde-9707036c567d
  - id: df312454-73c4-43f6-a90e-18f5043f074c
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5520579-b31f-4df7-9281-f0d9f91e2edc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 606
ht-degree: 53%

---

# Visão geral dos serviços de streaming de mídia da Adobe

![Banner](./assets/media_analytics_banner.png)

Os serviços de streaming de mídia da Adobe fornecem ferramentas eficientes de coleta, medição e personalização de conteúdo de streaming de mídia, como áudio, vídeo e anúncios para provedores de streaming de mídia. Você pode combinar métricas de transmissão de mídia com recursos como Audience Analytics, Mobile ou Cross-Device Analytics.

Os dados de mídia de transmissão se integram facilmente aos seguintes produtos da Adobe Experience Platform:

* Adobe Analytics

* Customer Journey Analytics

* Adobe Journey Optimizer

* Real-Time Customer Data Platform

>[!IMPORTANT]
>
>Para implementar os serviços de mídia de transmissão, entre em contato com o representante de vendas da Adobe ou com a equipe de conta da Adobe para garantir que o complemento Customer Journey Analytics Streaming Media Collection ou Adobe Analytics for Streaming Media Add-on faça parte do seu portfólio de produtos.

## Recursos principais

Os benefícios dos serviços de mídia de transmissão incluem monitoramento em tempo real, análise detalhada, insights acionáveis, oportunidades de monetização e muito mais.

* **Análise em tempo real**: tome decisões acionáveis em tempo real, utilizando as principais métricas de desempenho, como inicializações de mídia, em vários canais.

  Com os serviços de mídia de transmissão, você obtém detalhes precisos sobre duração, interrupções e inicializações quase em tempo real, o que permite avaliar e combinar métricas de vídeo e áudio. Esses insights permitem entender os hábitos de visualização e acompanhamento de seus clientes e aumentar o engajamento com recomendações altamente personalizadas.

* **Promover o engajamento**: envolva totalmente os usuários com menos eventos de buffer e entenda onde e quando os anúncios devem ser exibidos no conteúdo para fornecer uma experiência fluida e menos intrusiva, o que resulta no retorno de usuários.

* **Imagem holística**: combine vários pontos de dados em todos os distribuidores de conteúdo para obter uma visão completa de todas as atividades de mídia. Meça o engajamento e as visualizações/escutas em todos os canais possíveis.

  Os serviços de mídia de transmissão permitem rastrear a jornada completa do cliente em todo o site e nos aplicativos de transmissão para visualizar o caminho e os interesses do cliente, além de fornecer recomendações aprimoradas e personalizar as experiências do cliente.  A medição de mídia permite categorizar seus dados em várias dimensões e segmentos, capturando todos os metadados necessários para fazer uma análise completa e detalhada. Em seguida, você pode analisar dados e atribuir critérios de sucesso a mídias totalmente consumidas, tempo médio gasto e anúncios concluídos.

* **Métricas essenciais**: meça as métricas essenciais de entrega relacionadas à Qualidade da experiência (QoE), como quadros ignorados, tempo gasto no buffering e taxa média de bits.

* **Mais granularidade**: avalie o comportamento de visualização em mais detalhes, incluindo a hora de visita do visitante individual, os visualizadores/ouvintes simultâneos por minuto e a duração média do conteúdo consumido.

* **Medição precisa**: meça os vários dispositivos usados para o consumo de mídia, incluindo OTT, smartphones, tablets, dispositivos de desktop e muito mais, permitindo monitorar os padrões e hábitos de engajamento do usuário.

* **Segmentação**: aplique classificações a seus players, dispositivos, gêneros, capítulos e séries para observar o impacto de cada um em suas visualizações/acompanhamentos gerais e no engajamento do cliente com o conteúdo, áudio, anúncios e combinações.


## Como funciona

Os dados de rastreamento dos serviços de mídia de transmissão são coletados de um player usando a Extensão/SDK do Media para Edge Network, a Extensão de mídia com tags, os SDKs de mídia, a API do Media Edge ou a API da coleção de mídia.

Todos os dados granulares (até 10 segundos) são enviados para o Media Analytics Service ou para o Experience Edge (dependendo do [método de implementação](/help/implementation/overview.md) de sua escolha), que coletam e processam os dados para cada sessão de reprodução individual.

Após o término de uma sessão de reprodução, os dados de rastreamento calculados são enviados ao Adobe Analytics ou ao Customer Journey Analytics para armazenamento e produção de relatórios.

>[!NOTE]
>
>Com as implementações do Customer Journey Analytics, os dados podem ser enviados para o Customer Journey Analytics usando o Experience Edge ou o Conector de dados do Analytics (ADC).


Para obter informações detalhadas sobre os vários métodos de implementação, consulte [Implementar serviços de mídia de transmissão para Adobe Analytics ou Customer Journey Analytics](/help/implementation/overview.md).
