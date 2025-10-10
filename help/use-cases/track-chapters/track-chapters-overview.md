---
title: Saiba como rastrear capítulos e segmentos
description: Como implementar o rastreamento de capítulo e segmento com o SDK de mídia.
uuid: 3fe32425-5e2a-4886-8fea-d91d15671bb0
exl-id: d213b633-be3b-4eb8-be71-0ef55e78a570
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

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
   | `length` | Extensão do capítulo | Sim |
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
