---
title: Ativação de relatórios de mídia
description: Saiba mais sobre o conjunto de relatórios de mídia que coleta métricas de mídia.  Siga estas etapas para configurar relatórios de mídia antes do envio dos dados de mídia.
uuid: d306068d-a308-4b6e-8a72-742dda0de428
exl-id: 686d88a5-79b6-4936-ba9e-8f834ef330d1
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/2nLLlF-rFJUR3t-OMbcy5iqF42l-O7oLybXFGhdPyhU
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: b3f03848-ae12-48b2-8aab-cad18567eb32id: c153fd90-23e1-4614-81d3-3cc7571227f7id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559id: e38cbddc-1633-4cd5-bed5-9f289f2a6029id: ef60b66e-5984-4336-ba72-6d978b1b6f87id: f1f1a2d4-0976-4881-b091-c2bb8de7ffacid: f836f655-eebe-4b76-82bc-697955ec1ce3
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 503
ht-degree: 20%

---

# Ativação de relatórios de mídia

Cada conjunto de relatórios que coleta métricas de mídia deve ser configurado antes do envio dos dados de mídia.

1. No [Adobe Analytics](https://experience.adobe.com/analytics), navegue até **[!UICONTROL Admin]** → **[!UICONTROL Conjuntos de relatórios]**.
1. Selecione os conjuntos de relatórios que coletam dados de mídia. Selecione **[!UICONTROL Editar configurações]** → **[!UICONTROL Gerenciamento de mídia]** → **[!UICONTROL Relatórios de mídia]**.

   ![Captura de tela do menu do gerenciador de conjunto de relatórios](assets/media-reporting.png)

1. Na página **[!UICONTROL Relatórios de Mídia]**, habilite os componentes de mídia de streaming desejados (veja abaixo).

1. Selecione **[!UICONTROL Salvar].**

   Se esse conjunto de relatórios já estiver configurado para coletar dados de mídia, uma página de configuração adicional será exibida depois de clicar em **[!UICONTROL Salvar]**. Se você visualizar a página **[!UICONTROL Avaliação da mídia principal]**, continue para a próxima etapa.

## Módulos de streaming de mídia disponíveis

A avaliação de mídia inclui os seguintes módulos:

* **[!UICONTROL Mídia principal]**: obrigatório para todo o rastreamento de streaming de mídia. Ele reserva variáveis de solução para a reprodução de conteúdo e dados de sessão.
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
* **[!UICONTROL Anúncios de mídia]**: permite o rastreamento de anúncios dentro do conteúdo de mídia.
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
* **[!UICONTROL Capítulos de mídia]**: permite o rastreamento de capítulos dentro do conteúdo de mídia.
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
* **[!UICONTROL Qualidade de mídia]**: permite o rastreamento de dados de qualidade de reprodução, incluindo buffering, taxa de bits e eventos de erro.
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
* **[!UICONTROL Metadados de vídeo]**: permite o rastreamento de atributos padrão de conteúdo de vídeo, como programa, temporada e gênero.
   * **Dimensões:**
      * [!UICONTROL Carregamentos de anúncio]
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
* **[!UICONTROL Metadados de áudio]**: permite o rastreamento de atributos de conteúdo de áudio padrão, como artista, álbum e estação.
   * **Dimensões:**
      * [[!UICONTROL Álbum]](/help/reporting/dimensions/album.md)
      * [[!UICONTROL Artista]](/help/reporting/dimensions/artist.md)
      * [[!UICONTROL Autor]](/help/reporting/dimensions/author.md)
      * [[!UICONTROL Rótulo]](/help/reporting/dimensions/label.md)
      * [[!UICONTROL Publicador]](/help/reporting/dimensions/publisher.md)
      * [[!UICONTROL Estação]](/help/reporting/dimensions/station.md)
* **[!UICONTROL Rastreamento do estado do player]**: permite a medição de estados padrão da interface do usuário do player, como tela cheia, legendas ocultas e picture in picture.
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
