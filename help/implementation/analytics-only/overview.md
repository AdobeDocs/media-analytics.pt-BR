---
title: Visão geral da implementação somente no Analytics
description: Pré-requisitos e métodos de implementação para o complemento Adobe Analytics para mídia de streaming, usado para implementações exclusivas do Analytics.
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: 7b5232f25f3aa26e8566783557163f316af3fe57
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 5%

---

# Visão geral da implementação somente no Analytics

Implementações exclusivas do Analytics usam o complemento Adobe Analytics para mídia de streaming para enviar dados diretamente para o Adobe Analytics, sem o Edge Network. Esses métodos permanecem totalmente compatíveis. Para novas implementações, a Adobe recomenda a [implementação do Edge](/help/implementation/edge/overview.md), pois ela disponibiliza dados para a Customer Journey Analytics, o Adobe Journey Optimizer e o Real-Time CDP, além do Adobe Analytics.

## Pré-requisitos

1. **Conclua os pré-requisitos gerais.** Consulte os [pré-requisitos gerais](/help/getting-started/prereqs.md).

1. **Confirme uma implementação do Adobe Analytics.** Uma implementação de mídia de transmissão somente no Analytics requer uma implementação básica do Adobe Analytics. Consulte [Implementar o Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=pt-BR).

1. **Obter a URL do servidor de rastreamento de mídia.** Peça ao representante da Adobe Analytics a URL do servidor de rastreamento de mídia (a URL `collection-api-server`). O domínio normalmente segue o padrão `[your_namespace].hb-api.omtrdc.net`.

1. **Baixe o SDK ou instale a extensão.** Dependendo da sua plataforma, [baixe a SDK](/help/getting-started/download-sdks.md) atual ou instale a extensão de tag necessária.

## Escolha seu método de implementação

Cada página aborda a configuração específica de mídia de transmissão. O código por evento e por variável está em [Eventos](/help/implementation/events/overview.md) e [Variáveis](/help/implementation/variables/overview.md).

| Base de código | No código | Uso de tags |
|---|---|---|
| Web (JavaScript) | [JavaScript](javascript.md) | [Extensão de tag do Media Analytics](javascript-tags.md) |
| Chromecast | [Chromecast](chromecast.md) | — |
| API | [API da coleção de mídia](media-collection-api.md) | — |

## Próxima etapa

Uma vez concluída a implementação, você pode [Configurar relatórios para implementações somente do Analytics](/help/reporting/setup/analytics-reporting.md).

>[!MORELIKETHIS]
>
>* [Visão geral da implementação](/help/implementation/overview.md)
>* [Visão geral dos eventos](/help/implementation/events/overview.md)
>* [Visão geral das variáveis](/help/implementation/variables/overview.md)
