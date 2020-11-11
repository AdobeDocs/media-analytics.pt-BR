---
title: Avaliação da transmissão de mídia no Adobe Analytics
description: O Adobe Analytics for Media (também conhecido como Media Analytics) fornece aos clientes medições de mídia robustas para conteúdo, áudio e anúncios.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
translation-type: tm+mt
source-git-commit: 82b38f7870b6f890aaa812de30fa2d02d4f3ba8a
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 85%

---


# Medir mídia de transmissão no Adobe Analytics{#measuring-audio-and-video-in-adobe-analytics}

![Banner](./assets/media_analytics_banner.png)

## Sobre o Adobe Analytics for Streaming Media

O Adobe Analytics for Streaming Media é um complemento ao Adobe Analytics que oferece ferramentas poderosas de medição para áudio, vídeo e anúncios. O Adobe Analytics faz parte da Adobe Experience Platform.

O Adobe Analytics for Streaming Media permite rastrear a jornada completa do cliente em seu site. As métricas se integram facilmente aos Relatórios do Adobe Analytics e a outros produtos da Adobe Experience Cloud. A medição de mídia permite categorizar seus dados em várias dimensões e segmentos, capturando todos os metadados necessários para fazer uma análise completa e detalhada. Em seguida, você pode analisar dados e atribuir critérios de sucesso a mídias totalmente consumidas, tempo médio gasto e anúncios concluídos.

Você pode medir métricas essenciais do delivery relacionadas a QoS, como quadros ignorados, tempo gasto no buffering e taxa média de bits. E as métricas podem ser combinadas com os dados do seu site ou aplicativo para visualizar o caminho e os interesses do cliente, para fornecer recomendações avançadas e personalizar as experiências do cliente usando a Adobe Experience Cloud.

## Recursos {#features}

Os benefícios da Adobe Analytics para a mídia de transmissão contínua incluem monitoramento em tempo real, análise detalhada, insights acionáveis e oportunidades de monetização.
* **Análise em tempo real**: tome decisões acionáveis em tempo real utilizando métricas chave de desempenho, como duração, ex2 e ex3, em vários canais. Os eventos de conteúdo principal são medidos em intervalos de 10 segundos para capturar todas as atividades que ocorrem. Os eventos de rastreamento de anúncios ocorrem em intervalos de 1 segundo.
* **Promover o engajamento**: envolva totalmente os usuários com menos eventos de buffer e entenda onde e quando os anúncios devem ser exibidos no conteúdo para fornecer uma experiência perfeita e menos intrusiva que oferece visitas repetidas.
* **Imagem holística**: combine vários pontos de dados em todos os distribuidores de conteúdo para obter uma visão completa de todas as atividades de mídia e medir o engajamento e as visualizações/escutas em todos os canais possíveis por meio do recurso Federated Analytics.
* **Mais granularidade**: avalie o comportamento de visualização no nível mais granular, incluindo o momento do dia do visitante individual, os visualizadores/ouvintes simultâneos por minuto e a duração média do conteúdo consumido.
* **Medição precisa**: meça os vários dispositivos usados para o consumo de mídia, incluindo OTT, smartphone, tablet, desktop e muito mais, para monitorar os padrões e os hábitos de engajamento do usuário.
* **Segmentação**: aplique classificações a seus players, dispositivos, gêneros, capítulos e shows para ver como cada um tem impacto em suas visualizações/escutas gerais e na participação do cliente com conteúdo, áudio, anúncios e combinações.

## Medição de pulsação {#heartbeat}

O Adobe Analytics usa &quot;pulsações&quot; para coletar métricas de vídeo. Durante a reprodução do vídeo, as pulsações são enviadas ao servidor de rastreamento de pulsação para medir o tempo de reprodução. As chamadas de pulsação são enviadas a cada dez segundos. As pulsações resultam em métricas de engajamento granulares com o vídeo e relatórios de fallout de vídeo mais precisos. O Adobe Analytics for Streaming Media mede as pulsações usando o Adobe Launch com a extensão do Media Analytics, o SDK de mídia e a API de coleta de mídia. Os componentes `AppMeasurement` e `VisitorID` são usados para receber dados de vídeo.

O uso do Adobe Analytics Heartbeats para Streaming Media oferece os seguintes benefícios:

| Recurso | Descrição |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Eventos de mídia | Eventos detalhados e personalizados são enviados a cada 10 segundos para o conteúdo principal e a cada 1 segundo para anúncios |
| Métricas e dimensões | Métricas, dimensões e benchmarks padronizados e claros para todos os fornecedores<br>Com uma solução padronizada em todas as plataformas, você pode usar variáveis consistentes e padronizadas em todas as mídias e plataformas para permitir uma comparação mais eficiente entre campanhas, dispositivos e fornecedores. |
| Integrações | A Experience Cloud ID está vinculada à Adobe Experience Cloud para facilitar a análise cruzada<br>Com a integração automática da Adobe Experience Cloud, você pode segmentar os públicos de mídia, direcioná-los e fazer recomendações de mídia de acordo com as preferências do usuário. |
| Preços | Rastreamento transparente por fluxo de mídia (único) |
| Implementação e suporte | Configuração simplificada com atualizações e melhorias contínuas<br>Com um processo de implementação simplificado, você pode mapear variáveis rapidamente por meio da API do player e validar implementações usando a ferramenta de depuração da Adobe para garantir que todas as variáveis necessárias sejam rastreadas com precisão. |
| Compartilhamento de parceiros | Federated Analytics e Métricas certificadas<br>Com dados compartilhados por meio do Federated Analytics, você pode capitalizar nossos recursos de compartilhamento de mídia, o primeiro do setor, para avaliar dados de forma holística em todos os seus parceiros de distribuição de mídia, operadores, programadores e distribuidores. |
| Rastreamento avançado | O rastreamento de conteúdo baixado, o rastreamento de recuperação de erros e os visualizadores simultâneos<br>Você pode rastrear o conteúdo de mídia de streaming baixado e reproduzido em um dispositivo, independentemente de sua conectividade. |



## Segurança {#security}

Na Adobe, levamos a segurança dos seus ativos digitais muito a sério. Da rigorosa integração de segurança em nosso processo interno de desenvolvimento de software e ferramentas a nossas equipes multifuncionais de resposta a incidentes, nos esforçamos para ser proativos e ágeis. Além disso, nosso trabalho colaborativo com parceiros, pesquisadores e outras organizações do setor nos ajuda a entender as mais recentes ameaças e práticas recomendadas de segurança, além de aumentar continuamente a segurança nos produtos e serviços que oferecemos.


### Segurança da camada de transporte {#transport-layer-security}

**Aviso TLS —** a Adobe tem padrões de conformidade de segurança que exigem o fim da vida útil dos protocolos de segurança mais antigos. Para continuar a atender aos padrões de protocolo de segurança em evolução, a Adobe está migrando para o uso do TLS 1.2, a fim de ter a versão mais atualizada e segura em uso. A partir de 20 de fevereiro de 2019, a Adobe será compatível somente com o TLS 1.1 ou versão posterior. Com essa alteração, a Adobe não coletará mais dados de usuários finais com dispositivos mais antigos ou navegadores da Web que tenham o TLS 1.0 implantado. A migração para o TLS 1.2 oferece segurança aprimorada. É importante que você verifique as especificidades e planeje as alterações para uma transição suave.

>[!NOTE]
>
>O TLS é o protocolo de segurança mais implantado atualmente em termos de amplitude, usado em navegadores Web e outros aplicativos que exigem segurança durante a troca de dados em uma rede.
