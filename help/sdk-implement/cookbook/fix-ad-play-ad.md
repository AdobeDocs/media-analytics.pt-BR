---
seo-title: Resolving main play appearing between ads
title: Resolving main play appearing between ads
uuid: 228b4812-c23e-40c8-ae2b-e15ca69b0bc2
translation-type: tm+mt
source-git-commit: 8c20af925a1043c90b84d7d13021848725e05500

---


# Resolver a ocorrência de main:play entre anúncios{#resolving-main-play-appearing-between-ads}

## PROBLEMA

Em alguns cenários de rastreamento de anúncios, você pode encontrar chamadas `main:play` que ocorrem inesperadamente entre o fim de um anúncio e o início do próximo anúncio. If the delay between the ad complete call and the next ad start call is greater than 250 milliseconds, the Media SDK will fall back to sending `main:play` calls. Se esse recurso a `main:play` ocorrer durante um ad break precedente, a métrica de início de conteúdo poderá ser definida antecipadamente.

Uma lacuna entre anúncios, como descrito acima, é interpretada pelo SDK do Media como conteúdo principal porque não há sobreposição a nenhum conteúdo de anúncio. O SDK do Media não tem nenhuma informação de anúncio definida nele e o reprodutor está no estado de execução. Se não houver informações de anúncio e o reprodutor estiver no estado de execução, o SDK do Media creditará a duração da lacuna em relação ao conteúdo principal por padrão. Ele não poderá creditar a duração da reprodução em relação às informações de anúncio nulas.

## IDENTIFICAÇÃO

While using Adobe Debug or a network packet sniffer such as Charles, if you see the following Heartbeat calls in this order during a pre-roll ad break:

* Início da sessão: `s:event:type=start` &amp; `s:asset:type=main`
* Início do anúncio: `s:event:type=start` &amp; `s:asset:type=ad`
* Reprodução do anúncio: `s:event:type=play` &amp; `s:asset:type=ad`
* Anúncio concluído: `s:event:type=complete` &amp; `s:asset:type=ad`
* Reprodução do conteúdo principal: `s:event:type=play` &amp; `s:asset:type=main`**(inesperado)**

* Início do anúncio: `s:event:type=start` &amp; `s:asset:type=ad`
* Reprodução do anúncio: `s:event:type=play` &amp; `s:asset:type=ad`
* Anúncio concluído: `s:event:type=complete` &amp; `s:asset:type=ad`
* Reprodução do conteúdo principal: `s:event:type=play` &amp; `s:asset:type=main`**(esperado)**

## RESOLUÇÃO

***Atrasar o acionamento da chamada de Anúncio concluído.***

Lide com a lacuna no reprodutor, chamando `trackEvent:AdComplete` um pouco depois para o primeiro anúncio, seguido imediatamente por `trackEvent:AdStart` para o segundo anúncio. O aplicativo deve esperar para chamar o evento `AdComplete` após a conclusão do primeiro anúncio. Certifique-se de chamar `trackEvent:AdComplete` para o último anúncio no ad break. Se o reprodutor identificar que o ativo de anúncio atual é o último no ad break, chame `trackEvent:AdComplete` imediatamente. Essa resolução resultará em menos de 1 segundo de tempo adicional gasto com o anúncio para a unidade de anúncio anterior.

**No início do ad break, incluindo precedente:**

* Crie a instância de objeto `adBreak` para o ad break; por exemplo, `adBreakObject`.

* Chama `trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);`.

**Em cada início de ativo de anúncio:**

* **Chama`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >Chame isso somente se o anúncio anterior não tiver sido concluído. Considere um valor booleano para manter um estado "`isinAd`" para o anúncio anterior.

* Crie a instância do objeto de anúncio para o ativo de anúncio: por exemplo, `adObject`.
* Populate the ad metadata, `adCustomMetadata`.
* Chama `trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata);`.
* Call `trackPlay()` if this is the first ad in a pre-roll ad break.

**Em cada conclusão de ativo de anúncio:**

* **Não efetuar uma chamada**

   >[!NOTE]
   >
   >If the application knows it is the last ad in the ad break, call `trackEvent:AdComplete` here and skip setting `trackEvent:AdComplete` in the `trackEvent:AdBreakComplete`

**Ao ignorar o anúncio:**

* Chama `trackEvent(MediaHeartbeat.Event.AdSkip);`.

**Na conclusão do ad break:**

* **Chama`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >If this step is already performed above as part of the last `trackEvent:AdComplete` call then this can be skipped.

* Chama `trackEvent(MediaHeartbeat.Event.AdBreakComplete);`.

