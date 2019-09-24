---
seo-title: Avaliação de áudio e vídeo no Adobe Analytics
title: Avaliação de áudio e vídeo no Adobe Analytics
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
translation-type: tm+mt
source-git-commit: 9b6e61e8d97ca44772f5dc2e31472a4f6c54e29c

---


# Avaliação de áudio e vídeo no Adobe Analytics{#measuring-audio-and-video-in-adobe-analytics}

![Banner](./assets/media_analytics_banner.png)

>[!IMPORTANT]
>
>The documentation provided here is specific to clients utilizing version 1.5 or higher of Adobe's *Media SDK* for heartbeat measurement, or Adobe's newer *Media Collection API* for heartbeat measurement. Ele não inclui instruções sobre a implementação de vídeo do Marco herdado. Incentivamos todos os clientes a adotarem uma ou as duas soluções de rastreamento de mídia mais recentes, a fim de aproveitarem as melhorias e a medição expandida. Você pode visualizar os [benefícios da transição para as soluções mais recentes](media-overview.md#section_cnj_5st_p1b) abaixo. Embora continuemos a oferecer suporte ao método Milestone de rastreamento de vídeos, não haverá atualizações, correções ou aprimoramentos de recursos planejados. Caso tenha alguma dúvida, entre em contato com seu Gerente de conta da Adobe.

## Visão geral {#section_8BFE4F8DA64B4A5F826A4940B11AA466}

O Adobe Analytics for Media (também conhecido como Media Analytics) é um complemento da oferta básica do Analytics que fornece aos clientes uma avaliação de mídia avançada para conteúdo, áudio e anúncios. O Media Analytics fornece muitos benefícios aos clientes para permitir o rastreamento em tempo real, a análise detalhada, os insights acionáveis e as oportunidades de monetização.

O rastreamento de mídia é ativado por meio de um dos seguintes procedimentos:

* **SDK do Media -** Integra-se com os reprodutores de mídia mais usados.
* **API da coleção de mídia-** (RESTful API) Integra-se a reprodutores para os quais não há suporte para SDK (ou com reprodutores para os quais não é desejada integração com o SDK).

   A API da coleção de mídia também fornece um recurso adicional ainda não disponível no SDK:

   * **Rastreamento de conteúdo baixado -** Fornece suporte para o rastreamento de conteúdo de mídia (vídeo e áudio) que é baixado e reproduzido de um dispositivo, independentemente da conectividade. Esse recurso é criado sobre a API da coleção de mídia e segue a mesma especificação de rastreamento de reprodutor de mídia. (Ainda não há suporte para SDK no momento.)

O Adobe Analytics for Media permite aos clientes rastrear a jornada completa do cliente em todo o site, que inclui o consumo de mídia, e essas medidas são facilmente integradas ao relatório do Analytics e aos outros produtos da Experience Cloud. A medição de mídia permite dividir e analisar os dados em várias dimensões e segmentos, capturando todos os metadados necessários para fazer uma análise detalhada completa e atribuir critérios de sucesso a mídias totalmente consumidas, ao tempo médio gasto e aos anúncios concluídos.

As soluções de mídia não medem apenas as métricas essenciais de entrega relacionadas ao QoS, como os quadros ignorados, o tempo gasto com buffering e a taxa média de bits. Também podem ser combinadas com os dados do site ou do aplicativo para visualizar o fluxo do cliente e seus interesses, a fim de melhorar as recomendações e personalizar suas experiências na Adobe Experience Cloud.

## Benefícios {#section_7712BA90EAE64C118218D1C581EF68B7}

Alguns dos muitos benefícios que as soluções de avaliação de mídia da Adobe oferecem incluem:

* **Análise pontual -** Tome decisões práticas e em tempo real utilizando as principais métricas de desempenho (por exemplo, duração) em vários canais. Os eventos de conteúdo principal são medidos em intervalos de **10 segundos** para capturar todas as atividades que ocorrem. Os eventos de rastreamento de anúncios ocorrem em intervalos de **1 segundo**.
* **Impulsionar o envolvimento** - Envolva totalmente os usuários com menos eventos de buffering, compreendendo onde e quando os anúncios devem ser exibidos no conteúdo para fornecer uma experiência contínua e menos intrusiva, que traga os usuários de volta e gere visitas repetidas.
* **Imagem holística -** Combine vários pontos de dados em todos os distribuidores de conteúdo para obter uma visão completa de toda a sua atividade de mídia e medir o envolvimento e as visualizações/escutas em todos os canais possíveis por meio do recurso [Federated Analytics](data-sharing/federated-analytics.md) .
* **Maior granularidade** - Avalie o comportamento de exibição no nível mais granular, incluindo a hora do dia da visita individual, os visualizadores/ouvintes simultâneos por minuto e a duração média que o conteúdo foi consumido.
* **Medição precisa** - Meça os vários dispositivos usados para o consumo de mídia, incluindo OTT, smartphone, tablet, desktop e muito mais, para monitorar os padrões e os hábitos de envolvimento do usuário.
* **Segmentação -** Aplique classificações aos reprodutores, dispositivos, gêneros, capítulos e programas para ver como cada um tem um impacto nas exibições/áudios gerais e no envolvimento do cliente com conteúdo, áudio, anúncios e combinados.

## Benefícios do Heartbeat versus Marcos {#section_cnj_5st_p1b}

O Adobe Analytics for Media pode ser avaliado por dois meios: o método herdado Milestone (somente vídeo) e o método Heartbeats atual (áudio e vídeo, em destaque no SDK de mídia e na API Media Collection). O método Heartbeats é o preferencial para a avaliação e incentivamos todos os clientes a mudarem para essa versão caso ainda não a tenham, a fim de aproveitar os benefícios descritos abaixo.

O método herdado Marcos é baseado nas chamadas de servidor individuais para o servidor Analytics, para inícios, quartis, duração e conclusão de vídeo. O método Heartbeats fornece uma solução de rastreamento de mídia mais eficiente, que avalia o conteúdo principal em intervalos de 10 segundos, para fornecer métricas avançadas e padronizadas. Além disso, a Adobe tem aprendizagens derivadas de nosso método de Marcos para fornecer um processo de implementação contínuo e simplificado por meio do SDK do Media ou da API da coleção de mídia, utilizado pelo Heartbeats.

Alguns dos muitos benefícios do método Heartbeats incluem:

* **Processo de implementação simplificado -** Mapeie variáveis de forma mais fácil por meio da API do reprodutor e valide as implementações por meio da ferramenta Adobe Debug para garantir que todas as variáveis necessárias sejam rastreadas com precisão.
* **Integração automática da Adobe Experience Cloud** - Aproveite a integração automática com a Adobe Experience Cloud por meio da Experience Cloud ID, segmente os públicos-alvo de mídia, direcione-os e faça recomendações de vídeos com base nas preferências do usuário.
* **Dados compartilhados por meio do Federated Analytics -** Aproveite os nossos recursos de compartilhamento, inéditos do setor, para avaliar os dados de forma holística em todos os parceiros de distribuição de mídia: operadores, programadores e distribuidores.
* **Parceiros de classificações certificados** - A Adobe faz parceria com a Nielsen, parceira de classificações de público-alvo, para fornecer medições de terceiros neutras, a fim de permitir classificações confiáveis e certificadas.
* **Solução padronizada em todas as plataformas** - Habilite variáveis consistentes e padronizadas em todas as mídias e plataformas para permitir uma comparação mais eficiente entre campanhas, dispositivos e fornecedores.

### Gráfico de comparação

|  | Video Analytics - Marcos | Media Analytics - Heartbeats |
|---|---|---|
| **Eventos de mídia** | Eventos padrão de alto nível | Eventos detalhados e personalizados a cada 10 segundos para o conteúdo principal, a cada 1 segundo para anúncios |
| **Métricas e dimensões** | Variações entre fornecedores, métricas não padronizadas e dimensões | Métricas, dimensões e referências claras e padronizadas em todos os fornecedores |
| **Integrações com os produtos da Adobe** | Sessões individuais com alguns mapeamentos e integrações | Experience Cloud ID vinculada à Adobe Experience Cloud completa para facilitar a análise cruzada |
| **Preços** | Rastreado e faturado a cada chamada de servidor | Rastreamento transparente por fluxo de mídia (único) |
| **Implementação e suporte** | Integrações mais longas com suporte limitado em versões antigas e sem upgrades | Configuração simplificada com atualizações e melhorias contínuas |
| **Compartilhamento do parceiro** | N/A | Federated Analytics e métricas certificadas |
| **Rastreamento avançado** | N/A | Rastreamento da recuperação de erros e visualizadores simultâneos |

## Dispositivos compatíveis {#section_lkm_l5t_p1b}

O Adobe Analytics for Media evoluiu com o setor para fornecer ferramentas de coleta de dados eficientes, a fim de garantir que cada fluxo de mídia seja coletado e informado a todos os dispositivos importantes. Nosso SDK do Media é desenvolvido para todos os dispositivos mais utilizados, incluindo:

* Smartphones e tablets iOS e Android
* Dispositivos OTT para ROKU, Apple TV, FireTV e Android TV
* Navegador de JavaScript para Desktop e Laptop

Os SDK são atualizados rotineiramente quando novas versões de dispositivos são lançadas e você pode usá-los para se integrar com a maior parte dos maiores reprodutores de mídia, incluindo Brightcove e Ooyala.

Para dispositivos ou plataformas não compatíveis com o SDK (ou mesmo que sejam), é possível implementar a API da coleção de mídia, na qual você pode fazer chamadas de API RESTful diretamente do dispositivo/plataforma para o back-end do Media Analytics.

A tabela abaixo fornece uma lista de dispositivos suportados atualmente por meio da implementação do SDK do Media e da API da coleção de mídia. Para baixar a versão mais recente do SDK, consulte [Baixar SDKs.](sdk-implement/download-sdks.md) Se houver um dispositivo que não esteja listado, no qual deseja realizar a avaliação, entre em contato com o Atendimento ao cliente ou o consultor da solução para obter o status desse dispositivo.

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

Para o SDK de mídia, consulte também Suporte à versão [mínima da plataforma](./sdk-implement/setup/setup-overview.md#minimum-platform-version)

## Segurança da camada de transporte {#transport-layer-security}

**Aviso TLS —** a Adobe tem padrões de conformidade de segurança que exigem o fim da vida útil dos protocolos de segurança mais antigos. Para continuar a atender aos padrões de protocolo de segurança em evolução, a Adobe está migrando para o uso do TLS 1.2, a fim de ter a versão mais atualizada e segura em uso. A partir de 20 de fevereiro de 2019, a Adobe oferecerá suporte somente ao TLS 1.1 ou posterior. Com essa alteração, a Adobe não coletará mais dados de usuários finais com dispositivos mais antigos ou navegadores da Web implantando o TLS 1.0. A migração para o TLS 1.2 oferece segurança aprimorada. É importante que você verifique as especificidades e planeje as alterações para uma transição suave.

>[!NOTE]
>
>O TLS é atualmente o protocolo de segurança mais amplamente implantado usado em navegadores da Web e outros aplicativos que exigem que os dados sejam trocados com segurança por uma rede.
