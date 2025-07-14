---
title: O que é a atribuição de fluxo de mídia?
description: Saiba como vincular ações do aplicativo aos dados de rastreamento de mídia sem precisar de regras de processamento adicionais e variáveis personalizadas.
exl-id: 75cc9088-776d-4b10-b358-9fff956a7eb7
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 88%

---

# Atribuição de fluxo de mídia {#media-stream-attribution}

Com a atribuição de fluxo de mídia, é possível vincular as ações do aplicativo aos dados de rastreamento de mídia sem precisar de regras de processamento adicionais e variáveis personalizadas.

## Dimensões de mídia fora do rastreamento de mídia

Você pode adicionar dimensões de mídia às chamadas do Analytics, como exibições de página e links personalizados. Durante a implementação, você deve adicionar os parâmetros de dados de contexto de mídia às chamadas de rastreamento do Analytics. Para exibir a lista completa dos parâmetros de dados de contexto disponíveis para uso em mídias, consulte [Parâmetros de áudio e vídeo.](/help/implementation/variables/audio-video-parameters.md)

Para ativar esse recurso para um relatório específico, reative a configuração de rastreamento de mídia no Admin Console.

>[!NOTE]
>
>As métricas de mídia _não_ estão disponíveis para uso fora do rastreamento de mídia porque a maioria delas é calculada pela Coleção de mídia de streaming com base em eventos de heartbeat. Além disso, é importante que as métricas de mídia não sejam infladas por implementações diferentes.

## Usar a atribuição de fluxo de mídia

O exemplo de JavaScript abaixo gera uma chamada de rastreamento de link personalizado com o nome definido como “banner hero”.

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

Nos relatórios do Analytics, é possível usar a eVar `Show` para analisar os dados e contar as instâncias de rastreamento de link. O relatório seria semelhante a este:

![](/assets/myShow-rpt-1.png)

## Casos de uso

Os exemplos a seguir mostram casos de uso para:

* Posicionamento da categoria
* Posicionamento do principal
* Engajamento
* Subscrições

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)
