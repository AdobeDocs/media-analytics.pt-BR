---
title: Visão geral das métricas de streaming de mídia
description: Saiba como as métricas de transmissão de mídia são calculadas e organizadas no Adobe Analytics e no Customer Journey Analytics.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 3%

---


# Visão geral das métricas de streaming de mídia

As métricas no Streaming Media Analytics são contagens orientadas por eventos e durações computadas pelo back-end de mídia. O reprodutor de mídia envia eventos como início da sessão, reprodução, ping e início do anúncio; o back-end de mídia processa esses eventos e finaliza valores de métrica na chamada de fechamento da sessão.

## Como as métricas são calculadas

As métricas de mídia de transmissão seguem quatro padrões de cálculo principais:

* **Sinalizadores acionados por evento**: Defina a primeira vez que um evento de qualificação chegar em uma sessão. Um evento [`play`](/help/implementation/events/playback/play.md) para o conteúdo principal define o sinalizador [[!UICONTROL Início do conteúdo]](content-starts.md); um evento [`adStart`](/help/implementation/events/ads/ad-start.md) define [[!UICONTROL Início do anúncio]](ad-starts.md). O sinalizador é relatado uma vez por sessão na chamada de fechamento, não por evento.

* **Durações acumuladas**: soma os intervalos entre eventos de ping enquanto um determinado estado de reprodução está ativo. [[!UICONTROL O tempo gasto no conteúdo]](content-time-spent.md) é acumulado enquanto o conteúdo principal está sendo reproduzido; [[!UICONTROL O tempo gasto no anúncio]](ad-time-spent.md) é acumulado enquanto um anúncio está sendo reproduzido. O intervalo de ping recomendado da Adobe é de 10 segundos para o conteúdo principal e 1 segundo durante os anúncios, de modo que as métricas de tempo gasto só podem ser tão granulares quanto o intervalo de ping da implementação.

* **Contagens de eventos**: controle o total de ocorrências na sessão. Métricas de qualidade como [[!UICONTROL Eventos de buffer]](buffer-events.md), [[!UICONTROL Alterações na taxa de bits]](bitrate-changes.md), [[!UICONTROL Eventos de erro]](error-events.md) e [[!UICONTROL Pausar eventos]](pause-events.md) contam todas as ocorrências, não apenas as primeiras.

* **Fluxos impactados**: os sinalizadores de nível de sessão são definidos como 1 se o evento correspondente ocorrer a qualquer momento durante a sessão, independentemente de quantas vezes. Use essas métricas para medir o alcance, ao mesmo tempo em que usa a métrica de contagem de eventos para medir a gravidade. Por exemplo, você pode usar [[!UICONTROL Fluxos afetados pelo buffer]](buffer-impacted-streams.md) para determinar a proporção de sessões que foram afetadas pelo buffer em todas as sessões de reprodução.

## Disponibilidade por sistema de relatórios

| Sistema de relatório | Como as métricas chegam |
| --- | --- |
| Adobe Analytics | Preenchida com [Variáveis de dados de contexto](https://experienceleague.adobe.com/pt-br/docs/analytics/implementation/vars/page-vars/contextdata). Algumas métricas preenchem automaticamente eventos de solução usando essas variáveis de dados de contexto, enquanto outras devem ser mapeadas para um evento personalizado usando [Regras de processamento](https://experienceleague.adobe.com/pt-br/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview). As métricas que preenchem valores automaticamente devem ter sua respectiva [configuração de conjunto de relatórios de mídia de streaming](../setup/analytics-reporting.md) habilitada primeiro. |
| Customer Journey Analytics | Campos XDM em `xdm.mediaReporting.sessionDetails` e nós relacionados, originados de qualquer conjunto de dados que inclua dados de mídia de streaming. Você deve criar cada métrica com as configurações desejadas em [configurações do componente de Visualização de dados](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/cja-dataviews/component-settings/overview). |
| Feeds de dados | As métricas aparecem nas colunas `event_list` e `post_event_list` como IDs de evento. Cada arquivo de feed contém um arquivo `events.csv` que contém a pesquisa de todas as métricas, incluindo as métricas de mídia de transmissão. |

>[!MORELIKETHIS]
>
>* [Visão geral dos eventos](/help/implementation/events/overview.md): os eventos do player que preenchem as métricas
>* [Visão geral das variáveis](/help/implementation/variables/overview.md): os dados que os eventos carregam para o Adobe
>* [Visão geral das dimensões](/help/reporting/dimensions/overview.md): as dimensões de relatório que as variáveis preenchem
