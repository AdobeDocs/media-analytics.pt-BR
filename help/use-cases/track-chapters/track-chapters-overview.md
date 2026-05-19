---
title: Saiba como rastrear capítulos e segmentos
description: Como implementar o rastreamento de capítulo e segmento com o SDK de mídia.
uuid: 3fe32425-5e2a-4886-8fea-d91d15671bb0
exl-id: d213b633-be3b-4eb8-be71-0ef55e78a570
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/PAadkD9nJ7IRf7LdsNzIWtFp0yv54x0xV-Js-ona0Lg
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: 337
ht-degree: 95%

---

# Visão geral{#overview}

As instruções a seguir fornecem orientação para a implementação usando SDKs 2.x.

>[!IMPORTANT]
> 
> Se estiver implementando uma versão 1.x do SDK, você pode baixar o Guia dos desenvolvedores aqui: [Baixar SDKs.](/help/getting-started/download-sdks.md)

O rastreamento de capítulos e segmentos está disponível para capítulos ou segmentos de mídia definidos de forma personalizada. Alguns usos comuns para o rastreamento de capítulos são definir segmentos personalizados com base no conteúdo de mídia (como entradas de beisebol) ou definir segmentos de conteúdo entre ad breaks. O rastreamento de capítulos **não** é necessário para implementações de heartbeat de mídia principais.

O rastreamento do capítulo inclui inícios de capítulo, conclusões de capítulo e capítulos ignorados. Você pode usar a API do reprodutor de mídia com lógica de segmentação personalizada para identificar eventos do player e para preencher as variáveis de capítulo obrigatórias e opcionais.

## Eventos do player

### No início do capítulo

* Criar a instância do objeto de anúncio para o capítulo, `chapterObject`
* Preencha os metadados do capítulo, `chapterCustomMetadata`
* Chame `trackEvent(MediaHeartbeat.Event.ChapterStart, chapterObject, chapterCustomMetadata);`

### Na conclusão do capítulo

* Chame `trackEvent(MediaHeartbeat.Event.ChapterComplete);`

### Ao ignorar o capítulo

* Chame `trackEvent(MediaHeartbeat.Event.ChapterSkip);`

## Implementar o rastreamento de capítulo {#implement-chapter-tracking}

1. Identifique quando ocorre o evento de início do capítulo e crie a instância `ChapterObject` usando as informações do capítulo.

   Aqui está a referência para o rastreamento de capítulo `ChapterObject`:

   >[!NOTE]
   >
   >Essas variáveis somente são necessárias se você estiver planejando rastrear capítulos.

   | Nome da variável | Descrição | Obrigatório |
   | --- | --- | :---: |
   | `name` | Nome do capítulo | Sim |
   | `position` | Posição do capítulo | Sim |
   | `length` | Comprimento do capítulo | Sim |
   | `startTime` | Hora de início do capítulo | Sim |

1. Se você incluir metadados personalizados para o capítulo, crie as variáveis de dados de contexto para os metadados.
1. Para começar a rastrear a reprodução do capítulo, chame o evento `ChapterStart` na instância `MediaHeartbeat`.
1. Quando a reprodução atingir o limite final do capítulo, conforme definido pelo seu código personalizado, chame o evento `ChapterComplete` na instância `MediaHeartbeat`.
1. Se a reprodução do capítulo não tiver sido concluída porque o usuário optou por ignorar o capítulo (por exemplo, se o usuário sair do limite do capítulo), chame o evento `ChapterSkip` na instância MediaHeartbeat.
1. Se houver capítulos adicionais, repita as etapas de 1 até 5.

O código de exemplo a seguir usa o SDK 2.x do JavaScript para um reprodutor de mídia HTML5. Você deve usar esse código com o código de reprodução de mídia principal.

```js
/* Call on chapter start */
if (e.type == "chapter start") {
    var chapterObject = MediaHeartbeat.createChapterObject("Inning 5",5,500,2500);
    /* Set custom context data*/
    var chapterCustomMetadata = {
        segmentType:"Baseball Innings",
        segmentName:"Inning 5",
        segmentInfo:"Game Six"
    }
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                                   chapterObject,  
                                   chapterCustomMetadata);
};

/* Call on chapter complete */
if (e.type == "chapter complete") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete);
};

/* Call on chapter skip */
if (e.type == "chapter skip") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip);
};
```

>[!MORELIKETHIS]
>
>* [Início do capítulo](/help/implementation/events/chapters/chapter-start.md)
>* [Capítulo concluído](/help/implementation/events/chapters/chapter-complete.md)
>* [Capítulo ignorado](/help/implementation/events/chapters/chapter-skip.md)
