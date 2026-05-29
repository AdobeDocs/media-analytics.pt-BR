---
title: Visão geral das dimensões de mídia de streaming
description: Saiba como as dimensões de mídia de transmissão são preenchidas e organizadas no Adobe Analytics e no Customer Journey Analytics.
feature: Dimensions
role: User, Admin
source-git-commit: da289f8d425fcbaece42519a9ea7d061f80e4591
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 6%

---


# Visão geral das dimensões de mídia de streaming

As dimensões no Streaming Media Analytics permitem cortar e filtrar métricas por nome de conteúdo, tipo de fluxo, nome do anúncio e dezenas de outros atributos. A maioria é definida pelo reprodutor no início da sessão e transportada até o fechamento da sessão.

## Como as dimensões são preenchidas

As dimensões de mídia de transmissão seguem três padrões de população principais:

* **Fornecido pelo reprodutor de mídia**: a origem da maioria das dimensões. O player envia esses valores na chamada [Início da sessão](/help/implementation/events/session/session-start.md) e o back-end de mídia os anexa a todos os eventos subsequentes na sessão. O que o reprodutor envia no início da sessão é o que aparece nos relatórios. Os exemplos incluem [[!UICONTROL Tipo de fluxo]](/help/reporting/dimensions/stream-type.md), [[!UICONTROL Nome do conteúdo]](/help/reporting/dimensions/content-name.md) e [[!UICONTROL Comprimento do conteúdo]](/help/reporting/dimensions/content-length.md).

* **Valores derivados**: dimensões que o back-end de mídia calcula a partir do estado de reprodução acumulado, em vez de ler um valor fornecido pelo player. [[!UICONTROL O segmento de conteúdo]](/help/reporting/dimensions/content-segment.md) é calculado a partir da posição do indicador de reprodução durante a reprodução. [[!UICONTROL Caminho da mídia]](/help/reporting/dimensions/media-path.md) rastreia as transições entre os estados de conteúdo e anúncio na sessão. Essas dimensões não podem ser substituídas pelo reprodutor.

* **Classificações**: opcional. Em vez de preencher dimensões separadas, você pode manter os dados de classificação usando [Conjuntos de classificações](https://experienceleague.adobe.com/pt-br/docs/analytics/components/classifications/sets/overview) (Adobe Analytics) ou [Conjuntos de dados de pesquisa](https://experienceleague.adobe.com/en/docs/analytics-platform/using/compare-aa-cja/upgrade-to-cja/create-datasets/cja-upgrade-dataset-lookup) (Customer Journey Analytics).

## Disponibilidade por sistema de relatórios

| Sistema de relatório | Como as dimensões chegam |
| --- | --- |
| Adobe Analytics | Preenchida com [Variáveis de dados de contexto](https://experienceleague.adobe.com/pt-br/docs/analytics/implementation/vars/page-vars/contextdata). Algumas dimensões preenchem automaticamente as dimensões usando essas variáveis de dados de contexto, enquanto outras devem ser preenchidas usando as [Regras de processamento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview). As dimensões que preenchem valores automaticamente devem ter sua respectiva [configuração de conjunto de relatórios de mídia de streaming](../../implementation/media-sdk/setup/media-reports-enable.md) habilitada primeiro. |
| Customer Journey Analytics | Campos XDM normalmente em `xdm.mediaReporting.sessionDetails`, originados de qualquer conjunto de dados que inclua dados de mídia de transmissão. Você deve criar cada dimensão com as configurações desejadas em [configurações do componente de Visualização de dados](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/overview). |
| Feeds de dados | As dimensões preenchidas automaticamente têm seus próprios nomes de colunas de feed de dados (como `videostreamtype`, `videoname` ou `videolength`). As dimensões que exigem regras de processamento usam nomes de coluna `evar`. |
| Audience Manager | Dados de contexto encaminhados do Adobe Analytics. Disponível somente quando o encaminhamento do lado do servidor do Analytics para o Audience Manager estiver configurado. |

>[!MORELIKETHIS]
>
>* [Visão geral das métricas](../metrics/overview.md): referência às métricas de mídia de transmissão
>* [Mapeamento de parâmetros](/help/implementation/parameters-mapping.md): concluir referência de variável para coluna para XDM
>* [Segmentos de mídia](/help/reporting/segments.md): segmentos internos que usam dimensões de mídia de streaming
