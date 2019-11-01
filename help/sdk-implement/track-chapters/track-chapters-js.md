---
title: Rastrear capítulos e segmentos no JavaScript
description: Este tópico descreve a implementação do rastreamento de capítulo e segmento usando o SDK de mídia em aplicativos de navegador (JS).
uuid: ef99edf7-7a77-46c4-8429-bc9a856b98d6
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Rastrear capítulos e segmentos no JavaScript{#track-chapters-and-segments-on-javascript}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação usando SDKs 2.x. Se estiver implementando uma versão 1.x do SDK, você pode baixar o Guia dos desenvolvedores aqui: [Baixar SDKs.](/help/sdk-implement/download-sdks.md)

1. Identifique quando ocorre o evento de início do capítulo e crie a instância `ChapterObject` usando as informações do capítulo.

   `ChapterObject` referência de rastreamento de capítulo:

   >[!NOTE]
   >
   >Essas variáveis só são necessárias se você estiver planejando rastrear capítulos.

   | Nome da variável | Descrição | Obrigatório |
   | --- | --- | :---: |
   | `name` | Nome do capítulo | Sim |
   | `position` | Posição do capítulo | Sim |
   | `length` | Extensão do capítulo | Sim |
   | `startTime` | Hora de início do capítulo | Sim |

   Objeto do capítulo:

   ```js
   var chapterInfo =  
     MediaHeartbeat.createChapterObject(<CHAPTER_NAME>,  
                                        <POSITION>,  
                                        <LENGTH>,  
                                        <START_TIME>);
   ```

1. Se você incluir metadados personalizados para o capítulo, crie as variáveis de dados de contexto para os metadados:

   ```js
   var chapterCustomMetadata = { 
       segmentType: "Sample segment type",  
       segmentName: "Sample segment name",  
       segmentInfo: "Sample segment info" 
   };
   ```

1. Para começar a rastrear a reprodução do capítulo, chame o evento `ChapterStart` na instância `MediaHeartbeat`:

   ```js
   _onChapterStart = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                                       chapterObject,  
                                       chapterCustomMetadata); 
   };
   ```

1. Quando a reprodução atingir o limite final do capítulo, conforme definido pelo seu código personalizado, chame o evento `ChapterComplete` na instância `MediaHeartbeat`:

   ```js
   _onChapterComplete = function() { 
      this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete); 
   };
   ```

1. Se a reprodução do capítulo não tiver sido concluída porque o usuário optou por ignorar o capítulo (por exemplo, se o usuário sair do limite do capítulo), chame o evento `ChapterSkip` na instância MediaHeartbeat:

   ```js
   _onChapterSkip = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip); 
   };
   ```

1. Se houver capítulos adicionais, repita as etapas de 1 até 5.

