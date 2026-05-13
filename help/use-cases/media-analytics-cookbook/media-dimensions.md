---
title: O que é a atribuição de fluxo de mídia?
description: Saiba como vincular ações do aplicativo aos dados de rastreamento de mídia sem precisar de regras de processamento adicionais e variáveis personalizadas.
exl-id: 75cc9088-776d-4b10-b358-9fff956a7eb7
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/G0RufpSDBB65tr4XJRvPU2keKgKxv1uDviyhqzxEVD4
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: e4f5f438-eabb-4c54-9133-b817e3d125f5id: e7d92df1-c5ba-4e93-85df-f83171b889beid: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 215
ht-degree: 87%

---

# Atribuição de fluxo de mídia {#media-stream-attribution}

Com a atribuição de fluxo de mídia, é possível vincular as ações do aplicativo aos dados de rastreamento de mídia sem precisar de regras de processamento adicionais e variáveis personalizadas.

## Dimensões de mídia fora do rastreamento de mídia

Você pode adicionar dimensões de mídia às chamadas do Analytics, como exibições de página e links personalizados. Durante a implementação, você deve adicionar os parâmetros de dados de contexto de mídia às chamadas de rastreamento do Analytics.

Para habilitar esse recurso para um relatório específico, reabilite a configuração de rastreamento de mídia no Admin Console.

>[!NOTE]
>
>As métricas de mídia _não_ estão disponíveis para uso fora do rastreamento de mídia porque a maioria delas é calculada pelos serviços de mídia de streaming com base em eventos de heartbeat. Além disso, é importante que as métricas de mídia não sejam infladas por implementações diferentes.

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
