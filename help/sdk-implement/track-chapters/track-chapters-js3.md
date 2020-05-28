---
title: Rastrear capítulos e segmentos usando o JavaScript 3.x
description: Este tópico descreve a implementação do rastreamento de capítulo e segmento usando o SDK do Media em aplicativos de navegador (JS).
translation-type: tm+mt
source-git-commit: b14b56aea4a1821a2a160b9cd301cd181f1ba8dd
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 71%

---


# Rastrear capítulos e segmentos usando o JavaScript 3.x{#track-chapters-and-segments-on-javascript}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação usando SDKs 3.x. If you are implementing any previous versions of the SDK, you can download the Developers Guide here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

1. Identifique quando ocorre o evento de início do capítulo e crie a instância `ChapterObject` usando as informações do capítulo.

   Referência de rastreamento de capítulo `ChapterObject`:

   >[!NOTE]
   >
   >Essas variáveis somente são necessárias se você estiver planejando rastrear capítulos.

   | Nome da variável | Tipo | Descrição |
   | --- | --- | --- |
   | `name` | string | Sequência de caracteres não vazia que denota o nome do capítulo. |
   | `position` | número | A posição do capítulo no conteúdo, começando com 1. |
   | `length` | número | Número positivo que indica o comprimento do capítulo. |
   | `startTime` | número | Valor do indicador de reprodução no start do capítulo. |

   Objeto do capítulo:

   ```js
   var chapterObject =
     ADB.Media.createChapterObject.createChapterObject(<CHAPTER_NAME>,
                                        <POSITION>,
                                        <LENGTH>,
                                        <START_TIME>);
   ```

1. Se você incluir metadados personalizados para o capítulo, crie as variáveis de dados de contexto para os metadados:

   ```js
   var chapterMetadata = {};
   chapterMetadata["segmentType"] = "Sample segment type";
   ```

1. Para começar a rastrear a reprodução do capítulo, chame o evento `ChapterStart` na instância `MediaHeartbeat`:

   ```js
   _onChapterStart = function() {
     tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterObject, chapterMetadata);
   
   };
   ```

1. Quando a reprodução atingir o limite final do capítulo, conforme definido pelo seu código personalizado, chame o evento `ChapterComplete` na instância `MediaHeartbeat`:

   ```js
   _onChapterComplete = function() {
      tracker.trackEvent(ADB.Media.Event.ChapterComplete);
   };
   ```

1. Se a reprodução do capítulo não tiver sido concluída porque o usuário optou por ignorar o capítulo (por exemplo, se o usuário sair do limite do capítulo), chame o evento `ChapterSkip` na instância MediaHeartbeat:

   ```js
   _onChapterSkip = function() {
       tracker.trackEvent(ADB.Media.Event.ChapterSkip);
   };
   ```

1. Se houver capítulos adicionais, repita as etapas de 1 até 5.
