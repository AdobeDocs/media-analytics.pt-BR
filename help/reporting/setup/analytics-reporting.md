---
title: Configurar relatórios para implementações somente do Analytics
description: Ative os módulos do conjunto de relatórios de mídia no Adobe Analytics para que os dados de mídia de transmissão possam ser coletados e relatados.
feature: Streaming Media
role: User, Admin
source-git-commit: 7b5232f25f3aa26e8566783557163f316af3fe57
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 11%

---

# Configurar relatórios para implementações somente do Analytics

Para que uma implementação somente no Analytics possa coletar dados de mídia de transmissão, cada conjunto de relatórios que recebe esses dados deve ser configurado para habilitar os módulos de mídia apropriados. Esta página descreve como ativar esses módulos e onde encontrar os relatórios resultantes.

* **Pré-requisitos**: uma implementação do Adobe Analytics. Consulte a [visão geral da implementação somente do Analytics](/help/implementation/analytics-only/overview.md) e o método de implementação escolhido.

## Ativar relatórios de mídia em um conjunto de relatórios

Cada conjunto de relatórios que coleta métricas de mídia deve ser configurado antes do envio dos dados de mídia.

1. No [Adobe Analytics](https://experience.adobe.com/analytics), navegue até **[!UICONTROL Admin]** → **[!UICONTROL Conjuntos de relatórios]**.
1. Selecione os conjuntos de relatórios que coletam dados de mídia. Selecione **[!UICONTROL Editar configurações]** → **[!UICONTROL Gerenciamento de mídia]** → **[!UICONTROL Relatórios de mídia]**.

   ![Captura de tela do menu do gerenciador de conjunto de relatórios](assets/media-reporting.png)

1. Na página **[!UICONTROL Relatórios de Mídia]**, habilite os módulos de mídia de streaming desejados (veja abaixo).

1. Selecione **[!UICONTROL Salvar].**

   Se este conjunto de relatórios já estiver configurado para coletar dados de mídia, uma página de configuração adicional será exibida depois que você selecionar **[!UICONTROL Salvar]**. Se você visualizar a página **[!UICONTROL Avaliação da mídia principal]**, continue para a próxima etapa.

## Módulos de streaming de mídia disponíveis

A avaliação de mídia inclui os seguintes módulos:

* **[!UICONTROL Mídia principal]**: obrigatório para todo o rastreamento de streaming de mídia. Ele reserva variáveis de solução para a reprodução de conteúdo e dados de sessão.

  +++Selecione para exibir dimensões e métricas

   * **Dimensões:**
      * [[!UICONTROL Conteúdo]](/help/reporting/dimensions/content.md)
      * [[!UICONTROL Canal de conteúdo]](/help/reporting/dimensions/content-channel.md)
      * [[!UICONTROL Comprimento do conteúdo (variável)]](/help/reporting/dimensions/content-length.md)
      * [[!UICONTROL Nome do conteúdo (variável)]](/help/reporting/dimensions/content-name.md)
      * [[!UICONTROL Nome do player de conteúdo]](/help/reporting/dimensions/content-player-name.md)
      * [[!UICONTROL Segmento de conteúdo]](/help/reporting/dimensions/content-segment.md)
      * [[!UICONTROL Tipo de conteúdo]](/help/reporting/dimensions/content-type.md)
      * [[!UICONTROL Caminho da mídia]](/help/reporting/dimensions/media-path.md)
      * [[!UICONTROL ID da sessão de mídia]](/help/reporting/dimensions/media-session-id.md)
      * [[!UICONTROL Tipo de fluxo]](/help/reporting/dimensions/stream-type.md)
   * **Métricas:**
      * [[!UICONTROL Média de público-alvo por minuto]](/help/reporting/metrics/average-minute-audience.md)
      * [[!UICONTROL Conteúdo concluído]](/help/reporting/metrics/content-completes.md)
      * [[!UICONTROL Resumo do conteúdo]](/help/reporting/metrics/content-resumes.md)
      * [[!UICONTROL Exibições do segmento de conteúdo]](/help/reporting/metrics/content-segment-views.md)
      * [[!UICONTROL Início do conteúdo]](/help/reporting/metrics/content-starts.md)
      * [[!UICONTROL Tempo gasto com o conteúdo]](/help/reporting/metrics/content-time-spent.md)
      * [[!UICONTROL Início da mídia]](/help/reporting/metrics/media-starts.md)
      * [[!UICONTROL Pausar eventos]](/help/reporting/metrics/pause-events.md)
      * [[!UICONTROL Fluxos afetados pausados]](/help/reporting/metrics/paused-impacted-streams.md)
      * [[!UICONTROL Marcadores de progresso]](/help/reporting/metrics/progress-markers.md)
      * [[!UICONTROL Duração total da pausa]](/help/reporting/metrics/total-pause-duration.md)
      * [[!UICONTROL Tempo de execução exclusivo]](/help/reporting/metrics/unique-time-played.md)

  +++

* **[!UICONTROL Anúncios de mídia]**: permite o rastreamento de anúncios dentro do conteúdo de mídia.

  +++Selecione para exibir dimensões, classificações e métricas

   * **Dimensões:**
      * [[!UICONTROL Anúncio]](/help/reporting/dimensions/ad.md)
      * [[!UICONTROL Anúncio na posição pod]](/help/reporting/dimensions/ad-in-pod-position.md)
      * [[!UICONTROL Comprimento do anúncio (variável)]](/help/reporting/dimensions/ad-length.md)
      * [[!UICONTROL Nome do anúncio (variável)]](/help/reporting/dimensions/ad-name.md)
      * [[!UICONTROL Nome do player do anúncio]](/help/reporting/dimensions/ad-player-name.md)
      * [[!UICONTROL Pod de anúncio]](/help/reporting/dimensions/ad-pod.md)
      * [[!UICONTROL Anunciante]](/help/reporting/dimensions/advertiser.md)
      * [[!UICONTROL ID da campanha]](/help/reporting/dimensions/campaign-id.md)
   * **Dimensões de classificação:**
      * [[!UICONTROL ID do ativo]](/help/reporting/dimensions/asset-id.md)
      * [[!UICONTROL Classificação de conteúdo]](/help/reporting/dimensions/content-rating.md)
      * [[!UICONTROL Creative ID]](/help/reporting/dimensions/creative-id.md)
      * [[!UICONTROL Primeira transmissão]](/help/reporting/dimensions/first-air-date.md)
      * [[!UICONTROL Primeira data digital]](/help/reporting/dimensions/first-digital-date.md)
      * [[!UICONTROL Nome do pod]](/help/reporting/dimensions/pod-name.md)
      * [[!UICONTROL Posição do pod]](/help/reporting/dimensions/pod-position.md)
   * **Métricas:**
      * [[!UICONTROL Anúncio concluído]](/help/reporting/metrics/ad-completes.md)
      * [[!UICONTROL Início do anúncio]](/help/reporting/metrics/ad-starts.md)
      * [[!UICONTROL Tempo gasto com anúncio]](/help/reporting/metrics/ad-time-spent.md)
      * [[!UICONTROL Tempo gasto com a mídia]](/help/reporting/metrics/media-time-spent.md)

  +++

* **[!UICONTROL Capítulos de mídia]**: permite o rastreamento de capítulos dentro do conteúdo de mídia.

  +++Selecione para exibir dimensões, classificações e métricas

   * **Dimension:**
      * [[!UICONTROL Capítulo]](/help/reporting/dimensions/chapter.md)
   * **Dimensões de classificação:**
      * [[!UICONTROL Comprimento do capítulo]](/help/reporting/dimensions/chapter-length.md)
      * [[!UICONTROL Nome do capítulo]](/help/reporting/dimensions/chapter-name.md)
      * [[!UICONTROL Deslocamento de capítulo]](/help/reporting/dimensions/chapter-offset.md)
      * [[!UICONTROL Posição do capítulo]](/help/reporting/dimensions/chapter-position.md)
      * [[!UICONTROL Originador]](/help/reporting/dimensions/originator.md)
   * **Métricas:**
      * [[!UICONTROL Capítulo concluído]](/help/reporting/metrics/chapter-completes.md)
      * [[!UICONTROL Início do capítulo]](/help/reporting/metrics/chapter-starts.md)
      * [[!UICONTROL Tempo gasto com capítulo]](/help/reporting/metrics/chapter-time-spent.md)

  +++

* **[!UICONTROL Qualidade de mídia]**: permite o rastreamento de dados de qualidade de reprodução, incluindo buffering, taxa de bits e eventos de erro.

  +++Selecione para exibir dimensões e métricas

   * **Dimensões:**
      * [[!UICONTROL Taxa média de bits]](/help/reporting/dimensions/average-bitrate.md)
      * [[!UICONTROL Alterações na taxa de bits]](/help/reporting/dimensions/bitrate-changes.md)
      * [[!UICONTROL Eventos de buffer]](/help/reporting/dimensions/buffer-events.md)
      * [[!UICONTROL Quadros soltos]](/help/reporting/dimensions/dropped-frames.md)
      * [[!UICONTROL Erros]](/help/reporting/dimensions/errors.md)
      * [[!UICONTROL IDs de erro externo]](/help/reporting/dimensions/external-error-ids.md)
      * [[!UICONTROL IDs de erro do Player SDK]](/help/reporting/dimensions/player-sdk-error-ids.md)
      * [[!UICONTROL Hora de início]](/help/reporting/dimensions/time-to-start.md)
      * [[!UICONTROL Duração total do buffer]](/help/reporting/dimensions/total-buffer-duration.md)
   * **Métricas:**
      * [[!UICONTROL Taxa média de bits]](/help/reporting/metrics/average-bitrate.md)
      * [[!UICONTROL Fluxos afetados pela alteração na taxa de bits]](/help/reporting/metrics/bitrate-change-impacted-streams.md)
      * [[!UICONTROL Alterações na taxa de bits]](/help/reporting/metrics/bitrate-changes.md)
      * [[!UICONTROL Eventos de buffer]](/help/reporting/metrics/buffer-events.md)
      * [[!UICONTROL Fluxos afetados pelo buffer]](/help/reporting/metrics/buffer-impacted-streams.md)
      * [[!UICONTROL Fluxos afetados pelo quadro descartado]](/help/reporting/metrics/dropped-frame-impacted-streams.md)
      * [[!UICONTROL Quadros soltos]](/help/reporting/metrics/dropped-frames.md)
      * [[!UICONTROL Desistências antes do início]](/help/reporting/metrics/drops-before-start.md)
      * [[!UICONTROL Eventos de erro]](/help/reporting/metrics/error-events.md)
      * [[!UICONTROL Fluxos afetados pelo erro]](/help/reporting/metrics/error-impacted-streams.md)
      * [[!UICONTROL Hora de início]](/help/reporting/metrics/time-to-start.md)
      * [[!UICONTROL Duração total do buffer]](/help/reporting/metrics/total-buffer-duration.md)

  +++

* **[!UICONTROL Metadados de vídeo]**: permite o rastreamento de atributos padrão de conteúdo de vídeo, como programa, temporada e gênero.

  +++Selecione para exibir dimensões e métricas

   * **Dimensões:**
      * [[!UICONTROL Carregamentos de anúncio]](/help/reporting/dimensions/ad-load-type.md)
      * [[!UICONTROL Parte do dia]](/help/reporting/dimensions/day-part.md)
      * [[!UICONTROL Episódio]](/help/reporting/dimensions/episode.md)
      * [[!UICONTROL Gênero]](/help/reporting/dimensions/genre.md)
      * [[!UICONTROL Tipo de feed de mídia]](/help/reporting/dimensions/media-feed-type.md)
      * [[!UICONTROL MVPD]](/help/reporting/dimensions/mvpd.md)
      * [[!UICONTROL Rede]](/help/reporting/dimensions/network.md)
      * [[!UICONTROL Temporada]](/help/reporting/dimensions/season.md)
      * [[!UICONTROL Programa]](/help/reporting/dimensions/show.md)
      * [[!UICONTROL Mostrar tipo]](/help/reporting/dimensions/show-type.md)
   * **Métrica:**
      * [[!UICONTROL Autorizado]](/help/reporting/metrics/authorized.md)

  +++

* **[!UICONTROL Metadados de áudio]**: permite o rastreamento de atributos de conteúdo de áudio padrão, como artista, álbum e estação.

  +++Selecione para exibir dimensões

   * **Dimensões:**
      * [[!UICONTROL Álbum]](/help/reporting/dimensions/album.md)
      * [[!UICONTROL Artista]](/help/reporting/dimensions/artist.md)
      * [[!UICONTROL Autor]](/help/reporting/dimensions/author.md)
      * [[!UICONTROL Rótulo]](/help/reporting/dimensions/label.md)
      * [[!UICONTROL Publicador]](/help/reporting/dimensions/publisher.md)
      * [[!UICONTROL Estação]](/help/reporting/dimensions/station.md)

  +++

* **[!UICONTROL Rastreamento do estado do player]**: permite a medição de estados padrão da interface do usuário do player, como tela cheia, legendas ocultas e picture in picture.

  +++Selecione para exibir métricas

   * **Métricas:**
      * [[!UICONTROL Contagens de legendas ocultas]](/help/reporting/metrics/closed-captioning-count.md)
      * [[!UICONTROL Duração total das legendas ocultas]](/help/reporting/metrics/closed-captioning-total-duration.md)
      * [[!UICONTROL Contagens de tela inteira]](/help/reporting/metrics/full-screen-count.md)
      * [[!UICONTROL Duração total da tela inteira]](/help/reporting/metrics/full-screen-total-duration.md)
      * [[!UICONTROL Contagens da função Em foco]](/help/reporting/metrics/in-focus-count.md)
      * [[!UICONTROL Duração total do foco]](/help/reporting/metrics/in-focus-total-duration.md)
      * [[!UICONTROL Contagens da função Mudo]](/help/reporting/metrics/mute-count.md)
      * [[!UICONTROL Duração total da função Mudo]](/help/reporting/metrics/mute-total-duration.md)
      * [[!UICONTROL Contagens de Picture in picture]](/help/reporting/metrics/picture-in-picture-count.md)
      * [[!UICONTROL Duração total do Picture in picture]](/help/reporting/metrics/picture-in-picture-total-duration.md)
      * [[!UICONTROL Fluxos afetados pelas legendas ocultas]](/help/reporting/metrics/closed-captioning-streams-impacted.md)
      * [[!UICONTROL Fluxos afetados pela tela cheia]](/help/reporting/metrics/full-screen-streams-impacted.md)
      * [[!UICONTROL Fluxos afetados pela função em foco]](/help/reporting/metrics/in-focus-streams-impacted.md)
      * [[!UICONTROL Fluxos afetados pela função mudo]](/help/reporting/metrics/mute-streams-impacted.md)
      * [[!UICONTROL Fluxos afetados pela imagem na imagem]](/help/reporting/metrics/picture-in-picture-streams-impacted.md)

  +++

## Painéis de mídia disponíveis no Adobe Analytics

O Analysis Workspace inclui três painéis de mídia dedicados para clientes com o complemento Adobe Analytics para mídia de streaming. Esses painéis fornecem visualizações pré-construídas para as necessidades mais comuns de relatórios de mídia de transmissão.

* **[Público-alvo médio por minuto da mídia](https://experienceleague.adobe.com/pt-br/docs/analytics/analyze/analysis-workspace/panels/average-minute-audience-panel)**: compara o consumo médio de conteúdo entre programas de qualquer duração ou gênero. Oferece suporte aos modos de conteúdo específico (com base na duração) e período personalizado e permite a atualização das classificações de duração após o fato.
* **[Visualizadores simultâneos de mídia](https://experienceleague.adobe.com/pt-br/docs/analytics/analyze/analysis-workspace/panels/media-concurrent-viewers)**: analisa visualizadores simultâneos ao longo do tempo para identificar pico de simultaneidade e pontos de devolução. Suporta detalhamento de séries e granularidade configurável por segmentos, dimensões ou intervalos de datas.
* **[Tempo gasto com a reprodução da mídia](https://experienceleague.adobe.com/pt-br/docs/analytics/analyze/analysis-workspace/panels/media-playback-time-spent)**: analisa a duração da reprodução ao longo do tempo com detalhes sobre os períodos de pico e vale. Suporta granularidade configurável e formato de saída (horas ou minutos).

>[!MORELIKETHIS]
>
>* [Visão geral das dimensões](/help/reporting/dimensions/overview.md)
>* [Visão geral das métricas](/help/reporting/metrics/overview.md)
