---
title: Visão geral do Adobe Analytics para mídia de streaming
description: Use o Analytics para mídia de streaming e obtenha insights avançados de conteúdo, áudio e anúncios.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 984f058fda15b1c5e960e4c8d8e2378308d2b541
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 65%

---

# Visão geral do Adobe Analytics para mídia de streaming

![Banner](./assets/media_analytics_banner.png)

O Adobe Analytics para mídia de streaming é um complemento do Adobe Analytics e do Customer Journey Analytics que fornece ferramentas eficientes de medição para áudio, vídeo e anúncios. Com o Analytics para mídia de streaming, você obtém detalhes precisos sobre duração, interrupções e inicializações quase em tempo real, o que permite avaliar e combinar métricas de vídeo e áudio. Esses insights permitem entender os hábitos de visualização e acompanhamento de seus clientes e aumentar o engajamento com recomendações altamente personalizadas.

O Adobe Analytics para mídia de streaming permite acompanhar a jornada do cliente completa em seu site e aplicativos de streaming. Você pode combinar métricas de mídia de streaming com outros recursos do Adobe Analytics, como o Analytics para dispositivos móveis, Audience Analytics ou Cross-Device Analytics. Essas métricas se integram facilmente aos relatórios do Adobe Analytics e a outros produtos da Adobe Experience Platform. A medição de mídia permite categorizar seus dados em várias dimensões e segmentos, capturando todos os metadados necessários para fazer uma análise completa e detalhada. Em seguida, você pode analisar dados e atribuir critérios de sucesso a mídias totalmente consumidas, tempo médio gasto e anúncios concluídos.

Você pode medir métricas essenciais de entrega relacionadas à Qualidade de experiência (QoE), como quadros ignorados, tempo gasto no buffering e taxa média de bits. Adicionalmente, as métricas podem ser combinadas com os dados do seu site ou aplicativo para visualizar o caminho e os interesses do cliente, o que permite fornecer recomendações aprimoradas e personalizar a experiência dos clientes usando a Adobe Experience Platform.

>[!IMPORTANT]
>
>Para implementar a transmissão de mídia da Adobe Analytics, entre em contato com o representante de vendas da Adobe ou com a equipe de conta da Adobe para garantir que a transmissão de mídia faça parte do seu portfólio de produtos.


## Como funciona

Os dados de rastreamento de mídia de transmissão são coletados de um player usando a Extensão/SDK de rede de borda, a Extensão de mídia com tags, SDKs de mídia, API de borda de mídia ou a API de coleção de mídia.

Todos os dados granulares (até 10 segundos) são enviados para o Media Analytics Service ou para a Experience Edge (dependendo da [método de implementação](/help/implementation/overview.md) você escolher), que coletam e processam os dados de cada sessão de reprodução individual.

Após o término de uma sessão de reprodução, os dados de rastreamento calculados são enviados ao Adobe Analytics ou ao Customer Journey Analytics para armazenamento e relatórios.

>[!NOTE]
>
>Com implementações de Customer Journey Analytics, os dados podem ser enviados para o Customer Journey Analytics usando o Experience Edge ou o ADC (Conector de dados Analytics).


Consulte [Implementar mídia de transmissão para Adobe Analytics ou Customer Journey Analytics](/help/implementation/overview.md) para obter mais informações.

## Recursos

Os benefícios do Adobe Analytics para streaming de mídia incluem monitoramento em tempo real, análise detalhada, insights acionáveis e oportunidades de monetização.

* **Análise em tempo real**: tome decisões acionáveis em tempo real, utilizando as principais métricas de desempenho, como inicializações de mídia, em vários canais.

* **Promover o engajamento**: envolva totalmente os usuários com menos eventos de buffer e entenda onde e quando os anúncios devem ser exibidos no conteúdo para fornecer uma experiência fluida e menos intrusiva, o que resulta no retorno de usuários.

* **Visão integral**: combine vários pontos de dados em todos os distribuidores de conteúdo para obter uma visão completa de todas as atividades de mídia. Além disso, meça o engajamento e as visualizações/acompanhamentos em todos os canais possíveis por meio do recurso do Federated Analytics.

* **Mais granularidade**: avalie o comportamento de visualização em mais detalhes, incluindo a hora de visita do visitante individual, os visualizadores/ouvintes simultâneos por minuto e a duração média do conteúdo consumido.

* **Medição precisa**: meça os vários dispositivos usados para o consumo de mídia, incluindo OTT, smartphones, tablets, dispositivos de desktop e muito mais, permitindo monitorar os padrões e hábitos de engajamento do usuário.

* **Segmentação**: aplique classificações a seus players, dispositivos, gêneros, capítulos e séries para observar o impacto de cada um em suas visualizações/acompanhamentos gerais e no engajamento do cliente com o conteúdo, áudio, anúncios e combinações.
