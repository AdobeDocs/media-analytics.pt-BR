---
title: O que é a atribuição de fluxo de mídia?
description: Saiba como vincular ações do aplicativo aos dados de rastreamento de mídia sem precisar de regras de processamento adicionais e variáveis personalizadas.
exl-id: 75cc9088-776d-4b10-b358-9fff956a7eb7
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 39%

---

# Atribuição de fluxo de mídia {#media-stream-attribution}

Com a Atribuição de fluxo de mídia, é possível vincular as ações do aplicativo aos dados de rastreamento de mídia sem precisar de regras de processamento adicionais e variáveis personalizadas.

## Dimensões de mídia fora do rastreamento de mídia

É possível adicionar dimensões de mídia às chamadas do analytics, como exibições de página e links personalizados. Durante a implementação, 
você deve adicionar os parâmetros de dados de contexto de mídia às chamadas de rastreamento do Analytics. Para exibir a lista completa dos parâmetros de dados de contexto disponíveis usados para mídia, consulte [Parâmetros de áudio e vídeo.](/help/implementation/variables/audio-video-parameters.md)

Para ativar esse recurso para um relatório específico, reative a configuração de rastreamento de mídia no Admin Console.

>[!NOTE]
>
>As métricas de mídia são _not_ disponível para uso fora do rastreamento de mídia, pois a maioria é calculada pelo Streaming Media Analytics com base em eventos de pulsação. Além disso, é importante que as métricas de mídia não sejam infladas por implementações diferentes.

## Usar a atribuição de fluxo de mídia

O exemplo do JavaScript abaixo gera uma chamada de rastreamento de Link personalizado com o nome definido como &quot;Banner de exemplo&quot;.

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

Nos relatórios do Analytics, é possível usar a eVar `Show` para analisar os dados e contar as instâncias de rastreamento de link. O relatório seria semelhante a este:

![](/assets/myShow-rpt-1.png)

## Casos de uso

Os exemplos a seguir mostram casos de uso para o seguinte:

* Posicionamento da categoria
* Posicionamento do Hero
* Engajamento
* Subscrições

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)
