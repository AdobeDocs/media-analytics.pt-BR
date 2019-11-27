---
title: Rastrear capítulos e segmentos no Android
description: Este tópico descreve a implementação do rastreamento de capítulo e segmento usando o SDK do Media no Android.
uuid: 013815d7-4d9e-48f4-a2b9-3b70cb1149d3
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Rastrear capítulos e segmentos no Android {#track-chapters-and-segments-on-android}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação usando SDKs 2.x. Se estiver implementando uma versão 1.x do SDK, você pode baixar o Guia dos desenvolvedores aqui: [Baixar SDKs.](/help/sdk-implement/download-sdks.md)

## Implementar o rastreamento de capítulo

1. Identifique quando ocorre o evento de início do capítulo e crie a instância `ChapterObject` usando as informações do capítulo.

   Referência de rastreamento de capítulo `ChapterObject`:

   >[!NOTE]
   >
   >Essas variáveis somente são necessárias se você estiver planejando rastrear capítulos.

   | Nome da variável | Descrição | Obrigatório |
   | --- | --- | :---: |
   | `name` | Nome do capítulo | Sim |
   | `position` | Posição do capítulo | Sim |
   | `length` | Extensão do capítulo | Sim |
   | `startTime` | Hora de início do capítulo | Sim |

   Objeto do capítulo:

   ```java
   MediaObject chapterDataInfo =  
     MediaHeartbeat.createChapterObject(<CHAPTER_NAME>,  
                                        <POSITION>,  
                                        <LENGTH>,  
                                        <START_TIME>);
   ```

1. Se você incluir metadados personalizados para o capítulo, crie as variáveis de dados de contexto para os metadados:

   ```java
   HashMap<String, String> chapterMetadata =  
     new HashMap<String,String>(); 
   chapterMetadata.put("segmentType", "Sample Segment Type"); 
   chapterMetadata.put("segmentName", "Sample Segment Name"); 
   chapterMetadata.put("segmentInfo", "Sample Segment Info");
   ```

1. Para começar a rastrear a reprodução do capítulo, chame o evento `ChapterStart` na instância `MediaHeartbeat`:

   ```java
   public void onChapterStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.ChapterStart,  
                             chapterDataInfo,  
                             chapterMetadata); 
   }
   ```

1. Quando a reprodução atingir o limite final do capítulo, conforme definido pelo seu código personalizado, chame o evento `ChapterComplete` na instância `MediaHeartbeat`:

   ```java
   public void onChapterComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.ChapterComplete, null, null); 
   }
   ```

1. Se a reprodução do capítulo não tiver sido concluída porque o usuário optou por ignorar o capítulo (por exemplo, se o usuário sair do limite do capítulo), chame o evento `ChapterSkip` na instância MediaHeartbeat:

   ```java
   public void onChapterSkip(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.ChapterSkip, null, null); 
   }
   ```

1. Se houver capítulos adicionais, repita as etapas de 1 até 5.

