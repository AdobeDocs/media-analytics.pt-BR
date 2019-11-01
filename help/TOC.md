---
product: Media Analytics
audience: usuário final
user-guide-title: Adobe Analytics para áudio e vídeo
translation-type: tm+mt
source-git-commit: 6bf606e97dc11c20b4523393523feffe632ae287

---


# Adobe Analytics for Audio and Video {#using}

+ [Avaliação de áudio e vídeo no Adobe Analytics](media-overview.md)
+ Measurement Options {#measurement-options}
   + Media Module Milestone Tracking {#mm-milestone-tracking}
      + [Visão geral do marco](measurement-options/mm-milestone-tracking/milestone-overview.md)
      + [Migrar etapa para o Media Analytics](measurement-options/mm-milestone-tracking/migrate-ms-to-va.md)
      + [Migração do Marco para Link personalizado](measurement-options/mm-milestone-tracking/migrate-ms-to-cl.md)
   + Link personalizado no Analytics {#cl-in-aa}
      + [Guia de implementação de link personalizado](measurement-options/cl-in-aa/cl-impl-guide.md)
+ Introdução à análise de áudio e vídeo {#intro-to-ava}
   + [Pré-requisitos](intro-to-ava/prereqs.md)
   + Caminhos de implementação {#implementation-paths}
      + [Visão geral](intro-to-ava/implementation-paths/implementation-paths.md)
      + [Lado do cliente](intro-to-ava/implementation-paths/client-side-path.md)
      + [Adobe Experience Platform Launch](intro-to-ava/implementation-paths/launch-path.md)
      + [Primetime](intro-to-ava/implementation-paths/primetime-path.md)
   + [Ativação do Audience Manager](intro-to-ava/am-enablement.md)
+ SDK do Media Analytics {#sdk-implement}
   + [Baixar SDKs](sdk-implement/download-sdks.md)
   + Definir e configurar {#setup}
      + [Visão geral](sdk-implement/setup/setup-overview.md)
      + [Configurar Android](sdk-implement/setup/set-up-android.md)
      + [Configurar iOS](sdk-implement/setup/set-up-ios.md)
      + [Configurar JavaScript](sdk-implement/setup/set-up-js.md)
      + [Configurar Chromecast](sdk-implement/setup/set-up-chromecast.md)
      + [Configurar Roku](sdk-implement/setup/set-up-roku.md)
   + Rastrear a reprodução de áudio e vídeo {#track-av-playback}
      + [Visão geral](sdk-implement/track-av-playback/track-core-overview.md)
      + Track Core Audio and Video Playback {#track-core}
         + [Rastrear reprodução principal no Android](sdk-implement/track-av-playback/track-core/track-core-android.md)
         + [Rastrear reprodução principal no iOS](sdk-implement/track-av-playback/track-core/track-core-ios.md)
         + [Rastrear reprodução principal em JavaScript](sdk-implement/track-av-playback/track-core/track-core-js.md)
         + [Rastrear reprodução principal no Chromecast](sdk-implement/track-av-playback/track-core/track-core-chromecast.md)
         + [Rastrear reprodução principal no Roku](sdk-implement/track-av-playback/track-core/track-core-roku.md)
      + Track Buffering {#track-buffering}
         + [Monitoramento de buffer no Android](sdk-implement/track-av-playback/track-buffering/track-buffering-android.md)
         + [Monitoramento de buffer no iOS](sdk-implement/track-av-playback/track-buffering/track-buffering-ios.md)
         + [Monitoramento de buffer no JavaScript](sdk-implement/track-av-playback/track-buffering/track-buffering-js.md)
         + [Monitoramento de buffer no Chromecast](sdk-implement/track-av-playback/track-buffering/track-buffering-chromecast.md)
         + [Monitoramento de buffer no Roku](sdk-implement/track-av-playback/track-buffering/track-buffering-roku.md)
      + Track Seeking {#track-seeking}
         + [Busca de rastreamento no Android](sdk-implement/track-av-playback/track-seeking/track-seeking-android.md)
         + [Rastrear busca no iOS](sdk-implement/track-av-playback/track-seeking/track-seeking-ios.md)
         + [Busca de rastreamento no JavaScript](sdk-implement/track-av-playback/track-seeking/track-seeking-js.md)
         + [Busca de rastreamento no Chromecast](sdk-implement/track-av-playback/track-seeking/track-seeking-chromecast.md)
         + [Busca de rastreamento no Roku](sdk-implement/track-av-playback/track-seeking/track-seeking-roku.md)
      + Implementar metadados padrão {#impl-std-metadata}
         + [Implementar metadados padrão no Android](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)
         + [Implementar metadados padrão no iOS](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
         + [Chaves de metadados do iOS](sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
         + [Implementar metadados padrão no JavaScript](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-js.md)
         + [Implementar metadados padrão no Chromecast](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)
         + [Parâmetros padronizados de metadados - Chromecast](sdk-implement/track-av-playback/impl-std-metadata/chromecast-metadata.md)
         + [Implementar metadados padrão no Roku](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)
         + [Parâmetros padrão de metadados - Roku](sdk-implement/track-av-playback/impl-std-metadata/roku-metadata.md)
   + Rastreamento de anúncios {#track-ads}
      + [Visão geral](sdk-implement/track-ads/track-ads-overview.md)
      + [Rastrear anúncios no Android](sdk-implement/track-ads/track-ads-android.md)
      + [Rastrear anúncios no iOS](sdk-implement/track-ads/track-ads-ios.md)
      + [Rastrear anúncios em JavaScript](sdk-implement/track-ads/track-ads-js.md)
      + [Rastrear anúncios no Chromecast](sdk-implement/track-ads/track-ads-chromecast.md)
      + [Rastrear anúncios no Roku](sdk-implement/track-ads/track-ads-roku.md)
      + Implementar Metadados de publicidade padrão {#impl-std-ad-metadata}
         + [Implementar Metadados de publicidade padrão no Android](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
         + [Implementar Metadados de publicidade padrão no iOS](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
         + [Implementar Metadados de publicidade padrão no JavaScript](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-js.md)
         + [Implementar Metadados de publicidade padrão no Roku](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   + Rastrear capítulos e segmentos {#track-chapters}
      + [Visão geral](sdk-implement/track-chapters/track-chapters-overview.md)
      + [Rastrear capítulos e segmentos no Android](sdk-implement/track-chapters/track-chapters-android.md)
      + [Rastrear capítulos e segmentos no iOS](sdk-implement/track-chapters/track-chapters-ios.md)
      + [Rastrear capítulos e segmentos no JavaScript](sdk-implement/track-chapters/track-chapters-js.md)
      + [Rastrear capítulos e segmentos no Chromecast](sdk-implement/track-chapters/track-chapters-chromecast.md)
      + [Rastrear capítulos e segmentos no Roku](sdk-implement/track-chapters/track-chapters-roku.md)
   + Rastrear a qualidade da experiência {#track-qos}
      + [Visão geral](sdk-implement/track-qos/track-qos-overview.md)
      + [Qualidade de rastreamento da experiência no Android](sdk-implement/track-qos/track-qos-android.md)
      + [Acompanhar a qualidade da experiência no iOS](sdk-implement/track-qos/track-qos-ios.md)
      + [Monitoramento da qualidade da experiência em JavaScript](sdk-implement/track-qos/track-qos-js.md)
      + [Qualidade de rastreamento da experiência no Chromecast](sdk-implement/track-qos/track-qos-chromecast.md)
      + [Qualidade de rastreamento da experiência no Roku](sdk-implement/track-qos/track-qos-roku.md)
   + Track Errors {#track-errors}
      + [Visão geral](sdk-implement/track-errors/track-errors-overview.md)
      + [Rastrear erros no Android](sdk-implement/track-errors/track-errors-android.md)
      + [Rastrear erros no iOS](sdk-implement/track-errors/track-errors-ios.md)
      + [Rastrear erros no JavaScript](sdk-implement/track-errors/track-errors-js.md)
      + [Rastrear erros no Chromecast](sdk-implement/track-errors/track-errors-chromecast.md)
      + [Rastrear erros no Roku](sdk-implement/track-errors/track-errors-roku.md)
   + [Recusar e privacidade](sdk-implement/opt-out-privacy.md)
   + Tracking Scenarios {#tracking-scenarios}
      + [Reprodução VOD sem anúncios](sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
      + [Reprodução VOD com anúncios precedentes](sdk-implement/tracking-scenarios/vod-preroll-ads.md)
      + [Reprodução VOD com anúncios ignorados](sdk-implement/tracking-scenarios/vod-skipped-ads.md)
      + [Reprodução VOD com um capítulo](sdk-implement/tracking-scenarios/vod-one-chapter.md)
      + [Reprodução VOD com um capítulo ignorado](sdk-implement/tracking-scenarios/vod-skipped-chapter.md)
      + [Reprodução VOD com busca no conteúdo principal](sdk-implement/tracking-scenarios/vod-seeking.md)
      + [Reprodução VOD com buffering](sdk-implement/tracking-scenarios/vod-buffering.md)
      + [Vários rastreadores VOD ao mesmo tempo](sdk-implement/tracking-scenarios/vod-multi-trackers.md)
      + [Um rastreador VOD para várias sessões](sdk-implement/tracking-scenarios/vod-multi-track-one-session.md)
      + [Conteúdo principal disponível](sdk-implement/tracking-scenarios/live-main-content.md)
      + [Conteúdo principal ao vivo com monitoramento sequencial](sdk-implement/tracking-scenarios/live-sequential.md)
   + Validação {#validation}
      + [Visão geral da validação](sdk-implement/validation/validation-overview.md)
      + [Teste 1: reprodução padrão](sdk-implement/validation/test1-standard-playback.md)
      + [Teste 2: Interrupção de mídia](sdk-implement/validation/test2-media-interrupt.md)
      + [Testar detalhes da chamada](sdk-implement/validation/test-call-details.md)
      + [Descrições do parâmetro de pulsação](sdk-implement/validation/heartbeat-params.md)
      + Depuração {#debugging}
         + [Depuração do SDK](sdk-implement/validation/debugging/sdk-debugging.md)
         + [Configurar o Adobe Debug](sdk-implement/validation/debugging/config-adobe-debug.md)
         + [Criar um novo relatório de depuração](sdk-implement/validation/debugging/create-new-debug-report.md)
         + [Painéis e relatórios de depuração](sdk-implement/validation/debugging/debug-dash-repts.md)
   + Analytics in OTT Apps {#analytics-with-ott}
      + [Rastrear estados do aplicativo](sdk-implement/analytics-with-ott/track-app-states.md)
      + [Rastrear ações do aplicativo](sdk-implement/analytics-with-ott/track-app-actions.md)
      + [Definir IDs de usuário](sdk-implement/analytics-with-ott/set-user-ids.md)
      + [OTT e Audience Manager](sdk-implement/analytics-with-ott/ott-am.md)
      + [OTT e Experience Cloud](sdk-implement/analytics-with-ott/ott-experience-cloud.md)
   + Guia {#cookbook}
      + [Livro de receitas do SDK](sdk-implement/cookbook/sdk-cookbook-overview.md)
      + [O manuseio de aplicativos é interrompido durante a reprodução](sdk-implement/cookbook/app-interrupts.md)
      + [Resolver a ocorrência de main:play entre anúncios](sdk-implement/cookbook/fix-ad-play-ad.md)
      + [Retomando Sessões Inativas](sdk-implement/cookbook/resuming-inactive.md)
      + [Rastreamento no SceneGraph (Roku)](sdk-implement/cookbook/sdk-track-scenegraph.md)
   + Media Analytics 1.x to 2.x Migration {#va-1x-to-2x}
      + [Visão geral da migração](sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
      + [Comparação de código do : 1.x para 2.x](sdk-implement/va-1x-to-2x/code-comparison-1x-2x.md)
      + [Conversão da API do de 1.x para 2.x](sdk-implement/va-1x-to-2x/1x-2x-api-change.md)
+ API Media Collection (RESTful) {#media-collection-api}
   + [Visão geral](media-collection-api/mc-api-overview.md)
   + Referência da API {#mc-api-ref}
      + [Solicitação de sessões](media-collection-api/mc-api-ref/mc-api-sessions-req.md)
      + [Solicitação de eventos](media-collection-api/mc-api-ref/mc-api-events-req.md)
      + [Parâmetros da solicitação](media-collection-api/mc-api-ref/mc-api-req-params.md)
      + [Tipos e descrições de eventos](media-collection-api/mc-api-ref/mc-api-event-types.md)
      + [Esquemas de validação JSON](media-collection-api/mc-api-ref/mc-api-json-validation.md)
   + Implementar a API {#mc-api-impl}
      + [Início rápido](media-collection-api/mc-api-impl/mc-api-quick-start.md)
      + [Definição do tipo de solicitação HTTP no seu reprodutor](media-collection-api/mc-api-impl/mc-api-set-http-req.md)
      + [Obter uma ID de sessão](media-collection-api/mc-api-impl/mc-api-obtain-sid.md)
      + [Implementar uma solicitação de eventos](media-collection-api/mc-api-impl/mc-api-impl-events-req.md)
      + [Validar solicitações de evento](media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
      + [Enviar eventos de ping](media-collection-api/mc-api-impl/mc-api-sed-pings.md)
      + [Enviar dados de QoE](media-collection-api/mc-api-impl/mc-api-sending-qoe.md)
      + [Suporte a metadados personalizados](media-collection-api/mc-api-impl/mc-api-custom-meta.md)
      + [Condições de tempo limite](media-collection-api/mc-api-impl/mc-api-timeout.md)
      + [Controlar a ordem dos eventos](media-collection-api/mc-api-impl/mc-api-ctrl-order.md)
      + [Enfileirar eventos quando a resposta das sessões é lenta](media-collection-api/mc-api-impl/mc-api-queuing.md)
   + Media Tracking Timelines {#mc-api-timelines}
      + [Linha do tempo 1 - Visualização do conteúdo até o fim](media-collection-api/mc-api-timelines/mc-api-timeline-1.md)
      + [Linha do tempo 2 - Usuário abandona a sessão](media-collection-api/mc-api-timelines/mc-api-timeline-2.md)
      + [Linha do tempo 3 - Capítulos](media-collection-api/mc-api-timelines/mc-api-timeline-3.md)
   + [Acompanhar conteúdo baixado](media-collection-api/track-downloaded-content.md)
+ Guia {#media-analytics-cookbook}
   + [Guia](media-analytics-cookbook/media-analytics-cookbook.md)
   + [Atribuição de fluxo de mídia](media-analytics-cookbook/media-dimensions.md)
+ Métricas e metadados {#metrics-and-metadata}
   + [Parâmetros de áudio e vídeo](metrics-and-metadata/audio-video-parameters.md)
   + [Parâmetros de anúncio](metrics-and-metadata/ad-parameters.md)
   + [Parâmetros de capítulo](metrics-and-metadata/chapter-parameters.md)
   + [Parâmetros de qualidade](metrics-and-metadata/quality-parameters.md)
   + [Segmentos](metrics-and-metadata/segments.md)
   + [Métricas calculadas](metrics-and-metadata/calculated-metrics.md)
+ Reporting and Analysis {#media-reports}
   + [Ativação de relatórios de mídia](media-reports/media-reports-enable.md)
   + Media Default Reports {#media-default-reports}
      + [Visão geral dos relatórios padrão](media-reports/media-default-reports/default-reports-overview.md)
      + [Visão geral da mídia](media-reports/media-default-reports/media-reports-overview.md)
      + [Detalhe da mídia](media-reports/media-default-reports/media-reports-detail.md)
      + [Faixa de horário de mídia](media-reports/media-default-reports/media-reports-daypart.md)
      + [Visualizadores simultâneos de mídia](media-reports/media-default-reports/media-concurrent-viewers.md)
      + [Obter dados de relatório JSON de visualizadores simultâneos](media-reports/media-default-reports/get-concurrent-json.md)
   + [Modelos do Media Workspace](media-reports/media-workspace-templates.md)
+ [Federated Analytics](federated-analytics.md)
+ Recursos adicionais {#additional-resources}
   + [Recursos](additional-resources/doc-updates.md)
