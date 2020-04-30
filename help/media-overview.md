---
title: Avaliação de áudio e vídeo no Adobe Analytics
description: 'O Adobe Analytics for Media (também conhecido como Media Analytics) fornece aos clientes medições de mídia robustas para conteúdo, áudio e anúncios. '
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
translation-type: ht
source-git-commit: 689b7d4ce632d3ddba6704bb8040eec52bfc326f

---


# Avaliação de áudio e vídeo no Adobe Analytics {#measuring-audio-and-video-in-adobe-analytics}

![Banner](./assets/media_analytics_banner.png)

>[!IMPORTANT]
>
>A documentação de vídeo fornecida aqui é específica para clientes que utilizam a versão 1.5 ou posterior do *SDK do Media* da Adobe, ou a nova *API da coleção do Media* da Adobe, para a avaliação de heartbeats. Não inclui instruções sobre a implementação de marcos herdados do vídeo. Incentivamos todos os clientes a adotarem uma ou as duas soluções de rastreamento de mídia mais recentes, a fim de aproveitarem as melhorias e a medição expandida. Você pode visualização os [benefícios da transição para as soluções mais recentes](media-overview.md#heartbeat-versus-milestone-benefits) abaixo. Embora o suporte ao método de marcos de rastreamento de vídeos continue, não haverá atualizações, correções ou melhorias de recursos programadas. Caso tenha alguma dúvida, entre em contato com seu Gerente de conta da Adobe.

## Visão geral {#overview}

O Adobe Analytics for Media (também conhecido como Media Analytics) é um complemento da oferta básica do Analytics que fornece aos clientes uma avaliação de mídia robusta para conteúdo, áudio e anúncios. O Media Analytics oferece muitos benefícios aos clientes para permitir monitoramento em tempo real, análise detalhada, insights acionáveis e oportunidades de monetização.

O rastreamento de mídia é ativado por meio de:

* **SDK de mídia -** Integra-se aos players de mídia mais usados.
* **API Media Collection -** (RESTful API) Integra-se a reprodutores para os quais não há suporte para SDK (ou com reprodutores para os quais não é desejada integração com o SDK).

O Adobe Analytics for Media permite aos clientes rastrear a jornada completa do cliente em todo o site, que inclui o consumo de mídia, e essas medidas são facilmente integradas ao relatório do Analytics e aos outros produtos da Experience Cloud. A medição de mídia permite cortar e dividir os dados em várias dimensões e segmentos, capturando todos os metadados necessários para uma análise detalhada e atribuir critérios de sucesso à mídia totalmente consumida, tempo médio gasto e anúncios concluídos.

As soluções de mídia não só medem as métricas vitais do delivery relacionadas a QoS, como quadros ignorados, tempo gasto no buffering e taxa média de bits. Eles também podem ser combinados aos dados do seu site ou aplicativo para visualizar o fluxo do cliente e seus interesses, para melhor fazer recomendações e personalizar suas experiências por meio da Adobe Experience Cloud.

## Benefícios {#benefits}

Alguns dos muitos benefícios oferecidos pelas soluções de medição de mídia da Adobe incluem:

* **Análise em tempo real -** Tome decisões acionáveis em tempo real utilizando as principais métricas de desempenho (por exemplo, duração) em vários canais. Os eventos de conteúdo principal são medidos em intervalos de **10 segundos** para capturar todas as atividades que ocorrem. Os eventos de rastreamento de anúncios ocorrem em intervalos de **1 segundo**.
* **Impulsionar o engajamento -** Envolva totalmente os usuários com menos eventos de buffer e entenda onde e quando os anúncios devem ser exibidos no conteúdo para fornecer uma experiência perfeita e menos intrusiva que traz os usuários de volta e oferece visitas repetidas.
* **Imagem holística -** Combine vários pontos de dados em todos os distribuidores de conteúdo para obter uma visão completa de todas as atividades de mídia e medir o engajamento e as visualizações/escutas em todos os canais possíveis por meio do recurso [Federated Analytics](/help/federated-analytics.md).
* **Maior granularidade -** Avalie o comportamento de visualização no nível mais granular, incluindo o momento do dia do visitante individual, os visualizadores/ouvintes simultâneos por minuto e a duração média do conteúdo consumido.
* **Medição precisa -** Meça os vários dispositivos usados para o consumo de mídia, incluindo OTT, smartphone, tablet, desktop e muito mais, para monitorar os padrões e os hábitos de envolvimento do usuário.
* **Segmentação -** Aplique classificações a seus players, dispositivos, gêneros, capítulos e shows para ver como cada um tem impacto em suas visualizações/escutas gerais e na participação do cliente com conteúdo, áudio, anúncios e combinações.

## Benefícios do Heartbeat versus Marcos {#heartbeat-versus-milestone-benefits}

O Adobe Analytics for Media pode ser medido por dois meios: o método de Marcos herdados (somente vídeo) e o método de Heartbeats atual (áudio e vídeo, presentes no SDK do Media e na API Media Collection). O método Heartbeats é o melhor método de medição e incentivamos todos os clientes a migrar para essa versão caso ainda não tenham feito isso para aproveitar os benefícios descritos abaixo.

O método herdado Milestone é baseado em chamadas individuais de servidor para o servidor do Analytics, para início de vídeo, quartis, duração e conclusões. O método Heartbeats fornece uma solução de rastreamento de mídia mais eficiente, que avalia o conteúdo principal em intervalos de 10 segundos, para fornecer métricas avançadas e padronizadas. Além disso, a Adobe tem aprendizagens derivadas de nosso método de marcos para fornecer um processo de implementação contínuo e simplificado por meio do SDK do Media ou da API Media Collection, utilizado pelo Heartbeats.

Alguns dos muitos benefícios do método Heartbeats incluem:

* **Processo de implementação simplificado -** Mapeie variáveis com mais facilidade por meio da API do player e valide implementações por meio da ferramenta de depuração da Adobe para garantir que todas as variáveis necessárias sejam rastreadas com precisão.
* **Integração automática da Adobe Experience Cloud** - Aproveite a integração automática com a Adobe Experience Cloud por meio da Experience Cloud ID, segmente seus públicos de mídia, direcione-os e faça recomendações de mídia com base nas preferências do usuário.
* **Dados compartilhados por meio do Federated Analytics -** Aproveite nossos recursos de compartilhamento de mídia, pioneiros no setor, para avaliar dados de forma holística em todos os seus parceiros de distribuição de mídia: operadores, programadores e distribuidores.
* **Solução padronizada em todas as plataformas -** Habilite variáveis consistentes e padronizadas em todas as mídias e plataformas para permitir uma comparação mais eficiente entre campanhas, dispositivos e fornecedores.
* **Rastreamento de conteúdo baixado -** Rastreie conteúdo de mídia (vídeo e áudio) que é baixado e reproduzido em um dispositivo, independentemente da conectividade.

### Gráfico de comparação

|  | Video Analytics - Marcos | Media Analytics - Heartbeats |
|---|---|---|
| **Eventos de mídia** | Eventos padrão de alto nível | Eventos detalhados e personalizados a cada 10 anos para conteúdo principal, a cada 1 s para anúncios |
| **Métricas e dimensões** | Variações entre fornecedores, métricas e dimensões não padronizadas | Métricas, dimensões e benchmarks limpos e padronizados entre fornecedores |
| **Integrações c/ produtos da Adobe** | Sessões individuais c/ alguns Mapeamentos e Integrações | Experience Cloud ID vinculada ao Adobe Experience Cloud completo para análise cruzada mais fácil |
| **Preços** | Rastreado e cobrado em relação a cada chamada de servidor | Rastreamento transparente por fluxo de mídia (único) |
| **Implementação e suporte** | Integrações mais longas com suporte limitado em versões anteriores e sem atualizações | Configuração simplificada com atualizações e melhorias contínuas |
| **Compartilhamento de parceiros** | N/D | Federated Analytics e métricas certificadas |
| **Rastreamento avançado** | N/D | Rastreamento de recuperação de erros e visualizadores simultâneos |

## Dispositivos compatíveis {#devices-supported}

O Adobe Analytics for Media evoluiu com o setor para fornecer ferramentas de coleta de dados eficientes, a fim de garantir que cada fluxo de mídia seja coletado e informado a todos os dispositivos importantes. Nosso SDK de mídia é desenvolvido para todos os dispositivos mais utilizados, incluindo:

* Smartphones e tablets iOS e Android
* Dispositivos OTT para ROKU, AppleTV, FireTV e Android TV
* Navegador JavaScript para desktop e laptop

Os SDKs são atualizados regularmente quando novas versões de dispositivos são lançadas, e você pode usar esses SDKs para integrar a maioria dos maiores players de mídia de hoje, incluindo Brightcove e Ooyala.

Para dispositivos ou plataformas não compatíveis com o SDK (ou mesmo que sejam), é possível implementar a API Media Collection, na qual você pode fazer chamadas de API RESTful diretamente do dispositivo/plataforma para o back-end do Media Analytics.

A tabela abaixo fornece uma lista de dispositivos suportados atualmente por meio da implementação do SDK do Media e da API Media Collection. Para baixar a versão mais recente do SDK, consulte [Baixar SDKs.](sdk-implement/download-sdks.md) Se houver um dispositivo que não esteja listado, no qual deseja realizar a avaliação, entre em contato com o Atendimento ao cliente ou o consultor da solução para obter o status desse dispositivo.

|      | SDK do Media | API da coleção de mídia |
|---|:---:|:---:|
| **Navegador de JavaScript** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Dispositivos iOS** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Dispositivos Android** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Unified Windows Platforms (UWP)** |  | ![](assets/icon-blue-check.png) |
| **BlackBerry** |  | ![](assets/icon-blue-check.png) |
| **Apple TV (nova/antiga)** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **ROKU (JS)** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **ROKU (aplicativo nativo)** |  | ![](assets/icon-blue-check.png) |
| **OSX** |  | ![](assets/icon-blue-check.png) |
| **FireTV** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Android TV** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Chromecast** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Xbox One/360** |  | ![](assets/icon-blue-check.png) |
| **Sony PS3/PS4** |  | ![](assets/icon-blue-check.png) |
| **(Outros/novos dispositivos conectados)** |  | ![](assets/icon-blue-check.png) |

Para o SDK do Media, consulte também [Suporte à versão mínima da plataforma](./sdk-implement/setup/setup-overview.md#minimum-platform-version)

## Segurança da camada de transporte {#transport-layer-security}

**Aviso TLS —** a Adobe tem padrões de conformidade de segurança que exigem o fim da vida útil dos protocolos de segurança mais antigos. Para continuar a atender aos padrões de protocolo de segurança em evolução, a Adobe está migrando para o uso do TLS 1.2, a fim de ter a versão mais atualizada e segura em uso. A partir de 20 de fevereiro de 2019, a Adobe será compatível somente com o TLS 1.1 ou versão posterior. Com essa alteração, a Adobe não coletará mais dados de usuários finais com dispositivos mais antigos ou navegadores da Web que tenham o TLS 1.0 implantado. A migração para o TLS 1.2 oferece segurança aprimorada. É importante que você verifique as especificidades e planeje as alterações para uma transição suave.

>[!NOTE]
>
>O TLS é o protocolo de segurança mais implantado atualmente em termos de amplitude, usado em navegadores Web e outros aplicativos que exigem segurança durante a troca de dados em uma rede.

