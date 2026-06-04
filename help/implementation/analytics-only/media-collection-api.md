---
title: Configurar a API da coleção de mídia para mídia de transmissão
description: Use a API da coleção de mídia para enviar dados de mídia de transmissão diretamente para o Adobe Analytics com chamadas RESTful HTTP.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 1%

---

# Configurar a API da coleção de mídia para mídia de transmissão

A API Media Collection envia dados de mídia de transmissão diretamente para o Adobe Analytics usando chamadas RESTful HTTP. Como é totalmente personalizável, ele oferece suporte a rastreamento personalizado e dispositivos que os SDKs não abrangem. Use-a quando uma SDK não for uma opção para sua plataforma.

* **Pré-requisitos**: conclua a [visão geral da implementação somente do Analytics](overview.md).

## Implementar a API

Abra uma sessão com uma solicitação `sessionStart` e envie eventos subsequentes para a sessão retornada. Para obter os formatos de solicitação/resposta, parâmetros, esquemas de validação e orientações de implementação completos, consulte a [Referência da API Media Collection](../media-collection-api/mc-api-overview.md).

## Rastrear eventos de mídia

Consulte a guia **API da Coleção de Mídia** em cada página de [evento](/help/implementation/events/overview.md) e [variável](/help/implementation/variables/overview.md) para obter as cargas exatas.

## Próxima etapa

Uma vez concluída a implementação, você pode [Configurar relatórios para implementações somente do Analytics](/help/reporting/setup/analytics-reporting.md).

>[!MORELIKETHIS]
>
>* [Referência da API Media Collection](../media-collection-api/mc-api-overview.md)
>* [Visão geral dos eventos](/help/implementation/events/overview.md)
>* [Visão geral das variáveis](/help/implementation/variables/overview.md)
