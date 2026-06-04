---
title: Configurar a extensão de tag do Media Analytics
description: Use a extensão Adobe Media Analytics (3.x SDK) for Audio and Video tag para implementar mídia de transmissão somente no Analytics.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 12%

---

# Configurar a extensão de tag do Media Analytics

A extensão de tag do Adobe Media Analytics (3.x SDK) para áudio e vídeo implanta o Media SDK para JavaScript (3.x) por meio de tags, sem instalação manual do JavaScript. Esta página aborda a configuração de Tags. Para instalar o SDK no código, consulte [Configurar JavaScript para mídia de streaming](javascript.md). Para novas implementações, considere a [extensão de tag do Web SDK](/help/implementation/edge/web-sdk-tags.md) recomendada para o caminho do Edge.

* **Pré-requisitos**: conclua a [visão geral da implementação somente do Analytics](overview.md).

## Instalar e configurar a extensão

Adicione a instância do Media Tracker a um site habilitado para tags, instalando e configurando a extensão na interface da Coleção de dados. Para obter detalhes sobre instalação e configuração, consulte a [Extensão Adobe Media Analytics (3.x SDK) for Audio and Video](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=pt-BR).

## Rastrear eventos de mídia

Com a extensão configurada, rastreie cada evento de mídia usando seu método de rastreador. Consulte a guia **Media SDK JS 3.x** em cada página de [evento](/help/implementation/events/overview.md) e [variável](/help/implementation/variables/overview.md) para obter as chamadas exatas.

## Próxima etapa

Uma vez concluída a implementação, você pode [Configurar relatórios para implementações somente do Analytics](/help/reporting/setup/analytics-reporting.md).

>[!MORELIKETHIS]
>
>* [Extensão Adobe Media Analytics (3.x SDK) for Audio and Video](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=pt-BR)
>* [Configurar o JavaScript para mídia de streaming (no código)](javascript.md)
>* [Visão geral dos eventos](/help/implementation/events/overview.md)
