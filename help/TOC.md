---
product: adobe analytics
audience: end-user
user-guide-title: Adobe Analytics para mídia de streaming
breadcrumb-title: Guia do Media Analytics
user-guide-description: Implementar o Adobe Analytics para mídia de streaming. Inclui o SDK de mídia e a API de coleta de mídia.
sub-product: media analytics
source-git-commit: fa72159d968e50c3b3e02853e8509533d91f1785
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 96%

---


# Adobe Analytics para mídia de streaming {#using}

+ [Guia do Analytics para mídia de streaming](media-overview.md)
+ Notas de versão {#release-notes}
   + [Notas de versão de mídias de streaming](additional-resources/release-notes.md)
+ Introdução {#getting-started}
   + [Visão geral](getting-started/getting-started.md)
   + [Pré-requisitos ](getting-started/prereqs.md)
   + [Dispositivos compatíveis](getting-started/supported-devices.md)
   + [Documentação de mídia de streaming](getting-started/implementation-documentation.md)
   + [SDKs, bibliotecas e extensões](getting-started/download-sdks.md)
   + Fim do suporte {#end-of-support}
      + [Fim do suporte ao SDK móvel do Media Analytics](additional-resources/end-of-support-faqs.md)
      + Herdados - SDK de mídia independente para a migração do Launch {#sdk-to-launch} 
         + [Visão geral](legacy/sdk-to-launch/sdk-to-launch-migration.md)
         + [Android - SDK de mídia para o Launch](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)
         + [iOS - SDK de mídia para o Launch](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)
         + [JavaScript - SDK de mídia para o Launch](legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-js.md)
+ Implementação {#implementation}
   + [Visão geral da implementação](implementation/overview.md)
   + Implementações do Edge (recomendado) {#edge-recommended}
      + SDKs do Media Edge / Extensão {#media-edge-sdk}
         + [SDKs do Media Edge / Configuração de extensão](/help/implementation/edge/implementation-edge.md)
         + [SDKs móveis do Media Edge](/help/implementation/edge/edge-mobile-sdk.md)
      + [API Media Edge](/help/implementation/edge/implementation-edge-api.md)
   + Implementações somente do Adobe Analytics {#analytics-only}
      + SDKs de mídia / Extensão {#media-sdk}
         + [SDK da Web JavaScript](implementation/media-sdk/setup/web-implementation.md)
         + [Extensão do Media Analytics](implementation/media-sdk/setup/web-implementation-tags.md)
         + [SDKs móveis](implementation/media-sdk/setup/mobile-implementation.md)
         + SDKs OTT {#ott-setup}
            + [Instalar o SDK do Chromecast](implementation/media-sdk/setup/set-up-chromecast.md)
            + [Instalar o SDK do Roku](implementation/media-sdk/setup/set-up-roku.md)
      + APIs de coleção de mídia - Implementação {#streaming-media-apis}
         + [Coleção de mídia](implementation/media-collection-api/mc-api-overview.md)
         + [Início rápido da API](implementation/media-collection-api/mc-api-impl/mc-api-quick-start.md)
         + [Solicitação de sessões](implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)
         + [Solicitação de eventos](implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)
         + [Parâmetros da solicitação](implementation/media-collection-api/mc-api-ref/mc-api-req-params.md)
         + [Tipos e descrições de eventos](implementation/media-collection-api/mc-api-ref/mc-api-event-types.md)
         + Implementar a API {#mc-api-impl}
            + [Definição do tipo de solicitação HTTP no seu reprodutor](implementation/media-collection-api/mc-api-impl/mc-api-set-http-req.md)
            + [Obter uma ID de sessão](implementation/media-collection-api/mc-api-impl/mc-api-obtain-sid.md)
            + [Implementar uma solicitação de eventos ](implementation/media-collection-api/mc-api-impl/mc-api-impl-events-req.md)
            + [Esquemas de validação JSON](implementation/media-collection-api/mc-api-ref/mc-api-json-validation.md)
            + [Validar solicitações de evento](implementation/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
            + [Enviar eventos de ping](implementation/media-collection-api/mc-api-impl/mc-api-sed-pings.md)
            + [Enviar dados de QoE](implementation/media-collection-api/mc-api-impl/mc-api-sending-qoe.md)
            + [Suporte a metadados personalizados](implementation/media-collection-api/mc-api-impl/mc-api-custom-meta.md)
            + [Condições de tempo limite](implementation/media-collection-api/mc-api-impl/mc-api-timeout.md)
            + [Controlar a ordem dos eventos](implementation/media-collection-api/mc-api-impl/mc-api-ctrl-order.md)
            + [Enfileirar eventos quando a resposta das sessões é lenta](implementation/media-collection-api/mc-api-impl/mc-api-queuing.md)
   + Variáveis {#variables}
      + [Parâmetros de mídia de streaming](implementation/variables/audio-video-parameters.md)
      + [Parâmetros de publicidade](implementation/variables/ad-parameters.md)
      + [Parâmetros de capítulo ](implementation/variables/chapter-parameters.md)
      + [Parâmetros de estado do player ](implementation/variables/player-state-parameters.md)
      + [Parâmetros de qualidade ](implementation/variables/quality-parameters.md)
      + [Métricas calculadas ](implementation/variables/calculated-metrics.md)
+ Relatórios {#media-reports}
   + [Ativação de relatórios de mídia](reporting/media-reports-enable.md)
   + [Sobre os segmentos ](reporting/segments.md)
   + Relatórios de mídia padrão {#media-default-reports}
      + [Visão geral dos relatórios padrão](reporting/reports-and-analytics/default-reports-overview.md)
      + [Visão geral da mídia](reporting/reports-and-analytics/media-reports-overview.md)
      + [Detalhes da mídia](reporting/reports-and-analytics/media-reports-detail.md)
      + [Relatório de faixa de horário de mídia](reporting/reports-and-analytics/media-reports-daypart.md)
      + [Relatório de visualizadores simultâneos de mídia](reporting/reports-and-analytics/media-concurrent-viewers-reports.md)
   + Painéis do Espaço de trabalho de mídia {#media-workspace-panels}
      + [Painel Audiência média por minuto da mídia](reporting/workspace/average-minute-audience.md)
      + [Painel Visualizadores simultâneos de mídia](reporting/workspace/media-concurrent-viewers-overview.md)
      + [Painel Tempo gasto com a reprodução da mídia](reporting/workspace/media-playback-time-spent.md)
   + [Modelos do Espaço de trabalho de mídia ](reporting/workspace/media-workspace-templates.md)
   + [Obter dados de visualizadores simultâneos por meio da API](reporting/reports-and-analytics/get-concurrent-json20.md)
   + [Obter dados de Tempo gasto com a reprodução da mídia por meio da API](reporting/reports-and-analytics/get-mediaplaybacktimespent-json20.md)
+ Casos de uso {#media-use-cases}
   + [Casos de uso do SDK de mídia](use-cases/cookbook/sdk-cookbook-overview.md)
   + Rastreamento do estado do player {#player-state-tracking}
      + [Visão geral ](use-cases/player-state-tracking/player-state-overview.md)
      + [Estados padrão e personalizados](use-cases/player-state-tracking/standard-and-custom-states.md)
      + [Implementação e relatórios](use-cases/player-state-tracking/implementation-and-reporting.md)
      + [Acompanhamento do estado de vários players](use-cases/player-state-tracking/multiple-player-states.md)
      + [Exemplos de acompanhamento do estado do player](use-cases/player-state-tracking/player-state-examples.md)
   + [Acompanhar o conteúdo baixado offline](use-cases/track-downloaded-content.md)
   + [Federated Analytics ](use-cases/federated-analytics.md)
   + [Lidar com interrupções do aplicativo durante a reprodução](use-cases/cookbook/app-interrupts.md)
   + [Atribuição de fluxo de mídia](use-cases/media-analytics-cookbook/media-dimensions.md)
   + [Resumo de sessões inativas](use-cases/cookbook/resuming-inactive.md)
   + [Acompanhamento do Roku no SceneGraph](use-cases/cookbook/sdk-track-scenegraph.md)
   + [Manuseio de intervalos entre anúncios](use-cases/cookbook/fix-ad-play-ad.md)
   + Linhas do tempo {#timelines}
      + [Início e término do capítulo](use-cases/timelines/chapter-start-end.md)
      + [Exibir até o fim do conteúdo](use-cases/timelines/view-to-end-of-content.md)
      + [Abandonar sessão](use-cases/timelines/user-abandons-session.md)
   + Uso do Analytics em aplicativos OTT {#analytics-with-ott}
      + [Rastrear estados do aplicativo](use-cases/analytics-with-ott/track-app-states.md)
      + [Rastrear ações do aplicativo](use-cases/analytics-with-ott/track-app-actions.md)
      + [Definir IDs de usuário](use-cases/analytics-with-ott/set-user-ids.md)
      + [OTT e Audience Manager ](use-cases/analytics-with-ott/ott-am.md)
      + [OTT e Experience Cloud ](use-cases/analytics-with-ott/ott-experience-cloud.md)
+ Rastreamento {#tracking}
   + Acompanhamento {#track-av-playback}
      + [Visão geral ](use-cases/track-av-playback/track-core-overview.md)
      + Rastrear a reprodução de streaming de mídia principal {#track-core}
         + [Rastrear a reprodução principal no JavaScript 3.x](use-cases/track-av-playback/track-core/track-core-javascript/track-core-js3.md)
         + [Rastreamento da reprodução principal no Chromecast](use-cases/track-av-playback/track-core/track-core-chromecast.md)
         + [Rastreamento da reprodução principal no Roku](use-cases/track-av-playback/track-core/track-core-roku.md)
      + Monitoramento de buffering {#track-buffering}
         + [Rastrear buffering no JavaScript 3.x](use-cases/track-av-playback/track-buffering/track-buffering-js/track-buffering-js3.md)
         + [Rastrear buffering no Chromecast](use-cases/track-av-playback/track-buffering/track-buffering-chromecast.md)
         + [Rastrear buffering no Roku](use-cases/track-av-playback/track-buffering/track-buffering-roku.md)
      + Busca de faixa {#track-seeking}
         + [Busca de faixa no JavaScript 3.x](use-cases/track-av-playback/track-seeking/track-seeking-js/track-seeking-js3.md)
         + [Busca de faixa no Chromecast](use-cases/track-av-playback/track-seeking/track-seeking-chromecast.md)
         + [Busca de faixa no Roku](use-cases/track-av-playback/track-seeking/track-seeking-roku.md)
      + Implementar metadados padrão {#impl-std-metadata}
         + [Implementar metadados padrão no JavaScript 3.x](use-cases/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js3.md)
         + [Implementar metadados padrão no Chromecast](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)
         + [Parâmetros de metadados padrão — Chromecast](use-cases/track-av-playback/impl-std-metadata/chromecast-metadata.md)
         + [Implementar metadados padrão no Roku ](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)
         + [Parâmetros de metadados padrão — Roku](use-cases/track-av-playback/impl-std-metadata/roku-metadata.md)
      + Rastreamento de anúncios {#track-ads}
         + [Visão geral ](use-cases/track-ads/track-ads-overview.md)
         + [Rastrear anúncios no JavaScript 3.x](use-cases/track-ads/track-ads-js/track-ads-js3.md)
         + [Rastrear anúncios no Chromecast](use-cases/track-ads/track-ads-chromecast.md)
         + [Rastrear anúncios no Roku](use-cases/track-ads/track-ads-roku.md)
         + Implementar metadados de anúncio padrão {#impl-std-ad-metadata}
            + [Implementar metadados de anúncio padrão no JavaScript 3.x](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
            + [Implementar Metadados de publicidade padrão no Roku ](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
      + Rastrear capítulos e segmentos {#track-chapters}
         + [Visão geral ](use-cases/track-chapters/track-chapters-overview.md)
         + [Rastrear capítulos e segmentos no JavaScript 3.x](use-cases/track-chapters/track-chapters-js/track-chapters-js3.md)
         + [Rastrear capítulos e segmentos no Chromecast](use-cases/track-chapters/track-chapters-chromecast.md)
         + [Rastrear capítulos e segmentos no Roku](use-cases/track-chapters/track-chapters-roku.md)
      + Rastrear a qualidade da experiência {#track-qos}
         + [Visão geral ](use-cases/track-qos/track-qos-overview.md)
         + [Rastrear a qualidade da experiência no JavaScript 3.x](use-cases/track-qos/track-qos-js/track-qos-js3.md)
         + [Rastrear a qualidade da experiência no Chromecast](use-cases/track-qos/track-qos-chromecast.md)
         + [Rastrear a qualidade da experiência no Roku](use-cases/track-qos/track-qos-roku.md)
      + Rastrear erros {#track-errors}
         + [Visão geral ](use-cases/track-errors/track-errors-overview.md)
         + [Rastrear erros no JavaScript 3.x](use-cases/track-errors/track-errors-js/track-errors-js3.md)
         + [Rastrear erros no Chromecast](use-cases/track-errors/track-errors-chromecast.md)
         + [Rastrear erros no Roku](use-cases/track-errors/track-errors-roku.md)
+ Privacidade e segurança {#streaming-media-privacy}
   + [Configurações da opção de rejeição e privacidade](privacy/opt-out-privacy.md)
   + [Segurança](privacy/security.md)
+ Implementações herdadas {#legacy-implementations}
   + [Herdados - Visão geral](legacy/setup/legacy-setup-overview.md)
   + [Herdados - Baixar SDKs](legacy/legacy-download-sdks.md)
   + Herdados - SDKs de mídia {#legacy-media-sdks}
      + [Herdados - Visão geral do SDK de mídia](legacy/media-sdk/setup/setup-overview.md)
      + [Configurar Android](legacy/media-sdk/setup/set-up-android.md)
      + [Configurar iOS](legacy/media-sdk/setup/set-up-ios.md)
      + Configurar JavaScript {#setup-javascript}
         + [Configurar o JavaScript 2.x](legacy/media-sdk/setup/setup-javascript/set-up-js-2.md)
   + [Sobre a medição de pulsação](legacy/heartbeat-measurement.md)
   + [Adobe Primetime e Analytics para mídia de streaming](legacy/intro-to-ava/implementation-paths/primetime-path.md)
   + [Capacitação de Adobe Audience Management](legacy/intro-to-ava/am-enablement.md)
   + [Implementação de link personalizado](legacy/measurement-options/cl-in-aa/cl-impl-guide.md)
   + Rastreamento de marcos herdado {#legacy-milestone-tracking}
      + [Rastreamento de marcos herdado](legacy/measurement-options/mm-milestone-tracking/milestone-overview.md)
      + [Migrar marco para VA](legacy/measurement-options/mm-milestone-tracking/migrate-ms-to-va.md)
      + [Migrar marco para CL](legacy/measurement-options/mm-milestone-tracking/migrate-ms-to-cl.md)
   + Validação {#validation}
      + [Visão geral da validação](legacy/validation/validation-overview.md)
      + [Teste 1: reprodução padrão](legacy/validation/test1-standard-playback.md)
      + [Teste 2: Interrupção de mídia](legacy/validation/test2-media-interrupt.md)
      + [Detalhes da chamada de teste](legacy/validation/test-call-details.md)
      + [Descrições do parâmetro do Heartbeat](legacy/validation/heartbeat-params.md)
      + Depuração {#debugging}
         + [Depuração do SDK](legacy/validation/debugging/sdk-debugging.md)
   + [Migração herdada: VHL 1.x para VHL 2.x](legacy/va-1x-to-2x/mig-1x-2x-overview.md)
   + [Comparação de código: v1.x e v2.x](legacy/va-1x-to-2x/code-comparison-1x-2x.md)
   + [Acompanhamento de APIs: 1x a 2x](legacy/va-1x-to-2x/1x-2x-api-change.md)
   + [Herdados - Introdução ao AVA](legacy/intro-to-ava/implementation-paths/implementation-paths.md)
   + [Caminho do lado do cliente](legacy/intro-to-ava/implementation-paths/client-side-path.md)
   + Rastreamento herdado {#track-av-playback}
      + [Rastreamento da reprodução principal no Android](use-cases/track-av-playback/track-core/track-core-android.md)
      + [Rastreamento da reprodução principal no iOS](use-cases/track-av-playback/track-core/track-core-ios.md)
      + Rastreamento da reprodução principal no JavaScript {#track-core-javascript}
         + [Rastrear a reprodução principal no JavaScript 2.x](use-cases/track-av-playback/track-core/track-core-javascript/track-core-js.md)
         + [Rastrear buffering no Android](use-cases/track-av-playback/track-buffering/track-buffering-android.md)
         + [Rastrear buffering no iOS](use-cases/track-av-playback/track-buffering/track-buffering-ios.md)
         + Rastrear buffering no JavaScript {#track-buffering-js}
            + [Rastrear buffering no JavaScript 2.x](use-cases/track-av-playback/track-buffering/track-buffering-js/track-buffering-js.md)
         + [Busca de faixa no Android](use-cases/track-av-playback/track-seeking/track-seeking-android.md)
         + [Busca de faixa no iOS](use-cases/track-av-playback/track-seeking/track-seeking-ios.md)
         + Busca de faixa no JavaScript {#track-seeking-js}
            + [Busca de faixa no JavaScript 2.x](use-cases/track-av-playback/track-seeking/track-seeking-js/track-seeking-js.md)
         + [Implementar metadados padrão no Android](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)
         + [Implementar metadados padrão no iOS](use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
         + [Chaves de metadados de iOS](use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
         + Implementar metadados padrão no JavaScript {#impl-std-md-js}
            + [Implementar metadados padrão no JavaScript 2.x](use-cases/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)
      + Rastreamento de anúncios {#track-ads}
         + [Rastrear anúncios no Android](use-cases/track-ads/track-ads-android.md)
         + [Rastrear anúncios no iOS](use-cases/track-ads/track-ads-ios.md)
         + Rastrear anúncios no JavaScript {#track-ads-js}
            + [Rastrear anúncios no JavaScript 2.x](use-cases/track-ads/track-ads-js/track-ads-js.md)
            + [Implementar Metadados de publicidade padrão no Android ](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
            + [Implementar Metadados de publicidade padrão no iOS ](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
            + Implementar Metadados de anúncio padrão no JavaScript {#impl-std-ad-md-js}
               + [Implementar metadados de anúncio padrão no JavaScript 2.x](use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js.md)
      + Rastrear capítulos e segmentos {#track-chapters}
         + [Rastrear capítulos e segmentos no Android](use-cases/track-chapters/track-chapters-android.md)
         + [Rastrear capítulos e segmentos no iOS](use-cases/track-chapters/track-chapters-ios.md)
         + Rastrear capítulos e segmentos no JavaScript {#track-chapters-js}
            + [Rastrear capítulos e segmentos no JavaScript 2.x](use-cases/track-chapters/track-chapters-js/track-chapters-js.md)
         + [Rastrear a qualidade da experiência no Android](use-cases/track-qos/track-qos-android.md)
         + [Rastrear a qualidade da experiência no iOS](use-cases/track-qos/track-qos-ios.md)
         + Rastrear a qualidade da experiência no JavaScript {#track-qos-js}
            + [Rastrear a qualidade da experiência no JavaScript 2.x](use-cases/track-qos/track-qos-js/track-qos-js.md)
      + Rastrear erros {#track-errors}
         + [Rastrear erros no Android](use-cases/track-errors/track-errors-android.md)
         + [Rastrear erros no iOS ](use-cases/track-errors/track-errors-ios.md)
         + Rastrear erros no JavaScript {#track-errors-js}
            + [Rastrear erros no JavaScript 2.x](use-cases/track-errors/track-errors-js/track-errors-js.md)
      + Cenários de rastreamento {#tracking-scenarios}
         + [Reprodução de VOD sem anúncios](use-cases/tracking-scenarios/vod-no-intrs-details.md)
         + [Reprodução de VOD com anúncios antes da exibição](use-cases/tracking-scenarios/vod-preroll-ads.md)
         + [Reprodução de VOD com anúncios ignorados](use-cases/tracking-scenarios/vod-skipped-ads.md)
         + [Reprodução de VOD com um capítulo](use-cases/tracking-scenarios/vod-one-chapter.md)
         + [Reprodução de VOD com um capítulo ignorado](use-cases/tracking-scenarios/vod-skipped-chapter.md)
         + [Reprodução de VOD com busca no conteúdo principal](use-cases/tracking-scenarios/vod-seeking.md)
         + [Reprodução de VOD com buffering](use-cases/tracking-scenarios/vod-buffering.md)
         + [Vários rastreadores de VOD ao mesmo tempo](use-cases/tracking-scenarios/vod-multi-trackers.md)
         + [Um rastreador de VOD para várias sessões](use-cases/tracking-scenarios/vod-multi-track-one-session.md)
         + [Conteúdo principal ao vivo ](use-cases/tracking-scenarios/live-main-content.md)
         + [Conteúdo principal ao vivo com rastreamento sequencial](use-cases/tracking-scenarios/live-sequential.md)
