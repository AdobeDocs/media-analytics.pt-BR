---
title: Avaliação de áudio e vídeo no Adobe Analytics
description: O Adobe Analytics for Media (também conhecido como Media Analytics) fornece aos clientes medições de mídia robustas para conteúdo, áudio e anúncios.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
translation-type: tm+mt
source-git-commit: bddcbcd844145788518c60399bee9e4744e42d3a

---


# Avaliação de áudio e vídeo no Adobe Analytics {#measuring-audio-and-video-in-adobe-analytics}

![Banner](./assets/media_analytics_banner.png)

## Sobre o Adobe Analytics para áudio e vídeo

O Adobe Analytics para áudio e vídeo é um complemento do Adobe Analytics que fornece ferramentas poderosas de medição para áudio, vídeo e anúncios. O Adobe Analytics faz parte da Adobe Experience Platform.

O Adobe Analytics para áudio e vídeo permite rastrear a jornada completa do cliente em seu site. As métricas se integram facilmente aos Relatórios do Adobe Analytics e a outros produtos da Adobe Experience Cloud. A medição de mídia permite categorizar seus dados em várias dimensões e segmentos, capturando todos os metadados necessários para fazer uma análise completa e detalhada. Em seguida, você pode analisar dados e atribuir critérios de sucesso a mídias totalmente consumidas, tempo médio gasto e anúncios concluídos.

É possível medir métricas vitais de delivery relacionadas a QoS, como quadros ignorados, tempo gasto no buffer e taxa média de bits. E as métricas podem ser combinadas com os dados do seu site ou aplicativo para visualizar o caminho e os interesses do cliente — para fornecer recomendações aprimoradas e personalizar as experiências do cliente usando a Adobe Experience Cloud.

## Recursos {#features}

Os benefícios do Adobe Analytics para áudio e vídeo incluem monitoramento em tempo real, análise detalhada, insights acionáveis e oportunidades de monetização.
* **análise** em tempo real — tome decisões acionáveis em tempo real utilizando métricas chave de desempenho, como duração, ex2 e ex3, em vários canais. Os eventos de conteúdo principal são medidos em intervalos de 10 segundos para capturar todas as atividades que ocorrem. Os eventos de rastreamento de anúncios ocorrem em intervalos de 1 segundo.
* **Impulsionar o envolvimento**— envolva totalmente os usuários com menos eventos de buffering e entendendo onde e quando os anúncios devem ser reproduzidos dentro do conteúdo para proporcionar uma experiência mais suave e menos intrusiva que ofereça visitas repetidas.
* **Imagem** holística—Combine vários pontos de dados em todos os distribuidores de conteúdo para obter uma visualização completa de toda a sua atividade de mídia. Meça o envolvimento e as visualizações/escutas em todos os canais possíveis por meio do recurso Federated Analytics.
* **Maior granularidade**— Avalie o comportamento de visualização no nível mais granular, incluindo o horário individual do visitante do dia, os visualizadores/ouvintes simultâneos por minuto e a duração média do conteúdo consumido.
* **Medição** precisa — Meça os vários dispositivos usados para consumo de mídia, incluindo OTT, smartphone, tablet, desktop e muito mais, para monitorar os padrões e hábitos de envolvimento do usuário.
* **Segmentação**—Aplique classificações aos seus players, dispositivos, gêneros, capítulos e shows para ver como cada um tem impacto nas visualizações/escutas gerais e na participação do cliente com conteúdo, áudio, anúncios e combinados.

## Medição de pulsação {#heartbeat}

O Adobe Analytics usa &quot;pulsações&quot; para coletar métricas de vídeo. Durante a reprodução do vídeo, as pulsações são enviadas ao servidor de rastreamento de pulsação para medir o tempo de reprodução. As chamadas de pulsação são enviadas a cada dez segundos. As pulsações resultam em métricas granulares de envolvimento com o vídeo e relatórios de fallout de vídeo mais precisos. O Adobe Analytics para áudio e vídeo mede as pulsações usando o Adobe Launch com a extensão do Media Analytics, o SDK de mídia e a API de coleção de mídia. Os componentes `AppMeasurement` e `VisitorID` são usados para receber dados de vídeo.

Usar pulsações O Adobe Analytics para áudio e vídeo oferece os seguintes benefícios:

| Recurso | Descrição |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Eventos de mídia | Eventos detalhados e personalizados são enviados a cada 10 segundos para o conteúdo principal e a cada 1 segundo para anúncios |
| Métricas e dimensões | Métricas, dimensões e benchmarks padronizados e claros em todos os<br>fornecedoresCom uma solução padronizada em todas as plataformas, você pode usar variáveis consistentes e padronizadas em todas as suas mídias e plataformas para permitir uma comparação mais eficiente entre campanhas, dispositivos e fornecedores. |
| Integrações | A Experience Cloud ID está vinculada à Adobe Experience Cloud para facilitar a<br>análise cruzadaCom a integração automática da Adobe Experience Cloud, você pode segmentar suas audiências de mídia, público alvo-as e fazer recomendações de mídia com base nas preferências do usuário. |
| Preços  | Rastreamento transparente por fluxo de mídia (único) |
| Implementação e suporte | Configuração simplificada com atualizações e<br>melhorias contínuasCom um processo de implementação simplificado, você pode mapear variáveis rapidamente por meio da API do player e validar implementações usando a ferramenta de depuração da Adobe para garantir que todas as variáveis necessárias sejam rastreadas com precisão. |
| Compartilhamento de parceiros | Federated Analytics and Certified Metrics<br>With shared data through Federated Analytics, you can capitalize on our industry-first media sharing capabilities, to evaluate data holistically across all of your media distribution partners—operators, programmers, and distributors. |
| Rastreamento avançado | Rastreamento de conteúdo baixado, Rastreamento de recuperação de erros e<br>visualizadores simultâneosVocê pode rastrear o conteúdo de áudio e vídeo que é baixado e reproduzido em um dispositivo, independentemente de sua conectividade. |



## Segurança {#security}

Na Adobe, levamos a segurança dos seus ativos digitais a sério. Desde nossa rigorosa integração da segurança em nosso processo interno de desenvolvimento de software e ferramentas até nossas equipes de resposta a incidentes multifuncionais, nos esforçamos para sermos pró-ativos e ágeis. Além disso, nosso trabalho colaborativo com parceiros, pesquisadores e outras organizações do setor nos ajuda a entender as ameaças mais recentes e as práticas recomendadas de segurança, bem como a criar continuamente segurança nos produtos e serviços que ofertas.


### Segurança da camada de transporte {#transport-layer-security}

**Aviso TLS —** a Adobe tem padrões de conformidade de segurança que exigem o fim da vida útil dos protocolos de segurança mais antigos. Para continuar a atender aos padrões de protocolo de segurança em evolução, a Adobe está migrando para o uso do TLS 1.2, a fim de ter a versão mais atualizada e segura em uso. A partir de 20 de fevereiro de 2019, a Adobe será compatível somente com o TLS 1.1 ou versão posterior. Com essa alteração, a Adobe não coletará mais dados de usuários finais com dispositivos mais antigos ou navegadores da Web que tenham o TLS 1.0 implantado. A migração para o TLS 1.2 oferece segurança aprimorada. É importante que você verifique as especificidades e planeje as alterações para uma transição suave.

>[!NOTE]
>
>O TLS é o protocolo de segurança mais implantado atualmente em termos de amplitude, usado em navegadores Web e outros aplicativos que exigem segurança durante a troca de dados em uma rede.
