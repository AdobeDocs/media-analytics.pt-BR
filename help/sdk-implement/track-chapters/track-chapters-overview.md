---
seo-title: Visão geral
title: Visão geral
uuid: 3 fe 32425-5 e 2 a -4886-8 fea-d 91 d 15671 bb 0
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Visão geral{#overview}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação usando sdks 2. x. Se estiver implementando uma versão 1.x do SDK, você pode baixar o Guia dos desenvolvedores aqui: [Baixar SDKs.](/help/sdk-implement/download-sdks.md)

O rastreamento de capítulo e segmento está disponível para capítulos de mídia personalizados ou segmentos. Alguns usos comuns do rastreamento de capítulo são definidos para definir segmentos personalizados com base no conteúdo da mídia (como o beisebol) ou definir segmentos de conteúdo entre intervalos de anúncios. Chapter tracking is **not** required for core media tracking implementations.

O rastreamento do capítulo inclui inícios de capítulo, conclusões de capítulo e capítulos ignorados. Você pode usar a API do player de mídia com lógica de segmentação personalizada para identificar eventos de capítulo e preencher as variáveis de capítulo opcionais e opcionais.

## Eventos do player

### No início do capítulo

* Criar a instância do objeto de anúncio para o capítulo, `chapterObject`
* Populate the chapter metadata, `chapterCustomMetadata`
* Chama `trackEvent(MediaHeartbeat.Event.ChapterStart, chapterObject, chapterCustomMetadata);`

### Na conclusão do capítulo

* Chama `trackEvent(MediaHeartbeat.Event.ChapterComplete);`

### Ao ignorar o capítulo

* Chama `trackEvent(MediaHeartbeat.Event.ChapterSkip);`

## Implement chapter tracking {#section_52221B3A9BFD46B3A22DA6BCE97CCD75}

1. Identifique quando ocorre o evento de início do capítulo e crie a instância `ChapterObject` usando as informações do capítulo.

   Aqui está a referência para o rastreamento de capítulo `ChapterObject`:

   >[!NOTE]
   >
   >Essas variáveis só serão necessárias se você estiver planejando rastrear capítulos.

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

O código de exemplo a seguir usa o SDK do javascript 2. x para um player de mídia HTML 5. Você deve usar este código com o código de reprodução de mídia principal.

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

## Validar {#section_07EC2811BE3249249494596BFE9BF869}

### Início do capítulo

Ao iniciar uma reprodução de capítulo individual, uma chamada de chave é enviada:

* Início do capítulo do Heartbeat (esta chamada contém variáveis adicionais de metadados de capítulo.)

### Capítulo concluído

No limite final de um capítulo, uma chamada de heartbeat de capítulo concluído será enviada.

### Capítulo ignorado

Quando um capítulo é ignorado, uma chamada de capítulo ignorado do Heartbeat é enviada.
