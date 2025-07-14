---
title: Resolvendo o problema da reprodução principal aparecendo entre os anúncios
description: Saiba como lidar com chamadas inesperadas de main:play entre anúncios.
uuid: 228b4812-c23e-40c8-ae2b-e15ca69b0bc2
exl-id: f27ce2ba-7584-4601-8837-d8316c641708
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 97%

---


# Lidar com lacunas que aparecem entre anúncios{#resolving-main-play-appearing-between-ads}

## PROBLEMA

Em alguns cenários de rastreamento de anúncios, você pode encontrar chamadas `main:play` que ocorrem inesperadamente entre o fim de um anúncio e o início do próximo anúncio. Se o atraso entre a chamada de conclusão do anúncio e a chamada de início do próximo anúncio for maior que 250 milissegundos, o SDK do Media recorrerá ao envio de chamadas `main:play`. Se esse recurso a `main:play` ocorrer durante um ad break precedente, a métrica de início de conteúdo poderá ser definida antecipadamente.

Uma lacuna entre anúncios, como descrito acima, é interpretada pelo SDK do Media como conteúdo principal porque não há sobreposição a nenhum conteúdo de anúncio. O SDK do Media não tem nenhuma informação de anúncio definida nele e o reprodutor está no estado de execução. Se não houver informações de anúncio e o reprodutor estiver no estado de execução, o SDK do Media creditará a duração da lacuna em relação ao conteúdo principal por padrão. Ele não poderá creditar a duração da reprodução em relação às informações de anúncio nulas.

## IDENTIFICAÇÃO

Ao usar o Adobe Debug ou um farejador de pacotes de rede, como o Charles, se você vir as seguintes chamadas de heartbeat nesta ordem durante um ad break precedente:

* Início da sessão: `s:event:type=start` &amp; `s:asset:type=main`
* Início do anúncio: `s:event:type=start` &amp; `s:asset:type=ad`
* Reprodução do anúncio: `s:event:type=play` &amp; `s:asset:type=ad`
* Anúncio concluído: `s:event:type=complete` &amp; `s:asset:type=ad`
* Reprodução do conteúdo principal: `s:event:type=play` &amp; `s:asset:type=main` **(inesperado)**

* Início do anúncio: `s:event:type=start` &amp; `s:asset:type=ad`
* Reprodução do anúncio: `s:event:type=play` &amp; `s:asset:type=ad`
* Anúncio concluído: `s:event:type=complete` &amp; `s:asset:type=ad`
* Reprodução do conteúdo principal: `s:event:type=play` &amp; `s:asset:type=main` **(esperado)**

## RESOLUÇÃO

***Atrasar o acionamento da chamada de Anúncio concluído.***

Lide com a lacuna no reprodutor, chamando `trackEvent:AdComplete` um pouco depois para o primeiro anúncio, seguido imediatamente por `trackEvent:AdStart` para o segundo anúncio. O aplicativo deve esperar para chamar o evento `AdComplete` após a conclusão do primeiro anúncio. Certifique-se de chamar `trackEvent:AdComplete` para o último anúncio no ad break. Se o reprodutor identificar que o ativo de anúncio atual é o último no ad break, chame `trackEvent:AdComplete` imediatamente. Essa resolução resultará em menos de 1 segundo de tempo adicional gasto com o anúncio para a unidade de anúncio anterior.

**No início do ad break, incluindo precedente:**

* Crie a instância de objeto `adBreak` para o ad break; por exemplo, `adBreakObject`.

* Chame `trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);`.

**Em cada início de ativo de anúncio:**

* **Chame`trackEvent(MediaHeartbeat.Event.AdComplete);`**

  >[!NOTE]
  >
  >Chame isso somente se o anúncio anterior não tiver sido concluído. Considere um valor booleano para manter um estado &quot;`isinAd`&quot; para o anúncio anterior.

* Crie a instância do objeto de anúncio para o ativo de anúncio: por exemplo, `adObject`.
* Preencha os metadados do anúncio, `adCustomMetadata`.
* Chame `trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata);`.
* Chame `trackPlay()` se este for o primeiro anúncio em um ad break precedente.

**Em cada conclusão de ativo de anúncio:**

* **Não faça uma chamada**

  >[!NOTE]
  >
  >Se o aplicativo souber que se trata do último anúncio no ad break, chame `trackEvent:AdComplete` aqui e ignore a configuração de `trackEvent:AdComplete` no `trackEvent:AdBreakComplete`

**Ao ignorar o anúncio:**

* Chame `trackEvent(MediaHeartbeat.Event.AdSkip);`.

**Na conclusão do ad break:**

* **Chame`trackEvent(MediaHeartbeat.Event.AdComplete);`**

  >[!NOTE]
  >
  >Se esta etapa já tiver sido realizada como parte da última chamada `trackEvent:AdComplete`, isso poderá ser ignorado.

* Chame `trackEvent(MediaHeartbeat.Event.AdBreakComplete);`.
