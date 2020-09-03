---
audience: end-user
user-guide-title: Adobe Analytics para áudio e vídeo
user-guide-description: Implement Analytics on audio or video sources. Includes the Media SDK and the Media Collection API.
product: adobe analytics
sub-product: media analytics
translation-type: tm+mt
source-git-commit: 126b54173b8b488e53fe27fbc99ad9e83fb2c078
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 99%

---


# Adobe Analytics para áudio e vídeo {#using}

+ [Avaliação de áudio e vídeo no Adobe Analytics](media-overview.md)
+ [Dispositivos e plataformas compatíveis](measurement-options/supported-devices.md)
+ Introdução ao Áudio e vídeo do Analytics {#intro-to-ava}
   + [Pré-requisitos](intro-to-ava/prereqs.md)
   + Caminhos de implementação {#implementation-paths}
      + [Visão geral](intro-to-ava/implementation-paths/implementation-paths.md)
      + [Lado do cliente](intro-to-ava/implementation-paths/client-side-path.md)
      + Outros caminhos de implementação {#other-paths}
         + Rastreamento de marcos do módulo de mídia {#mm-milestone-tracking}
            + [Visão geral do marco](measurement-options/mm-milestone-tracking/milestone-overview.md)
            + [Migrar etapa para o Media Analytics](measurement-options/mm-milestone-tracking/migrate-ms-to-va.md)
            + [Migração do Marco para Link personalizado](measurement-options/mm-milestone-tracking/migrate-ms-to-cl.md)
         + Link personalizado no Analytics {#cl-in-aa}
            + [Guia de implementação de link personalizado](measurement-options/cl-in-aa/cl-impl-guide.md)
         + Primetime {#primetime}
            + [Primetime](intro-to-ava/implementation-paths/primetime-path.md)
         + [Ativação do Audience Manager](intro-to-ava/am-enablement.md)
+ SDK do Media Analytics {#sdk-implement}
   + [Perguntas frequentes sobre o fim do suporte ao SDK do Media Analytics](sdk-implement/end-of-support-faqs.md)
   + [Baixar SDKs](sdk-implement/download-sdks.md)
   + Definir e configurar {#setup}
      + [Visão geral](sdk-implement/setup/setup-overview.md)
      + [Configurar Android](sdk-implement/setup/set-up-android.md)
      + [Configurar iOS](sdk-implement/setup/set-up-ios.md)
      + Configurar JavaScript {#setup-javascript}
         + [Configurar o JavaScript 2.x](sdk-implement/setup/setup-javascript/set-up-js-2.md)
         + [Configurar o JavaScript 3.x](sdk-implement/setup/setup-javascript/set-up-js-3.md)
      + [Configurar Chromecast ](sdk-implement/setup/set-up-chromecast.md)
      + [Configurar Roku ](sdk-implement/setup/set-up-roku.md)
   + Rastrear a reprodução de áudio e vídeo {#track-av-playback}
      + [Visão geral](sdk-implement/track-av-playback/track-core-overview.md)
      + Rastreamento da reprodução principal de áudio e vídeo {#track-core}
         + [Rastreamento da reprodução principal no Android](sdk-implement/track-av-playback/track-core/track-core-android.md)
         + [Rastreamento da reprodução principal no iOS](sdk-implement/track-av-playback/track-core/track-core-ios.md)
         + Rastreamento da reprodução principal no JavaScript {#track-core-javascript}
            + [Rastrear a reprodução principal no JavaScript 2.x](sdk-implement/track-av-playback/track-core/track-core-javascript/track-core-js.md)
            + [Rastrear a reprodução principal no JavaScript 3.x](sdk-implement/track-av-playback/track-core/track-core-javascript/track-core-js3.md)
         + [Rastreamento da reprodução principal no Chromecast](sdk-implement/track-av-playback/track-core/track-core-chromecast.md)
         + [Rastreamento da reprodução principal no Roku](sdk-implement/track-av-playback/track-core/track-core-roku.md)
      + Monitoramento de buffering {#track-buffering}
         + [Rastrear buffering no Android](sdk-implement/track-av-playback/track-buffering/track-buffering-android.md)
         + [Rastrear buffering no iOS](sdk-implement/track-av-playback/track-buffering/track-buffering-ios.md)
         + Rastrear buffering no JavaScript {#track-buffering-js}
            + [Rastrear buffering no JavaScript 2.x](sdk-implement/track-av-playback/track-buffering/track-buffering-js/track-buffering-js.md)
            + [Rastrear buffering no JavaScript 3.x](sdk-implement/track-av-playback/track-buffering/track-buffering-js/track-buffering-js3.md)
         + [Rastrear buffering no Chromecast](sdk-implement/track-av-playback/track-buffering/track-buffering-chromecast.md)
         + [Rastrear buffering no Roku](sdk-implement/track-av-playback/track-buffering/track-buffering-roku.md)
      + Busca de faixa {#track-seeking}
         + [Busca de faixa no Android](sdk-implement/track-av-playback/track-seeking/track-seeking-android.md)
         + [Busca de faixa no iOS](sdk-implement/track-av-playback/track-seeking/track-seeking-ios.md)
         + Busca de faixa no JavaScript {#track-seeking-js}
            + [Rastrear buffering no JavaScript 2.x](sdk-implement/track-av-playback/track-seeking/track-seeking-js/track-seeking-js.md)
            + [Rastrear buffering no JavaScript 3.x](sdk-implement/track-av-playback/track-seeking/track-seeking-js/track-seeking-js3.md)
         + [Busca de faixa no Chromecast](sdk-implement/track-av-playback/track-seeking/track-seeking-chromecast.md)
         + [Busca de faixa no Roku](sdk-implement/track-av-playback/track-seeking/track-seeking-roku.md)
      + Implementar metadados padrão {#impl-std-metadata}
         + [Implementar metadados padrão no Android](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)
         + [Implementar metadados padrão no iOS](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
         + [Chaves de metadados de iOS](sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
         + Implementar metadados padrão no JavaScript {#impl-std-md-js}
            + [Implementar metadados padrão no JavaScript 2.x ](sdk-implement/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)
            + [Implementar metadados padrão no JavaScript 3.x ](sdk-implement/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js3.md)
         + [Implementar metadados padrão no Chromecast](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)
         + [Parâmetros de metadados padrão — Chromecast](sdk-implement/track-av-playback/impl-std-metadata/chromecast-metadata.md)
         + [Implementar metadados padrão no Roku](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)
         + [Parâmetros de metadados padrão — Roku](sdk-implement/track-av-playback/impl-std-metadata/roku-metadata.md)
   + Rastreamento de anúncios {#track-ads}
      + [Visão geral](sdk-implement/track-ads/track-ads-overview.md)
      + [Rastrear anúncios no Android](sdk-implement/track-ads/track-ads-android.md)
      + [Rastrear anúncios no iOS](sdk-implement/track-ads/track-ads-ios.md)
      + Rastrear anúncios no JavaScript {#track-ads-js}
         + [Rastrear anúncios no JavaScript 2.x](sdk-implement/track-ads/track-ads-js/track-ads-js.md)
         + [Rastrear anúncios no JavaScript 3.x](sdk-implement/track-ads/track-ads-js/track-ads-js3.md)
      + [Rastrear anúncios no Chromecast](sdk-implement/track-ads/track-ads-chromecast.md)
      + [Rastrear anúncios no Roku](sdk-implement/track-ads/track-ads-roku.md)
      + Implementar metadados de anúncio padrão {#impl-std-ad-metadata}
         + [Implementar Metadados de anúncio padrão no Android](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
         + [Implementar Metadados de anúncio padrão no iOS](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
         + Implementar Metadados de anúncio padrão no JavaScript {#impl-std-ad-md-js}
            + [Implementar metadados de anúncio padrão no JavaScript 2.x ](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js.md)
            + [Implementar metadados de anúncio padrão no JavaScript 3.x ](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
         + [Implementar Metadados de publicidade padrão no Roku](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   + Rastrear capítulos e segmentos {#track-chapters}
      + [Visão geral](sdk-implement/track-chapters/track-chapters-overview.md)
      + [Rastrear capítulos e segmentos no Android](sdk-implement/track-chapters/track-chapters-android.md)
      + [Rastrear capítulos e segmentos no iOS](sdk-implement/track-chapters/track-chapters-ios.md)
      + Rastrear capítulos e segmentos no JavaScript {#track-chapters-js}
         + [Rastrear capítulos e segmentos no JavaScript 2.x](sdk-implement/track-chapters/track-chapters-js/track-chapters-js.md)
         + [Rastrear capítulos e segmentos no JavaScript 3.x](sdk-implement/track-chapters/track-chapters-js/track-chapters-js3.md)
      + [Rastrear capítulos e segmentos no Chromecast](sdk-implement/track-chapters/track-chapters-chromecast.md)
      + [Rastrear capítulos e segmentos no Roku](sdk-implement/track-chapters/track-chapters-roku.md)
   + Rastrear a qualidade da experiência {#track-qos}
      + [Visão geral](sdk-implement/track-qos/track-qos-overview.md)
      + [Rastrear a qualidade da experiência no Android](sdk-implement/track-qos/track-qos-android.md)
      + [Rastrear a qualidade da experiência no iOS](sdk-implement/track-qos/track-qos-ios.md)
      + Rastrear a qualidade da experiência no JavaScript {#track-qos-js}
         + [Rastrear a qualidade da experiência no JavaScript 2.x](sdk-implement/track-qos/track-qos-js/track-qos-js.md)
         + [Rastrear a qualidade da experiência no JavaScript 3.x](sdk-implement/track-qos/track-qos-js/track-qos-js3.md)
      + [Rastrear a qualidade da experiência no Chromecast](sdk-implement/track-qos/track-qos-chromecast.md)
      + [Rastrear a qualidade da experiência no Roku](sdk-implement/track-qos/track-qos-roku.md)
   + Rastrear erros {#track-errors}
      + [Visão geral](sdk-implement/track-errors/track-errors-overview.md)
      + [Rastrear erros no Android](sdk-implement/track-errors/track-errors-android.md)
      + [Rastrear erros no iOS](sdk-implement/track-errors/track-errors-ios.md)
      + Rastrear erros no JavaScript {#track-errors-js}
         + [Rastrear erros no JavaScript 2.x](sdk-implement/track-errors/track-errors-js/track-errors-js.md)
         + [Rastrear erros no JavaScript 3.x](sdk-implement/track-errors/track-errors-js/track-errors-js3.md)
      + [Rastrear erros no Chromecast](sdk-implement/track-errors/track-errors-chromecast.md)
      + [Rastrear erros no Roku](sdk-implement/track-errors/track-errors-roku.md)
   + [Opção de rejeição e privacidade](sdk-implement/opt-out-privacy.md)
   + Cenários de rastreamento {#tracking-scenarios}
      + [Reprodução de VOD sem anúncios](sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
      + [Reprodução de VOD com anúncios precedentes](sdk-implement/tracking-scenarios/vod-preroll-ads.md)
      + [Reprodução de VOD com anúncios ignorados](sdk-implement/tracking-scenarios/vod-skipped-ads.md)
      + [Reprodução de VOD com um capítulo](sdk-implement/tracking-scenarios/vod-one-chapter.md)
      + [Reprodução de VOD com um capítulo ignorado](sdk-implement/tracking-scenarios/vod-skipped-chapter.md)
      + [Reprodução de VOD com busca no conteúdo principal](sdk-implement/tracking-scenarios/vod-seeking.md)
      + [Reprodução de VOD com buffering](sdk-implement/tracking-scenarios/vod-buffering.md)
      + [Vários rastreadores de VOD ao mesmo tempo](sdk-implement/tracking-scenarios/vod-multi-trackers.md)
      + [Um rastreador de VOD para várias sessões](sdk-implement/tracking-scenarios/vod-multi-track-one-session.md)
      + [Conteúdo principal ao vivo](sdk-implement/tracking-scenarios/live-main-content.md)
      + [Conteúdo principal ao vivo com monitoramento sequencial](sdk-implement/tracking-scenarios/live-sequential.md)
   + Validação {#validation}
      + [Visão geral da validação](sdk-implement/validation/validation-overview.md)
      + [Teste 1: reprodução padrão](sdk-implement/validation/test1-standard-playback.md)
      + [Teste 2: Interrupção de mídia](sdk-implement/validation/test2-media-interrupt.md)
      + [Detalhes da chamada de teste](sdk-implement/validation/test-call-details.md)
      + [Descrições do parâmetro Heartbeat](sdk-implement/validation/heartbeat-params.md)
      + Depuração {#debugging}
         + [Depuração do SDK](sdk-implement/validation/debugging/sdk-debugging.md)
         + [Configurar o Adobe Debug](sdk-implement/validation/debugging/config-adobe-debug.md)
         + [Criar um novo relatório de depuração](sdk-implement/validation/debugging/create-new-debug-report.md)
         + [Painéis e relatórios de depuração](sdk-implement/validation/debugging/debug-dash-repts.md)
   + Análises em aplicativos OTT {#analytics-with-ott}
      + [Rastrear estados do aplicativo](sdk-implement/analytics-with-ott/track-app-states.md)
      + [Rastrear ações do aplicativo](sdk-implement/analytics-with-ott/track-app-actions.md)
      + [Definir IDs de usuário](sdk-implement/analytics-with-ott/set-user-ids.md)
      + [OTT e Audience Manager](sdk-implement/analytics-with-ott/ott-am.md)
      + [OTT e Experience Cloud](sdk-implement/analytics-with-ott/ott-experience-cloud.md)
   + Guia {#cookbook}
      + [Guia do SDK](sdk-implement/cookbook/sdk-cookbook-overview.md)
      + [O manuseio de aplicativos é interrompido durante a reprodução](sdk-implement/cookbook/app-interrupts.md)
      + [Resolver a ocorrência de main:play entre anúncios](sdk-implement/cookbook/fix-ad-play-ad.md)
      + [Resumo de sessões inativas](sdk-implement/cookbook/resuming-inactive.md)
      + [Rastreamento no SceneGraph (Roku)](sdk-implement/cookbook/sdk-track-scenegraph.md)
   + Migração do Media Analytics 1.x para 2.x {#va-1x-to-2x}
      + [Visão geral da migração](sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
      + [Comparação de código: 1.x para 2.x](sdk-implement/va-1x-to-2x/code-comparison-1x-2x.md)
      + [Conversão da API do de 1.x para 2.x](sdk-implement/va-1x-to-2x/1x-2x-api-change.md)
   + SDK do Media Analytics para a migração do Launch {#sdk-to-launch}
      + [SDK para migração do Launch](sdk-implement/sdk-to-launch/sdk-to-launch-migration.md)
      + Guias da plataforma de migração do SDK para o Launch {#sdk-to-launch-migration-platforms}
         + [Android](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)
         + [iOS](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)
         + [JS](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-js.md)
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
   + Linhas do tempo do rastreamento de mídia {#mc-api-timelines}
      + [Linha do tempo 1 - Visualização do conteúdo até o fim](media-collection-api/mc-api-timelines/mc-api-timeline-1.md)
      + [Linha do tempo 2 - Usuário abandona a sessão](media-collection-api/mc-api-timelines/mc-api-timeline-2.md)
      + [Linha do tempo 3 - Capítulos](media-collection-api/mc-api-timelines/mc-api-timeline-3.md)
+ Guia {#media-analytics-cookbook}
   + [Guia](media-analytics-cookbook/media-analytics-cookbook.md)
   + [Atribuição de fluxo de mídia](media-analytics-cookbook/media-dimensions.md)
+ Métricas e metadados {#metrics-and-metadata}
   + [Parâmetros de áudio e vídeo](metrics-and-metadata/audio-video-parameters.md)
   + [Parâmetros de anúncio](metrics-and-metadata/ad-parameters.md)
   + [Parâmetros de capítulo](metrics-and-metadata/chapter-parameters.md)
   + [Parâmetros de estado do player](metrics-and-metadata/player-state-parameters.md)
   + [Parâmetros de qualidade](metrics-and-metadata/quality-parameters.md)
   + [Segmentos](metrics-and-metadata/segments.md)
   + [Métricas calculadas](metrics-and-metadata/calculated-metrics.md)
+ Relatórios e análise {#media-reports}
   + [Ativação de relatórios de mídia](media-reports/media-reports-enable.md)
   + Relatórios de mídia padrão {#media-default-reports}
      + [Visão geral dos relatórios padrão](media-reports/media-default-reports/default-reports-overview.md)
      + [Visão geral da mídia](media-reports/media-default-reports/media-reports-overview.md)
      + [Detalhes da mídia](media-reports/media-default-reports/media-reports-detail.md)
      + [Faixa de horário da mídia](media-reports/media-default-reports/media-reports-daypart.md)
      + [Visualizadores simultâneos de mídia](media-reports/media-default-reports/media-concurrent-viewers.md)
      + [Obter dados de relatório JSON de visualizadores simultâneos](media-reports/media-default-reports/get-concurrent-json.md)
   + Painéis do Media Workspace {#media-workspace-panels}
      + [Painel Visualizadores simultâneos de mídia](media-reports/media-workspace-panels/media-concurrent-viewers.md)
   + [Modelos do Workspace de mídia](media-reports/media-workspace-templates.md)
+ [Rastrear o conteúdo baixado](media-collection-api/track-downloaded-content.md)
+ [Federated Analytics](federated-analytics.md)
+ Rastreamento do estado do player {#player-state-tracking}
   + [Visão geral](sdk-implement/player-state-tracking/player-state-overview.md)
   + [Estados padrão e personalizados](sdk-implement/player-state-tracking/standard-and-custom-states.md)
   + [Implementação e relatórios](sdk-implement/player-state-tracking/implementation-and-reporting.md)
   + [Exemplos de rastreamento do estado do player](sdk-implement/player-state-tracking/player-state-examples.md)
+ Recursos adicionais {#additional-resources}
   + [Notas de versão](additional-resources/doc-updates.md)
