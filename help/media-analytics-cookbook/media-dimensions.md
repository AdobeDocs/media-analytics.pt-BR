---
title: Atribuição de fluxo de mídia
description: null
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Atribuição de fluxo de mídia

Esse recurso permite que você vincule as ações do aplicativo aos dados de rastreamento de mídia sem precisar de regras de processamento adicionais e variáveis personalizadas.

## Dimensões de mídia fora do rastreamento de mídia

Com a Atribuição de fluxo de mídia, os clientes agora podem adicionar qualquer dimensão de mídia a todas as outras chamadas de análise, como exibições de página e links personalizados. Durante a implementação, 
você deve adicionar os parâmetros de dados de contexto de mídia às chamadas de rastreamento do Analytics. A lista completa dos parâmetros de dados de contexto usados para mídia está disponível aqui: [Parâmetros de áudio e vídeo.](/help/metrics-and-metadata/audio-video-parameters.md)

Você também precisará reativar a configuração de rastreamento de mídia no Admin Console para cada relatório para o qual deseja habilitar este recurso.

>[!NOTE]
>As métricas de mídia _não_ estão disponíveis para serem usadas fora do rastreamento de mídia porque a maioria delas é calculada pelo Media Analytics
>com base em eventos de heartbeats. Além disso, é importante que as métricas de mídia não sejam infladas por implementações diferentes.

## Como

O exemplo do JavaScript abaixo gerará uma chamada de rastreamento de Link personalizado com o nome definido como "Banner principal".

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

Nos relatórios do Analytics, é possível usar a eVar `Show` para analisar os dados e contar as instâncias de rastreamento de link. O relatório seria semelhante a este:

![](/assets/myShow-rpt-1.png)

## Casos de uso

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)

